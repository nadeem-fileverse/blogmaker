[category]: <> (general)
[date]: <> (2026/03/09)
[title]: <> (Some ways to use ZK-SNARKs for privacysdasdasdqweq)


# Some ways to use ZK-SNARKs for privacysdasdasdqweqweasdasdasdqweqwe

ZK-SNARKs are a powerful cryptographic tool, and an increasingly important part of the applications that people are building both in the blockchain space and beyond. But they are complicated, both in terms of _how they work_, and in terms of _how you can use them_.

## What does a ZK-SNARK do? ssssss sadasdqweqeqwe

Suppose that you have a public input x, a private input w, and a (public) function f(x,w)→{True,False} that performs some kind of verification on the inputs. With a ZK-SNARK, you can prove that you know an w such that f(x,w)=True for some given f and x, without revealing what w is. Additionally, the verifier can verify the proof much faster than it would take for them to compute f(x,w) themselves, even if they know w.

![](https://vitalik.eth.limo/images/using_snarks/definition.png)

This gives the ZK-SNARK its two properties: **privacy** and **scalability**. As mentioned above, in this post our examples will focus on privacy.

## Holding centralized parties accountable

Sometimes, you need to build a scheme that has a central "operator" of some kind. This could be for many reasons: sometimes it's for scalability, and sometimes it's for privacy - specifically, the privacy of data held by the operator.

The MACI coercion-resistant voting system, for example, requires voters to submit their votes on-chain encrypted to a secret key held by a central operator. The operator would decrypt all the votes on-chain, count them up, and reveal the final result, along with a ZK-SNARK proving that they did everything correctly. This extra complexity is necessary to ensure a strong privacy property (called **coercion-resistance**): that users cannot prove to others how they voted even if they wanted to.

Thanks to blockchains and ZK-SNARKs, the amount of trust in the operator can be kept very low. A malicious operator could still break coercion resistance, but because votes are published on the blockchain, the operator cannot cheat by censoring votes, and because the operator must provide a ZK-SNARK, they cannot cheat by mis-calculating the result.

## Combining ZK-SNARKs with MPC

A more advanced use of ZK-SNARKs involves making proofs over computations where the inputs are split between two or more parties, and we don't want each party to learn the other parties' inputs. You can satisfy the privacy requirement with [garbled circuits](https://vitalik.eth.limo/general/2020/03/21/garbled.html) in the 2-party case, and more complicated multi-party computation protocols in the N-party case. ZK-SNARKs can be combined with these protocols to do verifiable multi-party computation.

This could enable more advanced reputation systems where multiple participants can perform joint computations over their private inputs, it could enable privacy-preserving but authenticated data markets, and many other applications. That said, note that the math for doing this efficiently is still relatively in its infancy.

> Read the full article by [Vitalik Buterin](https://vitalik.eth.limo/general/2021/01/26/snarks.html)

# Some ways to use ZK-SNARKs for privacy

ZK-SNARKs are a powerful cryptographic tool, and an increasingly important part of the applications that people are building both in the blockchain space and beyond. But they are complicated, both in terms of _how they work_, and in terms of _how you can use them_.

## What does a ZK-SNARK do?

Suppose that you have a public input x, a private input w, and a (public) function f(x,w)→{True,False} that performs some kind of verification on the inputs. With a ZK-SNARK, you can prove that you know an w such that f(x,w)=True for some given f and x, without revealing what w is. Additionally, the verifier can verify the proof much faster than it would take for them to compute f(x,w) themselves, even if they know w.bbbb

![](https://vitalik.eth.limo/images/using_snarks/definition.png)

This gives the ZK-SNARK its two properties: **privacy** and **scalability**. As mentioned above, in this post our examples will focus on privacy.

## Holding centralized parties accountable

Sometimes, you need to build a scheme that has a central "operator" of some kind. This could be for many reasons: sometimes it's for scalability, and sometimes it's for privacy - specifically, the privacy of data held by the operator.

The MACI coercion-resistant voting system, for example, requires voters to submit their votes on-chain encrypted to a secret key held by a central operator. The operator would decrypt all the votes on-chain, count them up, and reveal the final result, along with a ZK-SNARK proving that they did everything correctly. This extra complexity is necessary to ensure a strong privacy property (called **coercion-resistance**): that users cannot prove to others how they voted even if they wanted to.

Thanks to blockchains and ZK-SNARKs, the amount of trust in the operator can be kept very low. A malicious operator could still break coercion resistance, but because votes are published on the blockchain, the operator cannot cheat by censoring votes, and because the operator must provide a ZK-SNARK, they cannot cheat by mis-calculating the result.

## Combining ZK-SNARKs with MPC

A more advanced use of ZK-SNARKs involves making proofs over computations where the inputs are split between two or more parties, and we don't want each party to learn the other parties' inputs. You can satisfy the privacy requirement with [garbled circuits](https://vitalik.eth.limo/general/2020/03/21/garbled.html) in the 2-party case, and more complicated multi-party computation protocols in the N-party case. ZK-SNARKs can be combined with these protocols to do verifiable multi-party computation.

This could enable more advanced reputation systems where multiple participants can perform joint computations over their private inputs, it could enable privacy-preserving but authenticated data markets, and many other applications. That said, note that the math for doing this efficiently is still relatively in its infancy.

> Read the full article by [Vitalik Buterin](https://vitalik.eth.limo/general/2021/01/26/snarks.html)

# Some ways to use ZK-SNARKs for privacy

ZK-SNARKs are a powerful cryptographic tool, and an increasingly important part of the applications that people are building both in the blockchain space and beyond. But they are complicated, both in terms of _how they work_, and in terms of _how you can use them_.

## What does a ZK-SNARK do?

Suppose that you have a public input x, a private input w, and a (public) function f(x,w)→{True,False} that performs some kind of verification on the inputs. With a ZK-SNARK, you can prove that you know an w such that f(x,w)=True for some given f and x, without revealing what w is. Additionally, the verifier can verify the proof much faster than it would take for them to compute f(x,w) themselves, even if they know w.

![](https://vitalik.eth.limo/images/using_snarks/definition.png)

This gives the ZK-SNARK its two properties: **privacy** and **scalability**. As mentioned above, in this post our examples will focus on privacy.

## Holding centralized parties accountable

Sometimes, you need to build a scheme that has a central "operator" of some kind. This could be for many reasons: sometimes it's for scalability, and sometimes it's for privacy - specifically, the privacy of data held by the operator.

The MACI coercion-resistant voting system, for example, requires voters to submit their votes on-chain encrypted to a secret key held by a central operator. The operator would decrypt all the votes on-chain, count them up, and reveal the final result, along with a ZK-SNARK proving that they did everything correctly. This extra complexity is necessary to ensure a strong privacy property (called **coercion-resistance**): that users cannot prove to others how they voted even if they wanted to.

Thanks to blockchains and ZK-SNARKs, the amount of trust in the operator can be kept very low. A malicious operator could still break coercion resistance, but because votes are published on the blockchain, the operator cannot cheat by censoring votes, and because the operator must provide a ZK-SNARK, they cannot cheat by mis-calculating the result.

## Combining ZK-SNARKs with MPC

A more advanced use of ZK-SNARKs involves making proofs over computations where the inputs are split between two or more parties, and we don't want each party to learn the other parties' inputs. You can satisfy the privacy requirement with [garbled circuits](https://vitalik.eth.limo/general/2020/03/21/garbled.html) in the 2-party case, and more complicated multi-party computation protocols in the N-party case. ZK-SNARKs can be combined with these protocols to do verifiable multi-party computation.

This could enable more advanced reputation systems where multiple participants can perform joint computations over their private inputs, it could enable privacy-preserving but authenticated data markets, and many other applications. That said, note that the math for doing this efficiently is still relatively in its infancy.

> Read the full article by [Vitalik Buterin](https://vitalik.eth.limo/general/2021/01/26/snarks.html)

# Some ways to use ZK-SNARKs for privacy

ZK-SNARKs are a powerful cryptographic tool, and an increasingly important part of the applications that people are building both in the blockchain space and beyond. But they are complicated, both in terms of _how they work_, and in terms of _how you can use them_.

## What does a ZK-SNARK do?

Suppose that you have a public input x, a private input w, and a (public) function f(x,w)→{True,False} that performs some kind of verification on the inputs. With a ZK-SNARK, you can prove that you know an w such that f(x,w)=True for some given f and x, without revealing what w is. Additionally, the verifier can verify the proof much faster than it would take for them to compute f(x,w) themselves, even if they know w.

![](https://vitalik.eth.limo/images/using_snarks/definition.png)

This gives the ZK-SNARK its two properties: **privacy** and **scalability**. As mentioned above, in this post our examples will focus on privacy.

## Holding centralized parties accountable

Sometimes, you need to build a scheme that has a central "operator" of some kind. This could be for many reasons: sometimes it's for scalability, and sometimes it's for privacy - specifically, the privacy of data held by the operator.

The MACI coercion-resistant voting system, for example, requires voters to submit their votes on-chain encrypted to a secret key held by a central operator. The operator would decrypt all the votes on-chain, count them up, and reveal the final result, along with a ZK-SNARK proving that they did everything correctly. This extra complexity is necessary to ensure a strong privacy property (called **coercion-resistance**): that users cannot prove to others how they voted even if they wanted to.

Thanks to blockchains and ZK-SNARKs, the amount of trust in the operator can be kept very low. A malicious operator could still break coercion resistance, but because votes are published on the blockchain, the operator cannot cheat by censoring votes, and because the operator must provide a ZK-SNARK, they cannot cheat by mis-calculating the result.

## Combining ZK-SNARKs with MPC

A more advanced use of ZK-SNARKs involves making proofs over computations where the inputs are split between two or more parties, and we don't want each party to learn the other parties' inputs. You can satisfy the privacy requirement with [garbled circuits](https://vitalik.eth.limo/general/2020/03/21/garbled.html) in the 2-party case, and more complicated multi-party computation protocols in the N-party case. ZK-SNARKs can be combined with these protocols to do verifiable multi-party computation.

This could enable more advanced reputation systems where multiple participants can perform joint computations over their private inputs, it could enable privacy-preserving but authenticated data markets, and many other applications. That said, note that the math for doing this efficiently is still relatively in its infancy.

> Read the full article by [Vitalik Buterin](https://vitalik.eth.limo/general/2021/01/26/snarks.html)

# Some ways to use ZK-SNARKs for privacy

ZK-SNARKs are a powerful cryptographic tool, and an increasingly important part of the applications that people are building both in the blockchain space and beyond. But they are complicated, both in terms of _how they work_, and in terms of _how you can use them_.

## What does a ZK-SNARK do?

Suppose that you have a public input x, a private input w, and a (public) function f(x,w)→{True,False} that performs some kind of verification on the inputs. With a ZK-SNARK, you can prove that you know an w such that f(x,w)=True for some given f and x, without revealing what w is. Additionally, the verifier can verify the proof much faster than it would take for them to compute f(x,w) themselves, even if they know w.

![](https://vitalik.eth.limo/images/using_snarks/definition.png)

This gives the ZK-SNARK its two properties: **privacy** and **scalability**. As mentioned above, in this post our examples will focus on privacy.

## Holding centralized parties accountable

Sometimes, you need to build a scheme that has a central "operator" of some kind. This could be for many reasons: sometimes it's for scalability, and sometimes it's for privacy - specifically, the privacy of data held by the operator.

The MACI coercion-resistant voting system, for example, requires voters to submit their votes on-chain encrypted to a secret key held by a central operator. The operator would decrypt all the votes on-chain, count them up, and reveal the final result, along with a ZK-SNARK proving that they did everything correctly. This extra complexity is necessary to ensure a strong privacy property (called **coercion-resistance**): that users cannot prove to others how they voted even if they wanted to.

Thanks to blockchains and ZK-SNARKs, the amount of trust in the operator can be kept very low. A malicious operator could still break coercion resistance, but because votes are published on the blockchain, the operator cannot cheat by censoring votes, and because the operator must provide a ZK-SNARK, they cannot cheat by mis-calculating the result.

## Combining ZK-SNARKs with MPC

A more advanced use of ZK-SNARKs involves making proofs over computations where the inputs are split between two or more parties, and we don't want each party to learn the other parties' inputs. You can satisfy the privacy requirement with [garbled circuits](https://vitalik.eth.limo/general/2020/03/21/garbled.html) in the 2-party case, and more complicated multi-party computation protocols in the N-party case. ZK-SNARKs can be combined with these protocols to do verifiable multi-party computation.

This could enable more advanced reputation systems where multiple participants can perform joint computations over their private inputs, it could enable privacy-preserving but authenticated data markets, and many other applications. That said, note that the math for doing this efficiently is still relatively in its infancy.

> Read the full article by [Vitalik Buterin](https://vitalik.eth.limo/general/2021/01/26/snarks.html)

# Some ways to use ZK-SNARKs for privacy

ZK-SNARKs are a powerful cryptographic tool, and an increasingly important part of the applications that people are building both in the blockchain space and beyond. But they are complicated, both in terms of _how they work_, and in terms of _how you can use them_.

## What does a ZK-SNARK do?

Suppose that you have a public input x, a private input w, and a (public) function f(x,w)→{True,False} that performs some kind of verification on the inputs. With a ZK-SNARK, you can prove that you know an w such that f(x,w)=True for some given f and x, without revealing what w is. Additionally, the verifier can verify the proof much faster than it would take for them to compute f(x,w) themselves, even if they know w.

![](https://vitalik.eth.limo/images/using_snarks/definition.png)

This gives the ZK-SNARK its two properties: **privacy** and **scalability**. As mentioned above, in this post our examples will focus on privacy.

## Holding centralized parties accountable

Sometimes, you need to build a scheme that has a central "operator" of some kind. This could be for many reasons: sometimes it's for scalability, and sometimes it's for privacy - specifically, the privacy of data held by the operator.

The MACI coercion-resistant voting system, for example, requires voters to submit their votes on-chain encrypted to a secret key held by a central operator. The operator would decrypt all the votes on-chain, count them up, and reveal the final result, along with a ZK-SNARK proving that they did everything correctly. This extra complexity is necessary to ensure a strong privacy property (called **coercion-resistance**): that users cannot prove to others how they voted even if they wanted to.

Thanks to blockchains and ZK-SNARKs, the amount of trust in the operator can be kept very low. A malicious operator could still break coercion resistance, but because votes are published on the blockchain, the operator cannot cheat by censoring votes, and because the operator must provide a ZK-SNARK, they cannot cheat by mis-calculating the result.

## Combining ZK-SNARKs with MPC

A more advanced use of ZK-SNARKs involves making proofs over computations where the inputs are split between two or more parties, and we don't want each party to learn the other parties' inputs. You can satisfy the privacy requirement with [garbled circuits](https://vitalik.eth.limo/general/2020/03/21/garbled.html) in the 2-party case, and more complicated multi-party computation protocols in the N-party case. ZK-SNARKs can be combined with these protocols to do verifiable multi-party computation.

This could enable more advanced reputation systems where multiple participants can perform joint computations over their private inputs, it could enable privacy-preserving but authenticated data markets, and many other applications. That said, note that the math for doing this efficiently is still relatively in its infancy.

> Read the full article by [Vitalik Buterin](https://vitalik.eth.limo/general/2021/01/26/snarks.html)

# Some ways to use ZK-SNARKs for privacy

ZK-SNARKs are a powerful cryptographic tool, and an increasingly important part of the applications that people are building both in the blockchain space and beyond. But they are complicated, both in terms of _how they work_, and in terms of _how you can use them_.

## What does a ZK-SNARK do?

Suppose that you have a public input x, a private input w, and a (public) function f(x,w)→{True,False} that performs some kind of verification on the inputs. With a ZK-SNARK, you can prove that you know an w such that f(x,w)=True for some given f and x, without revealing what w is. Additionally, the verifier can verify the proof much faster than it would take for them to compute f(x,w) themselves, even if they know w.

![](https://vitalik.eth.limo/images/using_snarks/definition.png)

This gives the ZK-SNARK its two properties: **privacy** and **scalability**. As mentioned above, in this post our examples will focus on privacy.

## Holding centralized parties accountable

Sometimes, you need to build a scheme that has a central "operator" of some kind. This could be for many reasons: sometimes it's for scalability, and sometimes it's for privacy - specifically, the privacy of data held by the operator.

The MACI coercion-resistant voting system, for example, requires voters to submit their votes on-chain encrypted to a secret key held by a central operator. The operator would decrypt all the votes on-chain, count them up, and reveal the final result, along with a ZK-SNARK proving that they did everything correctly. This extra complexity is necessary to ensure a strong privacy property (called **coercion-resistance**): that users cannot prove to others how they voted even if they wanted to.

Thanks to blockchains and ZK-SNARKs, the amount of trust in the operator can be kept very low. A malicious operator could still break coercion resistance, but because votes are published on the blockchain, the operator cannot cheat by censoring votes, and because the operator must provide a ZK-SNARK, they cannot cheat by mis-calculating the result.

## Combining ZK-SNARKs with MPC

A more advanced use of ZK-SNARKs involves making proofs over computations where the inputs are split between two or more parties, and we don't want each party to learn the other parties' inputs. You can satisfy the privacy requirement with [garbled circuits](https://vitalik.eth.limo/general/2020/03/21/garbled.html) in the 2-party case, and more complicated multi-party computation protocols in the N-party case. ZK-SNARKs can be combined with these protocols to do verifiable multi-party computation.

This could enable more advanced reputation systems where multiple participants can perform joint computations over their private inputs, it could enable privacy-preserving but authenticated data markets, and many other applications. That said, note that the math for doing this efficiently is still relatively in its infancy.

> Read the full article by [Vitalik Buterin](https://vitalik.eth.limo/general/2021/01/26/snarks.html)

# Some ways to use ZK-SNARKs for privacy

ZK-SNARKs are a powerful cryptographic tool, and an increasingly important part of the applications that people are building both in the blockchain space and beyond. But they are complicated, both in terms of _how they work_, and in terms of _how you can use them_.

## What does a ZK-SNARK do?

Suppose that you have a public input x, a private input w, and a (public) function f(x,w)→{True,False} that performs some kind of verification on the inputs. With a ZK-SNARK, you can prove that you know an w such that f(x,w)=True for some given f and x, without revealing what w is. Additionally, the verifier can verify the proof much faster than it would take for them to compute f(x,w) themselves, even if they know w.

![](https://vitalik.eth.limo/images/using_snarks/definition.png)

This gives the ZK-SNARK its two properties: **privacy** and **scalability**. As mentioned above, in this post our examples will focus on privacy.

## Holding centralized parties accountable

Sometimes, you need to build a scheme that has a central "operator" of some kind. This could be for many reasons: sometimes it's for scalability, and sometimes it's for privacy - specifically, the privacy of data held by the operator.

The MACI coercion-resistant voting system, for example, requires voters to submit their votes on-chain encrypted to a secret key held by a central operator. The operator would decrypt all the votes on-chain, count them up, and reveal the final result, along with a ZK-SNARK proving that they did everything correctly. This extra complexity is necessary to ensure a strong privacy property (called **coercion-resistance**): that users cannot prove to others how they voted even if they wanted to.

Thanks to blockchains and ZK-SNARKs, the amount of trust in the operator can be kept very low. A malicious operator could still break coercion resistance, but because votes are published on the blockchain, the operator cannot cheat by censoring votes, and because the operator must provide a ZK-SNARK, they cannot cheat by mis-calculating the result.

## Combining ZK-SNARKs with MPC

A more advanced use of ZK-SNARKs involves making proofs over computations where the inputs are split between two or more parties, and we don't want each party to learn the other parties' inputs. You can satisfy the privacy requirement with [garbled circuits](https://vitalik.eth.limo/general/2020/03/21/garbled.html) in the 2-party case, and more complicated multi-party computation protocols in the N-party case. ZK-SNARKs can be combined with these protocols to do verifiable multi-party computation.

This could enable more advanced reputation systems where multiple participants can perform joint computations over their private inputs, it could enable privacy-preserving but authenticated data markets, and many other applications. That said, note that the math for doing this efficiently is still relatively in its infancy.

> Read the full article by [Vitalik Buterin](https://vitalik.eth.limo/general/2021/01/26/snarks.html)

# Some ways to use ZK-SNARKs for privacy

ZK-SNARKs are a powerful cryptographic tool, and an increasingly important part of the applications that people are building both in the blockchain space and beyond. But they are complicated, both in terms of _how they work_, and in terms of _how you can use them_.

## What does a ZK-SNARK do?

Suppose that you have a public input x, a private input w, and a (public) function f(x,w)→{True,False} that performs some kind of verification on the inputs. With a ZK-SNARK, you can prove that you know an w such that f(x,w)=True for some given f and x, without revealing what w is. Additionally, the verifier can verify the proof much faster than it would take for them to compute f(x,w) themselves, even if they know w.

![](https://vitalik.eth.limo/images/using_snarks/definition.png)

This gives the ZK-SNARK its two properties: **privacy** and **scalability**. As mentioned above, in this post our examples will focus on privacy.

## Holding centralized parties accountable

Sometimes, you need to build a scheme that has a central "operator" of some kind. This could be for many reasons: sometimes it's for scalability, and sometimes it's for privacy - specifically, the privacy of data held by the operator.

The MACI coercion-resistant voting system, for example, requires voters to submit their votes on-chain encrypted to a secret key held by a central operator. The operator would decrypt all the votes on-chain, count them up, and reveal the final result, along with a ZK-SNARK proving that they did everything correctly. This extra complexity is necessary to ensure a strong privacy property (called **coercion-resistance**): that users cannot prove to others how they voted even if they wanted to.

Thanks to blockchains and ZK-SNARKs, the amount of trust in the operator can be kept very low. A malicious operator could still break coercion resistance, but because votes are published on the blockchain, the operator cannot cheat by censoring votes, and because the operator must provide a ZK-SNARK, they cannot cheat by mis-calculating the result.

## Combining ZK-SNARKs with MPC

A more advanced use of ZK-SNARKs involves making proofs over computations where the inputs are split between two or more parties, and we don't want each party to learn the other parties' inputs. You can satisfy the privacy requirement with [garbled circuits](https://vitalik.eth.limo/general/2020/03/21/garbled.html) in the 2-party case, and more complicated multi-party computation protocols in the N-party case. ZK-SNARKs can be combined with these protocols to do verifiable multi-party computation.

This could enable more advanced reputation systems where multiple participants can perform joint computations over their private inputs, it could enable privacy-preserving but authenticated data markets, and many other applications. That said, note that the math for doing this efficiently is still relatively in its infancy.

> Read the full article by [Vitalik Buterin](https://vitalik.eth.limo/general/2021/01/26/snarks.html)

# Some ways to use ZK-SNARKs for privacy

ZK-SNARKs are a powerful cryptographic tool, and an increasingly important part of the applications that people are building both in the blockchain space and beyond. But they are complicated, both in terms of _how they work_, and in terms of _how you can use them_.

## What does a ZK-SNARK do?

Suppose that you have a public input x, a private input w, and a (public) function f(x,w)→{True,False} that performs some kind of verification on the inputs. With a ZK-SNARK, you can prove that you know an w such that f(x,w)=True for some given f and x, without revealing what w is. Additionally, the verifier can verify the proof much faster than it would take for them to compute f(x,w) themselves, even if they know w.

![](https://vitalik.eth.limo/images/using_snarks/definition.png)

This gives the ZK-SNARK its two properties: **privacy** and **scalability**. As mentioned above, in this post our examples will focus on privacy.

## Holding centralized parties accountable

Sometimes, you need to build a scheme that has a central "operator" of some kind. This could be for many reasons: sometimes it's for scalability, and sometimes it's for privacy - specifically, the privacy of data held by the operator.

The MACI coercion-resistant voting system, for example, requires voters to submit their votes on-chain encrypted to a secret key held by a central operator. The operator would decrypt all the votes on-chain, count them up, and reveal the final result, along with a ZK-SNARK proving that they did everything correctly. This extra complexity is necessary to ensure a strong privacy property (called **coercion-resistance**): that users cannot prove to others how they voted even if they wanted to.

Thanks to blockchains and ZK-SNARKs, the amount of trust in the operator can be kept very low. A malicious operator could still break coercion resistance, but because votes are published on the blockchain, the operator cannot cheat by censoring votes, and because the operator must provide a ZK-SNARK, they cannot cheat by mis-calculating the result.

## Combining ZK-SNARKs with MPC

A more advanced use of ZK-SNARKs involves making proofs over computations where the inputs are split between two or more parties, and we don't want each party to learn the other parties' inputs. You can satisfy the privacy requirement with [garbled circuits](https://vitalik.eth.limo/general/2020/03/21/garbled.html) in the 2-party case, and more complicated multi-party computation protocols in the N-party case. ZK-SNARKs can be combined with these protocols to do verifiable multi-party computation.

This could enable more advanced reputation systems where multiple participants can perform joint computations over their private inputs, it could enable privacy-preserving but authenticated data markets, and many other applications. That said, note that the math for doing this efficiently is still relatively in its infancy.

> Read the full article by [Vitalik Buterin](https://vitalik.eth.limo/general/2021/01/26/snarks.html)

# Some ways to use ZK-SNARKs for privacy

ZK-SNARKs are a powerful cryptographic tool, and an increasingly important part of the applications that people are building both in the blockchain space and beyond. But they are complicated, both in terms of _how they work_, and in terms of _how you can use them_.

## What does a ZK-SNARK do?

Suppose that you have a public input x, a private input w, and a (public) function f(x,w)→{True,False} that performs some kind of verification on the inputs. With a ZK-SNARK, you can prove that you know an w such that f(x,w)=True for some given f and x, without revealing what w is. Additionally, the verifier can verify the proof much faster than it would take for them to compute f(x,w) themselves, even if they know w.

![](https://vitalik.eth.limo/images/using_snarks/definition.png)

This gives the ZK-SNARK its two properties: **privacy** and **scalability**. As mentioned above, in this post our examples will focus on privacy.

## Holding centralized parties accountable

Sometimes, you need to build a scheme that has a central "operator" of some kind. This could be for many reasons: sometimes it's for scalability, and sometimes it's for privacy - specifically, the privacy of data held by the operator.

The MACI coercion-resistant voting system, for example, requires voters to submit their votes on-chain encrypted to a secret key held by a central operator. The operator would decrypt all the votes on-chain, count them up, and reveal the final result, along with a ZK-SNARK proving that they did everything correctly. This extra complexity is necessary to ensure a strong privacy property (called **coercion-resistance**): that users cannot prove to others how they voted even if they wanted to.

Thanks to blockchains and ZK-SNARKs, the amount of trust in the operator can be kept very low. A malicious operator could still break coercion resistance, but because votes are published on the blockchain, the operator cannot cheat by censoring votes, and because the operator must provide a ZK-SNARK, they cannot cheat by mis-calculating the result.

## Combining ZK-SNARKs with MPC

A more advanced use of ZK-SNARKs involves making proofs over computations where the inputs are split between two or more parties, and we don't want each party to learn the other parties' inputs. You can satisfy the privacy requirement with [garbled circuits](https://vitalik.eth.limo/general/2020/03/21/garbled.html) in the 2-party case, and more complicated multi-party computation protocols in the N-party case. ZK-SNARKs can be combined with these protocols to do verifiable multi-party computation.

This could enable more advanced reputation systems where multiple participants can perform joint computations over their private inputs, it could enable privacy-preserving but authenticated data markets, and many other applications. That said, note that the math for doing this efficiently is still relatively in its infancy.

> Read the full article by [Vitalik Buterin](https://vitalik.eth.limo/general/2021/01/26/snarks.html)

# Some ways to use ZK-SNARKs for privacy

ZK-SNARKs are a powerful cryptographic tool, and an increasingly important part of the applications that people are building both in the blockchain space and beyond. But they are complicated, both in terms of _how they work_, and in terms of _how you can use them_.

## What does a ZK-SNARK do?

Suppose that you have a public input x, a private input w, and a (public) function f(x,w)→{True,False} that performs some kind of verification on the inputs. With a ZK-SNARK, you can prove that you know an w such that f(x,w)=True for some given f and x, without revealing what w is. Additionally, the verifier can verify the proof much faster than it would take for them to compute f(x,w) themselves, even if they know w.

![](https://vitalik.eth.limo/images/using_snarks/definition.png)

This gives the ZK-SNARK its two properties: **privacy** and **scalability**. As mentioned above, in this post our examples will focus on privacy.

## Holding centralized parties accountable

Sometimes, you need to build a scheme that has a central "operator" of some kind. This could be for many reasons: sometimes it's for scalability, and sometimes it's for privacy - specifically, the privacy of data held by the operator.

The MACI coercion-resistant voting system, for example, requires voters to submit their votes on-chain encrypted to a secret key held by a central operator. The operator would decrypt all the votes on-chain, count them up, and reveal the final result, along with a ZK-SNARK proving that they did everything correctly. This extra complexity is necessary to ensure a strong privacy property (called **coercion-resistance**): that users cannot prove to others how they voted even if they wanted to.

Thanks to blockchains and ZK-SNARKs, the amount of trust in the operator can be kept very low. A malicious operator could still break coercion resistance, but because votes are published on the blockchain, the operator cannot cheat by censoring votes, and because the operator must provide a ZK-SNARK, they cannot cheat by mis-calculating the result.

## Combining ZK-SNARKs with MPC

A more advanced use of ZK-SNARKs involves making proofs over computations where the inputs are split between two or more parties, and we don't want each party to learn the other parties' inputs. You can satisfy the privacy requirement with [garbled circuits](https://vitalik.eth.limo/general/2020/03/21/garbled.html) in the 2-party case, and more complicated multi-party computation protocols in the N-party case. ZK-SNARKs can be combined with these protocols to do verifiable multi-party computation.

This could enable more advanced reputation systems where multiple participants can perform joint computations over their private inputs, it could enable privacy-preserving but authenticated data markets, and many other applications. That said, note that the math for doing this efficiently is still relatively in its infancy.

> Read the full article by [Vitalik Buterin](https://vitalik.eth.limo/general/2021/01/26/snarks.html)

asdasdasdasdkqwnelqkwnelqwne