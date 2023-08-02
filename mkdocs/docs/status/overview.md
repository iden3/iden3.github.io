# Credential status

**Credential Status** (CS) is an essential component of **Verifiable Credentials** (VC). Its primary purpose is to provide information about the revocation status of a credential. Anyone can utilize CS to determine whether a VC has been revoked or remains valid. Within the iden3 Verifiable Credentials system, there are four types of CS available:

1. **SparseMerkleTreeProof**
2. **Iden3ReverseSparseMerkleTreeProof**
3. **Iden3commRevocationStatusV1.0**
4. **Iden3OnchainSparseMerkleTreeProof2023**

All these types have the same message format:

```json
{
	"id": "...",
    "type": "...",
	"revocationNonce": 0
}
```

`id` - a unique ID for the CS. The content of this field depends on the `type`.

`type` - the type of the credential status.

`revocationNonce` -a unique number for the Verifiable credential.

## SparseMerkleTreeProof

Example of CS:

```json
"credentialStatus": {
	"id": "https://issuer.com/api/v1/identities/did%3Apolygonid%3Apolygon%3Amumbai%3A2qEjShhoHGFdi88ZPCXcApSesmGzk8aqqf3hymnyiW/claims/revocation/status/1016367164",
	"revocationNonce": 1016367164,
	"type": "SparseMerkleTreeProof"
}, 
```

If the `type == SparseMerkleTreeProof`, the `id` field will contain a URL to the issuer node. Users can utilize this URL to process the revocation status.

### Workflow:

