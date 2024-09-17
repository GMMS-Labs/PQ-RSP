# PQ-RSP
Post Quantum Remote SIM Provisioning

---
### [TTDF Call for Proposals: Quantum Encryption Algorithm (QEA)](https://ttdf.usof.gov.in/users/quantumencryption)
>
>The call for proposals is for developing an India specific Quantum Encryption Algorithm (QEA) that will represent a cutting-edge approach to securing digital communication channels by leveraging the principles of quantum mechanics.
>The algorithm should ensure:
>- Unparalleled Security,
>- Advanced Encryption Capabilities
>- Ultrafast and Efficient Encryption etc.

###### [!NOTICE] This research work focuses on Post Quantum Cryptography in Consumer focused Remote SIM Provisioning, one of the [PQC telco use cases](https://www.gsma.com/newsroom/wp-content/uploads/PQ.03-Post-Quantum-Cryptography-Guidelines-for-Telecom-Use-v1.0.pdf), Internal to MNO use case: RSP (Remote Sim Provisioning / eSIM) for Consumer Electronics (SGP.22).

## Scope
We consider the impact of quantum computing on the **profile download** and **profile (State) management** (e.g. Enable, Disable, …) procedures for the three existing specifications (M2M, Consumer and IoT) and discuss the potential migration strategies for each of them.

## Sensitive Data Discovery
A profile contains very sensitive data such as the long-term secret key K, the operator secret key OPc and the IMSI/SUPI. With such data, an adversary could authenticate to the operator
on behalf of the legitimate user, impersonate the operator towards the user using this profile and even decrypt all their communications.

## Cryptographic Inventory
Cryptographic protocols present some differences between M2M, Consumer and IoT.

### Consumer Device 
A secure channel between the SM-DP+ and the eUICC to protect the Profile. The LPA (running on the Device or the eUICC) is responsible about the transport layer which is using HTTPS with server authentication only. In the context of SGP.22, RSP follows a different approach involving three entities, the SMDP+, the Device and the eUICC.

#### SM-DP+/Device Channel
The channel between SM-DP+ and the Device is secured using TLS with ECDHE key exchange and ECDSA or RSA signatures. The list of supported cipher suites can be found in Section 2.6.6 of SGP.22.

#### SM-DP+/eUICC
The protection of the profile package is done using keys derived from a shared secret computed using Diffie-Hellman key exchange. Several initial steps are however required to establish such a shared secret involving many cryptographic computations.
- First, the SM-DP+ and the eUICC initiates a so-called “common mutual authentication procedure” (described in Section 3.0.1 of SGP.22) where,
- Each of these entities generates a signature and authenticates the other party by verifying its signature and the corresponding certificates. Once this stage is over,
- The SM-DP+ produces a signature on the transaction data which is sent to the eUICC. If the signature is valid,
- The eUICC generates its Diffie-Hellman key share which is signed by the eUICC along with some transaction data.
- The resulting elements are then sent to the SM-DP+. If the signature is valid,
- The SM-DP+ generates its own Diffie-Hellman key share and can thus derive a shared secret used to generate the Bound Profile Package (BPP).
- This key share can thus be sent to the eUICC along with the BPP and a signature authenticating this material.

## Migration Strategy Analysis and Impact Assessment
The very different nature of the M2M secure channels and the Consumer/IoT Device ones may lead to different strategies, depending on the security model considered.

### Consumer Device and eSIM IoT (SGP.22 and SGP.32)
In the case of SGP.22 and SGP.32, Profile Download is done through two channels but that essentially rely on the same cryptographic tools. An adversary able to break the security of one of them using a quantum computer would then have no difficulty in breaking the security of the other one. Any migration strategy should then consider updating these two channels at the same time.

## Zero Trust Architecture in the Context of Post Quantum Cryptography
>
>ZTA is orthogonal to all cryptography algorithms and their corresponding use cases.
>ZTA encompasses cryptography as well as other aspects of security.
>ZTA is amethodology of recursive application of steps an organization takes to conform with.
>Part ofthose steps is the creation of Zero Trust security policies which could include application of cryptographic algorithms to data.
>The Zero Trust security policies are defined using the Kipling method:
>- Why?
>- When?
>- How?
>- Where?
>- Who?
>- What?

ZTA relies upon multiple security mechanisms, including cryptographic algorithms, in order to provide authentication, confidentiality and integrity protection.
ZTA includes mechanisms that are vulnerable to quantum computing (i.e., classical cryptographic algorithms); the quantum threat applies to ZTA as well.
Hence, ZTA in the Post Quantum realm must encompass the deployment of Post Quantum Cryptographic algorithms.

---

Work in progress . . .
