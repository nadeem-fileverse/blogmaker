[category]: <> (general)
[date]: <> (2026/02/03)
[title]: <> (Idea 1:)


Idea 1:

**Ephemeral Content Key + Static Envelope**

1. Encryption Flow
    
    1. We have a static Link Key
    2. Generate Ephermal Secret → Wrapping Key → kdf\_key - PBKDF2
    3. kdfKey encrypts content key(Penumbra Key) → encrypted\_k\_content
    4. Link Key encrypts the ephermal secret → encrypted\_ephemeral\_secret
    5. Content Key encrypts conten → encrypted\_content

Items to store in metadata

```plaintext
{
encrypted_k_content,
encrypted_ephemeral_secret,
iv1, iv2, iv3,
salt used for PBKDF
}
```

2. Decryption Flow
    
    1. Link Key decrypts encrypted\_ephemeral\_secret → ephermal\_secret
    2. kdf\_key is derived back from ephermal\_secret → kdf\_key
    3. kdf\_key decrypts the encrypted\_k\_content → k\_content
    4. k\_content decrypts content

In this whole flow the core problem remains same as IPFS hashes are available on public nodes any one can regenerate key meaning cant revoke past content access to doc

===

Idea 2

**Versioned Key Derivation from Link Key**

1. Derive per version key → HMAC(LinkKey, vN) → kN
2. Encrypt content Key (Penumbra Key) with kN

On IPFS

```ts
{
  version: vN
  iv: string,
encrypted_k_content: string
}
```