1. Making an HTTP call to the URL from the `id` field:
    
    Example of response:
    
    ```json
    {
        "issuer": {
            "state": "52e66f413231e4d7c43cc09aaf076b8bc0f3a4f18f95e29dc92ab001e401e708",
            "claimsTreeRoot": "c5a516e17a16160fdf567c130d73909fefbd5fcec1ad74b9707fbac989d4e812"
        },
        "mtp": {
            "existence": false,
            "siblings": []
        }
    }
    ```
    
    More about this response: [https://raw.githubusercontent.com/iden3/claim-schema-vocab/main/core/vocab/SparseMerkleTreeProof.md](https://raw.githubusercontent.com/iden3/claim-schema-vocab/main/core/vocab/SparseMerkleTreeProof.md)
    
    In this case, when `mtp.existence == false`, it means that the user's revocationNonce doesn't exist in the revocation tree. This is a positive outcome for the user because it allows them to build a non-revocation proof.
    
2. Building non-revocation/revocation proof using the response.

## **Iden3ReverseSparseMerkleTreeProof**

In this scenario, the issuer utilizes the [RHS server](https://github.com/iden3/reverse-hash-service/) to store the tree info in a distributed manner. This approach ensures data resilience and accessibility in a distributed fashion.

Algorithm for rhs is described [here](https://docs.iden3.io/services/rhs/#publishing-identity-state-to-rhs).

Moreover, the **credentialStatus** contains `statusIssuer` as a backup mechanism in case the [RHS server](https://github.com/iden3/reverse-hash-service/) becomes unavailable. By having the `statusIssuer`, the issuer retains the ability to verify and manage the CS even if the  storage through the [RHS server](https://github.com/iden3/reverse-hash-service/) encounters any issues.

This dual approach of utilizing a decentralized system while also having a backup option in the form of `statusIssuer` enhances the reliability and availability of the revocation and verification process for the users' credentials.

Example of CS:

```json
"credentialStatus": {
	"id": "https://rhs-staging.polygonid.me",
	"revocationNonce": 1016367164,
	"statusIssuer": {
	    "id": "https://1e1a-46-133-26-136.ngrok-free.app/api/v1/identities/did%3Apolygonid%3Apolygon%3Amumbai%3A2qEeAALESZRcocQTh7ri1skPKkMiHftaH1ufEVJWku/claims/revocation/status/0",
	    "revocationNonce": 1016367164,
	    "type": "SparseMerkleTreeProof"
	},
	"type": "Iden3ReverseSparseMerkleTreeProof"
}
```

### Workflow

To verify the revocation status of a credential, follow these steps:

1. Utilize the [RHS server](https://github.com/iden3/reverse-hash-service/) using the information provided in the `credentialStatus.id` field. This will enable the building of a non-revocation/revocation proof.
2. In the event that the [RHS server](https://github.com/iden3/reverse-hash-service/) is unavailable or encounters issues, users can fall back to using the `credentialStatus.statusIssuer` object to process the revocation status. This object is designed with `type == SparseMerkleTreeProof`, allowing users to treat it as a `SparseMerkleTreeProof` type. Consequently, users can continue the revocation verification process as intended, ensuring the continuity of the verification even in the absence of the [RHS server](https://github.com/iden3/reverse-hash-service/).

By following this workflow, users can confidently verify the revocation status of their credentials, utilizing either the [RHS server](https://github.com/iden3/reverse-hash-service/) or the `credentialStatus.statusIssuer` object as necessary to obtain the proof required for verification. This flexible approach ensures the reliability and robustness of the revocation process for user credentials.

## **Iden3commRevocationStatusV1.0**

Example of CS:

```json
"credentialStatus": {
	"id": "https://issuer.com/api/v1/agent",
  "revocationNonce": 2234893355,
  "type": "Iden3commRevocationStatusV1.0"
},
```

In this case, the `id` is set to the issuer's agent endpoint. To establish communication with the issuer's agent, users should utilize the [iden3comm protocol](http://iden3-communication.io/credentials/overview/).

## Workflow

To verify the revocation status of a credential, follow these steps using the appropriate communication protocols:

1. Construct the [revocation status request idne3comm message](http://iden3-communication.io/revocation/1.0/request-status/). This message will be used to request information about the revocation status.
2. Send the constructed revocation status request message in plain text format to the issuer's agent endpoint, which is specified in the `id` field. The communication will take place using the iden3comm protocol.
3. The issuer will respond with a [status iden3comm protocol message](http://iden3-communication.io/revocation/1.0/status/) that contains the necessary information.
4. Upon receiving the response, extract the `body` field from it. The `body` field will contain essential details related to the issuer and the revocation status:
    
    ```json
    {
        "issuer": {
            "state": "52e66f413231e4d7c43cc09aaf076b8bc0f3a4f18f95e29dc92ab001e401e708",
            "claimsTreeRoot": "c5a516e17a16160fdf567c130d73909fefbd5fcec1ad74b9707fbac989d4e812"
        },
        "mtp": {
            "existence": false,
            "siblings": []
        }
    }
    ```
    
5. Utilize the information obtained from the `body` field of the issuer's response to construct the non-revocation/revocation proof as required.

It's important to note that the difference between revocation statuses `SparseMerkleTreeProof` and `Iden3commRevocationStatusV1.0` lies in the format of the response/request. While `SparseMerkleTreeProof` uses the HTTP protocol for communication, `Iden3commRevocationStatusV1.0` employs the [iden3comm protocol](http://iden3-communication.io/) for communication.

## **Iden3OnchainSparseMerkleTreeProof2023**

The `Iden3OnchainSparseMerkleTreeProof2023` type is used for onchain issuers as well as for issuer who store their tree information onchain, providing a mechanism to verify the revocation status of credentials in the decentralized way.

Here are two examples of the credential status (CS) objects using this type:

**Example 1:**

```json
{
    "id": "did:polygonid:polygon:mumbai:2qCU58EJgrELbXjWbWGC9kPPnczQdp93nUR6LC45F6/credentialStatus?revocationNonce=1051565438&contractAddress=80001:0x2fCE183c7Fbc4EbB5DB3B0F5a63e0e02AE9a85d2",
    "type": "Iden3OnchainSparseMerkleTreeProof2023",
    "revocationNonce": 1051565438
}
```

**Example 2:**

```json
{
    "id": "did:polygonid:polygon:main:2qCU58EJgrEMWhziKqC3qNXJkZPY8XCxDSBM4mqPkM/credentialStatus",
    "type": "Iden3OnchainSparseMerkleTreeProof2023",
    "revocationNonce": 1051565438
}
```

In both examples, the `id` field is a valid Decentralized Identifier (DID) with optional parameters: `revocationNonce` and `contractAddress`.

The format of the `id` field follows this structure:

```
[did]:[methodid]:[chain]:[network]:[id]/credentialStatus?(revocationNonce=value)&&(contractAddress=[chainID]:[contractAddress])
```

## Workflow

To verify the revocation status of an onchain credential using the `Iden3OnchainSparseMerkleTreeProof2023` type, follow these steps:

1. Use core libraries such as the [js-iden3-core](https://github.com/iden3/js-iden3-core/blob/baa0ead8a3e2340bb4d78132ec63e6e24d806da9/src/did/did.ts#L160) (JavaScript) or [go-iden3-core](https://github.com/iden3/go-iden3-core/blob/014f51e92da5c0c89c95c31e42bfca1652d2ad14/w3c/did_w3c.go#L165) (Go) to parse the `id` field as a valid DID.
2. Extract the `core.ID` from the parsed DID using the appropriate method in the core library, such as [js-iden3-core](https://github.com/iden3/js-iden3-core/blob/baa0ead8a3e2340bb4d78132ec63e6e24d806da9/src/did/did.ts#L160) (JavaScript) or [go-iden3-core](https://github.com/iden3/go-iden3-core/blob/014f51e92da5c0c89c95c31e42bfca1652d2ad14/did.go#L184) (Go).
3. Extract the `revocationNonce` from the DID parameters. If the `revocationNonce` does not exist in the DID parameters, use the `revocationNonce` from the `credentialStatus` object.
4. Extract the `chainID` and `contractAddress` from the DID parameters. If the `contractAddress` does not exist in the DID parameters, extract the `chainID` and `contractAddress` from the DID itself.
5. Utilize the provided ABI to call the `getRevocationStatus` function of the smart contract. Pass the extracted `core.ID` and `revocationNonce` as parameters to this function. The function will return a response containing the revocation status information.
    - ABI
        
        ```json
        [
            {
              "inputs": [
                {
                  "internalType": "uint256",
                  "name": "id",
                  "type": "uint256"
                },
                {
                  "internalType": "uint64",
                  "name": "nonce",
                  "type": "uint64"
                }
              ],
              "name": "getRevocationStatus",
              "outputs": [
                {
                  "components": [
                    {
                      "components": [
                        {
                          "internalType": "uint256",
                          "name": "state",
                          "type": "uint256"
                        },
                        {
                          "internalType": "uint256",
                          "name": "claimsTreeRoot",
                          "type": "uint256"
                        },
                        {
                          "internalType": "uint256",
                          "name": "revocationTreeRoot",
                          "type": "uint256"
                        },
                        {
                          "internalType": "uint256",
                          "name": "rootOfRoots",
                          "type": "uint256"
                        }
                      ],
                      "internalType": "struct IOnchainCredentialStatusResolver.IdentityStateRoots",
                      "name": "issuer",
                      "type": "tuple"
                    },
                    {
                      "components": [
                        {
                          "internalType": "uint256",
                          "name": "root",
                          "type": "uint256"
                        },
                        {
                          "internalType": "bool",
                          "name": "existence",
                          "type": "bool"
                        },
                        {
                          "internalType": "uint256[]",
                          "name": "siblings",
                          "type": "uint256[]"
                        },
                        {
                          "internalType": "uint256",
                          "name": "index",
                          "type": "uint256"
                        },
                        {
                          "internalType": "uint256",
                          "name": "value",
                          "type": "uint256"
                        },
                        {
                          "internalType": "bool",
                          "name": "auxExistence",
                          "type": "bool"
                        },
                        {
                          "internalType": "uint256",
                          "name": "auxIndex",
                          "type": "uint256"
                        },
                        {
                          "internalType": "uint256",
                          "name": "auxValue",
                          "type": "uint256"
                        }
                      ],
                      "internalType": "struct IOnchainCredentialStatusResolver.Proof",
                      "name": "mtp",
                      "type": "tuple"
                    }
                  ],
                  "internalType": "struct IOnchainCredentialStatusResolver.CredentialStatus",
                  "name": "",
                  "type": "tuple"
                }
              ],
              "stateMutability": "view",
              "type": "function"
            }
          ]
        ```
        

Example of supporting **Iden3OnchainSparseMerkleTreeProof2023** status: [https://github.com/0xPolygonID/js-sdk/blob/b1ac92b6b18023fda6d4fb15f28a4f0e5166e2e3/src/credentials/status/on-chain-revocation.ts#L73](https://github.com/0xPolygonID/js-sdk/blob/b1ac92b6b18023fda6d4fb15f28a4f0e5166e2e3/src/credentials/status/on-chain-revocation.ts#L73)