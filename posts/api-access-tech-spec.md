[category]: <> (general)
[date]: <> (2026/02/03)
[title]: <> (API Access Tech Spec)


# API Access Tech Spec

The idea behind api access is to have a peripheral portal, where file operations can be done via an external API, LLMs, local servers, etc. There are two main components for this setup

1. **Ddoc Frontend**
    
    1. Deploys the peripheral portal
    2. Generates different associated keys
    3. Allows users to manage api keys
    4. Connects with the satellite package to list/show docs created via the api access
2. **Satellite Package**: IMP User needs to install this package for API access to work
    
    1. It’s a locally running server on users machine
    2. The user needs to install the package locally to be able to work with api access
    3. Acts as an interface for other outside APIs (LLms, external servers, etc.) that want to create/edit files
    4. Exposes list, read and other apis for the Ddoc frontend to consume
    5. Takes care of creating, editing, encrypting, and publishing a file

## Tech Specs FE

1. Content Hash: [Update in](https://github.com/fileverse/ddocs.new/blob/89294b1dc386a8466b689156c2f3ad173659ee8f/utils/content-hash/maps.ts)
    
    1. Code Name = `apiportal+ipfsenc://`
    2. Name to Varint = `Uint8Array.from([11])`
2. Some important Functions

Registry Address:

1. Sepolia: `0xbE1133bcDDCa3058fe641eb10A115CE8B6632213`
2. Gnosis: `0x94b1Eca21D327C4966F8F7547e2c21bDBd950b40`

**Mint Api Access Portal**

```ts
export const mintApiAccessPortal = async () => {
  const ownerEdKeyPair = await generateRandomUcanEdKeyPair();
  // ed secret
  const ownerSecret = await ownerEdKeyPair.export();
  // owner did
  const ownerDid = ownerEdKeyPair.did();

  const portalSeed = generateRandomBytes(24);
  const { publicKey, privateKey } = generateECKeyPair();

  const keyVerifiers = getPortalKeyVerifiers({
    appEncryptionKey: publicKey,
    appDecryptionKey: privateKey,
  })

  const encodedCallData = encodeFunctionData({
    abi: CONTRACT_ABI_MAP[ContractType.RegistryAppKey],
    functionName: ContractMethod.Mint,
    args: [
      PORTAL_METADATA_IPFS_HASH,
      ownerDid,
      keyVerifiers.appEncryptionKeyVerifier,
      keyVerifiers.appDecryptionKeyVerifier,
    ],
  });

  const receipt = await AgentInstance.executeUserOperationRequest({
    data: encodedCallData,
    contractAddress: REGISTRY_CONTRACT_ADDRESS,
  }, DEFAULT_TIMEOUT);

  if (!receipt.success) {
    throw new Error('Failed to mint api access portal');
  }
  const parsedLog = parseEventLogs({
    abi: CONTRACT_ABI_MAP[ContractType.RegistryAppKey],
    eventName: PortalContractEvent.Mint,
    logs: receipt.logs,
  });
  if (parsedLog.length === 0) {
    throw new Error('No Portal Mint Event Found (userOpHash: ${receipt.userOpHash})');
  }
  const portalAddress = (parsedLog[0]?.args as any)?.app as Hex;
  if (!portalAddress) {
    throw new Error('Portal address not found in Mint event');
  }



  return {
    owner: AgentInstance.getAgentAddress(),
    portalAddress,
    credentials: {
      ownerDid,
      ownerSecret,
    },
    appKeys: {
      appEncryptionKey: fromUint8Array(publicKey),
      appDecryptionKey: fromUint8Array(privateKey),
    },
    portalKeySeed: fromUint8Array(portalSeed),
  };
}
```

**Check If Api key portal is already deployed**

```ts

// Get all address in the keystore
export const getKeyStoreAddresses = async (
  walletAddress: Hex,
  identityModuleAddress: Hex
) => {
  const response = await publicClient.readContract({
    abi: IDENTITY_MODULE_ABI,
    address: identityModuleAddress,
    functionName: IdentityModuleMethod.GetKeyStoreAddresses,
    account: walletAddress,
  });

  return response as Hex[];
};



export const getApiKeyStoreFromContract = async (
  keyStoreAddresses: Hex[],
  walletAddress: Hex,
  identityModuleAddress: Hex
) => {
  const response = (await publicClient.readContract({
    abi: IDENTITY_MODULE_ABI,
    address: identityModuleAddress,
    functionName: IdentityModuleMethod.GetIdentityModuleKeyStoreDetails,
    args: [keyStoreAddresses],
    account: walletAddress,
  })) as Hex[];

  for (let i = 0; i < response.length; i++) {
    const hash = response[i];
    const address = keyStoreAddresses[i];

    if (ContentHash.isOfType(hash, "apiportal+ipfsenc://")) {
      const encryptedHash = ContentHash.decode(hash);

      const decryptedHash = bytesToString(
        await IdentityInstance.decryptEnvelope(encryptedHash)
      );

      return {
        address: address,
        hash: decryptedHash
      }
    }
  }

  return undefined;
};
```

**Remove Collaborator**

```ts
export const removeCollaboratorKeysCall = async (collaboratorAgent: AgentClient, appAddress: Hex) => {
  const callData = encodeFunctionData({
    abi: CONTRACT_ABI_MAP[ContractType.PortalAppKey],
    functionName: 'removeCollaboratorKeys',
    args: [],
  });

  const receipt = await collaboratorAgent.executeUserOperationRequest({
    data: callData,
    contractAddress: appAddress,
  }, DEFAULT_TIMEOUT);

  if (!receipt.success) {
    throw new Error('Failed to remove collaborator keys');
  }

  const parsedLog = parseEventLogs({
    abi: CONTRACT_ABI_MAP[ContractType.PortalAppKey],
    eventName: PortalContractEvent.RemovedCollaboratorKeys,
    logs: receipt.logs,
  });

  if (parsedLog.length === 0) {
    throw new Error('Failed to remove collaborator keys');
  }

  return { userOpHash: receipt.userOpHash };
}



export const removeCollaboratorCall = async (appAddress: Hex, collaboratorAddress: Hex) => {
  const existingCollaborators = await publicClient.readContract({
    address: appAddress,
    abi: CONTRACT_ABI_MAP[ContractType.PortalAppKey],
    functionName: 'getCollaborators',
  }) as Hex[];

  if (!existingCollaborators.includes(collaboratorAddress)) {
    throw new Error('Collaborator not found');
  }

  // find previous collaborator address, meaning the collaborator just before the collaborator to be removed
  const previousCollaboratorAddress = existingCollaborators[existingCollaborators.indexOf(collaboratorAddress) - 1];

  const callData = encodeFunctionData({
    abi: CONTRACT_ABI_MAP[ContractType.PortalAppKey],
    functionName: 'removeCollaborator',
    args: [previousCollaboratorAddress, collaboratorAddress],
  });

  const receipt = await AgentInstance.executeUserOperationRequest({
    data: callData,
    contractAddress: appAddress,
  }, DEFAULT_TIMEOUT);

  if (!receipt.success) {
    throw new Error('Failed to remove collaborator');
  }

  return { userOpHash: receipt.userOpHash };

}
```

**Register Collaborator**

```ts
export const registerCollaborator = async (args: {
  portalAddress: Hex;
  privateAccountKey: Uint8Array;
  collaboratorDid: string;
}) => {
  const collaboratorAgent = new AgentClient();
  await collaboratorAgent.initializeAgentClient(args.privateAccountKey);

//Function already in code
  await addCollaboratorCall({
    appAddress: args.portalAddress,
    collaboratorAddress: collaboratorAgent.getAgentAddress(),
  });
  await registerCollaboratorKeysCall(collaboratorAgent, {
    appAddress: args.portalAddress,
    collaboratorDid: args.collaboratorDid,
  });
  return collaboratorAgent;
};
```

**Register Collaborator Keys**

```ts
export const registerCollaboratorKeysCall = async (collaboratorAgent: AgentClient, args: {
  appAddress: Hex;
  collaboratorDid: string;

}) => {
  const callData = encodeFunctionData({
    abi: CONTRACT_ABI_MAP[ContractType.PortalAppKey],
    functionName: ContractMethod.RegisterCollaboratorKeys,
    args: [args.collaboratorDid],
  });

  const receipt = await collaboratorAgent.executeUserOperationRequest({
    data: callData,
    contractAddress: args.appAddress,
  }, DEFAULT_TIMEOUT);

  if (!receipt.success) {
    throw new Error('Failed to register collaborator keys');
  }

  const parsedLog = parseEventLogs({
    abi: CONTRACT_ABI_MAP[ContractType.PortalAppKey],
    eventName: PortalContractEvent.RegisteredCollaboratorKeys,
    logs: receipt.logs,
  });

  if (parsedLog.length === 0) {
    throw new Error('Failed to register collaborator keys');
  }

  return { userOpHash: receipt.userOpHash };
}
```

**Derive Collaborator Key Material**

```ts


export const deriveCollaboratorMaterial = (apiKeySeed: Uint8Array) => {
  const salt = new Uint8Array([0]);
  const privateAccountKey = deriveHKDFKey(
    apiKeySeed,
    salt,
    stringToBytes('COLLABORATOR_PRIVATE_KEY')
  );
  
  const collaboratorDerivedUcanSecret = deriveHKDFKey(
    apiKeySeed,
    salt,
    stringToBytes('COLLABORATOR_UCAN_SECRET')
  );
  const { secretKey: ucanSecret } = generateKeyPairFromSeed(collaboratorDerivedUcanSecret)
  const edKeyPair = ucans.EdKeypair.fromSecretKey(fromUint8Array(ucanSecret), {
    exportable: true,
  });
  const collaboratorDid = edKeyPair.did();
  return { privateAccountKey, collaboratorDid };
};
```

**Buld Api Key Store JSON**

```ts
export const buildApiKeyStoreJson = async (args: {
  portalKeySeed: string;
  apiKeys: unknown;
  portalAddress: Hex;
  ownerDid: string;
  ownerSecret: string;
  appDecryptionKey: string;
  enabled: boolean;
}) => {
  return {
    portalKeySeed: await IdentityInstance.encryptEnvelope(
      toUint8Array(args.portalKeySeed)
    ),
    apiKeys: await IdentityInstance.encryptEnvelope(
      stringToBytes(JSON.stringify(args.apiKeys))
    ),
    portalAddress: args.portalAddress,
    ownerDid: args.ownerDid,
    encryptedOwnerSecret: await IdentityInstance.encryptEnvelope(
      toUint8Array(args.ownerSecret)
    ),
    encryptedAppDecryptionKey: await IdentityInstance.encryptEnvelope(
      toUint8Array(args.appDecryptionKey)
    ),
    enabled: args.enabled
  };
};
```

**Update Api Key Store**

```ts

export const updateApiKeyStore = async (args: {
  portalAddress: Hex;
  ipfsHash: string;
  contentHashName: string;
}) => {
  const encryptedKeyStoreIPFS = await IdentityInstance.encryptEnvelope(
    stringToBytes(args.ipfsHash)
  );

  const callData = encodeFunctionData({
    abi: IDENTITY_MODULE_ABI,
    functionName: IdentityModuleMethod.UpdateKeyStoreContract,
    args: [
      ContentHash.encode(args.contentHashName, encryptedKeyStoreIPFS),
      args.portalAddress,
    ],
  });

  const receipt = await AgentInstance.executeUserOperationRequest(
    {
      data: callData,
      contractAddress: IdentityInstance.getIdentityAddress(),
    },
    DEFAULT_TIMEOUT
  );

  if (!receipt.success) {
    throw new Error('Failed to update keystore data');
  }

  const parsedLogs = parseEventLogs({
    abi: IDENTITY_MODULE_ABI,
    eventName: 'UpdateKeyStoreContract',
    logs: receipt.logs,
  });

  if (parsedLogs.length === 0) {
    throw new Error(
      `No UpdateKeyStoreContract Event Found (userOpHash: ${receipt.userOpHash})`
    );
  }
};
```

```ts


//Base Key Store interface = Same as NewKeyStore
interface BaseKeyStore {
  portalAddress: Hex;
  ownerDid: string;
  ownerSecret: string;
  appEncryptionKey: string;
  appDecryptionKey: string;
}

interface ApiKeyInfo {
  apiKeySeed: string; //base64 string
  collaboratorAddress: Hex;
  name: string;
  createdAt: number;
}

interface ApiAccessKeyStore extends BaseKeyStore {
  portalKeySeed: string; // Uint8Array to urlSafe base64 String also encrypted
  apiKeys: ApiKeyInfo[]; // when store on key store whole array is encrypted
  enabled: boolean;
}

// Exact class
class ApiKeyStore {
  private portalAddress: Hex;
  private ownerDid: string;
  private ownerSecret: string;
  private appEncryptionKey: string;
  private appDecryptionKey: string;
  private ucanToken?: string; // Not necessary I guess
  // new fields
  private portalKeySeed: string;
  apiKeys: ApiKeyInfo[];
  constructor(keyStoreData: ApiAccessKeyStore){}
  
  // Boiler plate code
  getPortalAddress(): Hex {}
  async encryptData(data: Uint8Array): Promise<string>{
   return eciesEncrypt(toBytes(this.appEncryptionKey), data);
  }
  async decryptData(data: string): Promise<string> {
    return eciesDecrypt(toBytes(this.appDecryptionKey), data);
  }

  // Api access keystore specific methods
  getApiKeyDetails(name: string): ApiKeyInfo {
   // filter this.apiKeys by name
  } 

   async addNewApiKey(name: string) {
    if (this.apiKeys.find(key => key.name === name)) {
      throw new Error('Api key already exists');
    }
    const apiKeySeed = generateRandomBytes(32)
    const { privateAccountKey, collaboratorDid } = deriveCollaboratorMaterial(apiKeySeed);
    const collaboratorAgent = await registerCollaborator({
      portalAddress: this.portalAddress,
      privateAccountKey,
      collaboratorDid,
    });
    const newApiKeyInfo = {
      apiKeySeed: fromUint8Array(apiKeySeed, true),
      collaboratorAddress: collaboratorAgent.getAgentAddress(),
      name: name,
      createdAt: Date.now(),
    };

    const newApiKeys = [...this.apiKeys, newApiKeyInfo];
    const apiKeyStoreJSON = await buildApiKeyStoreJson({
      portalKeySeed: this.portalKeySeed,
      apiKeys: newApiKeys,
      portalAddress: this.portalAddress,
      ownerDid: this.ownerDid,
      ownerSecret: this.ownerSecret,
      appDecryptionKey: this.appDecryptionKey,
    });
    const ipfsHash = await uploadApiKeyStore(apiKeyStoreJSON);
    await updateApiKeyStore({
      portalAddress: this.portalAddress,
      ipfsHash,
      contentHashName: 'apiportal+ipfsenc://',
    });
    this.apiKeys = newApiKeys;
    // call satellite package to save the api key info
    // update indexeDB cache
  }

  async removeApiKey(name: string){
     const apiKeyInfo = this.apiKeys.find(key => key.name === name)
    if (!apiKeyInfo) {
      throw new Error('Api key not found');
    }
    const { privateAccountKey } = deriveCollaboratorMaterial(toBytes(apiKeyInfo.apiKeySeed));
    const collaboratorAgent = new AgentClient();
    await collaboratorAgent.initializeAgentClient(privateAccountKey);

    await removeCollaboratorKeysCall(collaboratorAgent, this.portalAddress);

    await removeCollaboratorCall(this.portalAddress, apiKeyInfo.collaboratorAddress);

    this.apiKeys = this.apiKeys.filter(key => key.name !== name);
    const apiKeyStoreJSON = await buildApiKeyStoreJson({
      portalKeySeed: this.portalKeySeed,
      apiKeys: this.apiKeys,
      portalAddress: this.portalAddress,
      ownerDid: this.ownerDid,
      ownerSecret: this.ownerSecret,
      appDecryptionKey: this.appDecryptionKey,
    });
    const ipfsHash = await uploadApiKeyStore(apiKeyStoreJSON);
    await updateApiKeyStore({
      portalAddress: this.portalAddress,
      ipfsHash,
      contentHashName: 'apiportal+ipfsenc://',
    });

    // call satellite package to remove api key from satellite
    // await removeApiKeyFromSatellite(apiKeyInfo.collaboratorAddress);
    // update indexedb cache
  }
}
```

User Flows:

1. User toggles Developer Mode - On
    
    1. Check if the keystore already contains a api access portal
    2. If not, `Mint Api Access Portal` portal
    3. Update Keystore as explained above in the code blocks
    4. Call the satellite package to save the api access portal info
        
        1. Portal Address
        2. Portal Key Seed
    5. Save in indexedb cache
2. User toggles Developer mode - Off
    
    1. Remove all collaborators from the api access portal except the owner
    2. Update key store as explained above in the code blocks
        
        1. Set enabled field to false
3. User clicks on Generate new api key
    
    1. On `ApiKeyStoreInstance` call the `addNewApiKey` method on the instance
4. User clicks on Remove Api Key
    
    1. On `ApiKeyStoreInstance` call the `removeApiKey` method on the instance

List Api Access Docs:

This is going to be a fetch call to the satellite package