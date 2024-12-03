<div align="center">
<img src="logo.svg" align="center" width="128px"/>
<br /><br />
</div>

---
# Introduction

The Iden3comm protocol defines the rules for communication between agents, wallets. It is built on the DIDComm messaging protocol.

The Iden3comm protocol specification introduces protocols such as credential, revocation, auth, etc. Currently, Iden3comm does not support any existing DIDComm protocols, such as Discovery Features or Trust Ping. Therefore, there is no need to implement those specific DIDComm protocols. However, if the standard protocols/methods provided are insufficient, it is possible to extend the specification with custom protocols and methods to meet your requirements.

Since the Iden3comm protocol is built on the DIDComm protocol, we must adhere to all the rules of the DIDComm protocol.

The specification itself is not tied to any specific technology. Similar to the DIDComm Messaging Specification, it does not impose any limitations on the transport layers used, allowing for various technologies to be employed in implementing it.

More about the architecture of message handling: [Asynchronous](https://identity.foundation/didcomm-messaging/spec/#ramifications) and synchronous:

> On top of this foundation, it is possible to build elegant, synchronous request-response interactions. All of us have interacted with a friend who’s emailing or texting us in near-realtime. However, interoperability begins with a least-common-denominator assumption that’s simpler.
> 

DIDcomm requires strict versioning. Iden3comm supports this specification: [https://semver.org/](https://semver.org/)

| Name            | Version | Description                                                                                                            |  |
|-----------------| --- |------------------------------------------------------------------------------------------------------------------------| --- |
| Credentials     | 1.0 | This protocol is aimed at performing actions with a credential. Fetching a credential, issuing a credential, and more. |  |
| Auth            | 1.0 | This protocol is used to exchange authorization requests and responses between communicators                           |  |
| Contract invoke | 1.0 | Contains all information for calling a smart contract                                                                  |  |
| Proof           | 1.0 | This protocol aimed to exchange proof between communicators                                                            |  |
| Revocation      | 1.0 | Revocation protocol for getting existing non-existent revocation proof                                                 |  |

All of these protocols share the same high-level message structure but have different message bodies that depend on the specific protocol being used. The details of this high-level message structure are outlined in the [DIDComm specification](https://identity.foundation/didcomm-messaging/spec/#message-headers).

Example of common message:

```json
{
	"id": "0297b976-bb81-458b-982b-67edea81d439",
	"typ": "application/iden3comm-zkp-json",
	"type": "https://iden3-communication.io/authorization/1.0/request",
	"thid": "b05334c8-7a4e-4dfa-bbe8-7b0259efad63",
	"body": <depend_on_protocol>,
	"from": "did:polygonid:polygon:mumbai:2qJ689kpoJxcSzB5sAFJtPsSBSrHF5dq722BHMqURL",
	"to": "did:polygonid:polygon:mumbai:2qK2Rwf2zqzzhqVLqTWXetGUbs1Sc79woomP5cDLBE"
}
```
The field `typ` can be one of the following three types:
    1. `application/iden3comm-signed-json` for a signed message;
    2. `application/iden3comm-plain-json` for plain message;
    3. `application/iden3comm-encrypted-json` for encrypted message.
    4. `application/iden3-zkp-json` for JSON Web Zeroknowledge message;

---

###### <div align="center">
<a href="https://github.com/iden3/iden3comm" target="_blank">Iden3comm on GitHub</a></div>









