# did:iden3 Implementations

This page lists known implementations and services related to the **did:iden3** method.
It focuses on **core libraries**, **protocol implementations**, and **services** that enable
DID creation, resolution, authentication, and verifiable credential workflows.

If you maintain a did:iden3-related implementation that is not listed here, or want to update
an existing entry, please submit a [pull request](https://github.com/iden3/iden3.github.io).

---

## iden3 Communication Protocol

Implementations of the **iden3 communication protocol**, which defines message formats
and flows used for authorization requests, responses, and credential-based interactions.

### Resolver Implementations

- **[driver-did-iden3](https://github.com/iden3/driver-did-iden3)**
  Universal Resolver driver enabling resolution of `did:iden3` identifiers via
  standard resolver infrastructure. 
  See an example resolution here: [DID resolution](https://resolver.privado.id/1.0/identifiers/did:iden3:polygon:main:wpaFHwfPYjVnimeX1gSxvxonmQ1NG66AcAPPbDWn8).

---

### Core Libraries (Multi-language)

Core libraries provide the fundamental building blocks for working with did:iden3 identities,
claims, authentication messages, and zero-knowledge proofs.
Implementations are available across **TypeScript / JavaScript**, **Go**, and **Flutter**.

#### TypeScript / JavaScript

- **[js-iden3-core](https://github.com/iden3/js-iden3-core)**  
  Low-level API to create and manipulate iden3 claims and related cryptographic primitives.

- **[js-sdk](https://github.com/0xPolygonID/js-sdk)**  
  High-level JavaScript SDK implementing iden3 communication flows, DID interactions,
  and verifiable credential usage.  
  Can be used as a foundation for issuer, holder, and verifier applications.

---

#### Go

- **[go-iden3-core](https://github.com/iden3/go-iden3-core)**  
  Go implementation of the iden3 core library, providing primitives for claims, proofs,
  and DID-related data structures.

- **[iden3comm](https://github.com/iden3/iden3comm)**  
  Go implementation of the iden3 communication protocol used for message exchange,
  authorization requests, and responses.

---

#### Flutter / Dart

- **[polygonid-flutter-sdk](https://github.com/0xPolygonID/polygonid-flutter-sdk)**  
  Flutter SDK enabling iden3comm-based authentication and credential presentation
  in mobile applications.

---

### Authentication & Authorization Libraries

Libraries focused specifically on handling authentication messages in the communication protocol.

#### TypeScript / JavaScript

- **[js-iden3-auth](https://github.com/iden3/js-iden3-auth)**  
  TypeScript libraries for handling iden3 authentication messages
  and protocol-level authorization flows.

- **[js-jwz](https://github.com/iden3/js-jwz)**  
  JavaScript implementation of **JSON Web Zero-Knowledge (JWZ)**,
  used to encapsulate zero-knowledge proofs and signed messages.

---

#### Go

- **[go-iden3-auth](https://github.com/iden3/go-iden3-auth)**  
  Go implementation of iden3 authentication message handling
  and authorization protocol logic.

- **[go-jwz](https://github.com/iden3/go-jwz)**  
  Go implementation of the JSON Web Zero-Knowledge (JWZ) standard.

---

### Circuits & Proof Systems

Zero-knowledge circuits, proving systems, and supporting libraries used by `did:iden3`
implementations for credential verification and privacy-preserving proofs.

- **[circuits](https://github.com/iden3/circuits)**  
  Canonical repository of iden3 zero-knowledge circuits used for authentication,
  credential queries, and authorization flows.

- **[go-circuits](https://github.com/iden3/go-circuits)**  
  Go bindings and tooling for working with iden3 circuits.

- **[circomlib](https://github.com/iden3/circomlib)**  
  Core Circom circuit library used by iden3 and other zero-knowledge systems.

- **[rapidsnark](https://github.com/iden3/rapidsnark)**  
  High-performance zkSNARK prover optimized for iden3 and Circom-based circuits.

---

### Smart Contracts

Smart contracts used by the `did:iden3` ecosystem for on-chain identity state management,
verification, and integration with blockchain networks.

- **[contracts](https://github.com/0xPolygonID/contracts)**  
  Smart contracts supporting identity state transitions, proof verification,
  and on-chain components of the iden3 protocol.

---

## Example Implementations of the iden3comm Protocol

These projects demonstrate practical usage of the iden3 communication protocol in
applications, SDKs, and backend services.

- **[js-sdk](https://github.com/0xPolygonID/js-sdk)**  
  High-level JavaScript SDK implementing iden3 communication flows, DID interactions,
  and verifiable credential usage.

- **[polygonid-flutter-sdk](https://github.com/0xPolygonID/polygonid-flutter-sdk)**  
  Flutter SDK demonstrating iden3comm-based authentication and credential presentation
  in mobile applications.

- **[issuer-node](https://github.com/0xPolygonID/issuer-node)**  
  Backend service implementing iden3 communication flows for issuing verifiable credentials
  within the Privado ID ecosystem.

---

## Issuer Software

Software components designed for **issuers** to create, manage,
and issue verifiable credentials using `did:iden3`.

- **[issuer-node](https://github.com/0xPolygonID/issuer-node)**  
  Backend service for issuers implementing iden3 communication flows
  and credential issuance logic.

- **[js-sdk](https://github.com/0xPolygonID/js-sdk)**  
  Can also be used as a building block for custom issuer applications
  implemented in JavaScript / TypeScript.

---

## Notes

- All listed repositories are **public** and actively maintained.
- This page is organized to reflect the **protocol stack** of `did:iden3`,
  from low-level primitives to concrete protocol implementations.
