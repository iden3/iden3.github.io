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

Moreover, the **credentialStatus** contains `statusIssuer` as a backup mechanism in case the [RHS server](https://github.com/iden3/reverse-hash-service/) becomes unavailable. By having the `statusIssuer`, the issuer retains the ability to verify and manage the CS even if the storage through the [RHS server](https://github.com/iden3/reverse-hash-service/) encounters any issues.

This dual approach of utilizing a decentralized system while also having a backup option in the form of `statusIssuer` enhances the reliability and availability of the revocation and verification process for the users' credentials.

For now, only `SparseMerkleTreeProof` credential status is supported as a backup optio

********************Example :********************

```json
"credentialStatus": {
	"id": "https://rhs-staging.polygonid.me?state=a1abdb9f44c7b649eb4d21b59ef34bd38e054aa3e500987575a14fc92c49f42c",
	"revocationNonce": 1016367164,
	"statusIssuer": {
	    "id": "https://1e1a-46-133-26-136.ngrok-free.app/api/v1/identities/did%3Apolygonid%3Apolygon%3Amumbai%3A2qEeAALESZRcocQTh7ri1skPKkMiHftaH1ufEVJWku/claims/revocation/status/0",
	    "revocationNonce": 1016367164,
	    "type": "SparseMerkleTreeProof"
	},
	"type": "Iden3ReverseSparseMerkleTreeProof"
}
```

********************Workflow:********************

1. Attempt to retrieve the latest issuer state using the state contract. Utilize the `GetLatestStateById` method from the state contract.
2. In the event that the state contract returns the error `IDENTITY_DOES_NOT_EXIST`, follow these steps:
    1. If the `state` parameter exists and it is a `genesis` state, use this state to generate a non-revocation proof via the [RHS service](https://github.com/iden3/reverse-hash-service/). Provide the extracted state as the latest state and the revocation nonce to the [RHS service](https://github.com/iden3/reverse-hash-service/).
    2. If the `state` parameter does not exist - throw an error.
        1. As a legacy option, for statuses where state doesn’t persist in the current implementation, we use additional custom issuer data from BJJSignatureProof or Iden3SparseMerkleTreeProof  to extract tree roots and the issuer’s state to construct a non-revocation proof. If this param is not provided - an error is thrown. This is not mandatory in new implementations. 
        
3. If the state contract returns the latest state, utilize the [RHS service](https://github.com/iden3/reverse-hash-service/) with the latest state and nonce to generate non-revocation/revocation proof according to the [algorithm](https://docs.iden3.io/services/rhs/).
4. In the event that the [RHS server](https://github.com/iden3/reverse-hash-service/) is unavailable or encounters issues, users can fall back to using the `credentialStatus.statusIssuer` object to process the revocation status. This object must have`SparseMerkleTreeProof` type, so it will be processed accordingly. 

Example of implementation: [JS](https://github.com/0xPolygonID/js-sdk/blob/5ffd319f0e01a95963364a4622d98c970ef0ec59/src/credentials/status/reverse-sparse-merkle-tree.ts),  [GO](https://github.com/0xPolygonID/c-polygonid/blob/16c1705655ddbb1ef9f2247d33bc5f8952983fd7/inputs_sig.go#L1826)

## **Iden3commRevocationStatusV1.0**

Example of Сredential status:

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

1. Construct the [revocation status request iden3comm message](http://iden3-communication.io/revocation/1.0/request-status/). This message will be used to request information about the revocation status.
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

It's important to note that the difference between revocation statuses `SparseMerkleTreeProof` and `Iden3commRevocationStatusV1.0` lies in the format of the response/request. While `SparseMerkleTreeProof` uses the non-protocol request-response format, `Iden3commRevocationStatusV1.0` relays the [iden3comm protocol](http://iden3-communication.io/) for communication.

## **Iden3OnchainSparseMerkleTreeProof2023**

The `Iden3OnchainSparseMerkleTreeProof2023` type is specifically used for revocation trees which are stored on the blockchain.

Here are two examples of the credential status (CS) objects using this type:

**Example:**

```json
{
    "id": "did:polygonid:polygon:mumbai:2qCU58EJgrELbXjWbWGC9kPPnczQdp93nUR6LC45F6/credentialStatus?revocationNonce=1051565438&contractAddress=80001:0x2fCE183c7Fbc4EbB5DB3B0F5a63e0e02AE9a85d2&state=a1abdb9f44c7b649eb4d21b59ef34bd38e054aa3e500987575a14fc92c49f42c",
    "type": "Iden3OnchainSparseMerkleTreeProof2023",
    "revocationNonce": 1051565438
}
```

In both examples, the `id` field is a valid Decentralized Identifier (DID) with one required `contractAddress` and two optional parameters: `revocationNonce` and `state`.

Where:

- `contractAddress` consists of two parts: the `chainID`, which specifies the blockchain where the contract exists, and the smart contract address used for generating non-revocation proof.
- `revocationNonce` represents the credential nonce.
- `state` refers to the most recently published issuer state or genesis.

The format of the `id` field follows this structure:

```
[did]:[methodid]:[chain]:[network]:[id]/credentialStatus?(revocationNonce=value)&[contractAddress=[chainID]:[contractAddress]]&(state=issuerState)
```

## Workflow

To verify the revocation status of an onchain using the `Iden3OnchainSparseMerkleTreeProof2023` type, follow these steps:

1. Parse the `id` as a valid DID and extract the on-chain issuer contract address from this `id`:
a. If the `contractAddress` parameter is not empty, use this address to build the non-revocation proof.
b. If the `contractAddress` is empty return an error. 
2. Extract `chainID` from `contractAddress` parameter. If `chainID` not exists - extract chain id from DID.
3. Parse the `id` to obtain the `revocationNonce`:
a. You can extract the `revocationNonce` from the `id` parameter `revocationNonce`.
b. If the `id` doesn't have the `revocationNonce`, you can get the `revocationNonce` from the `revocationNonce` field.
c. If the parameter doesn't exist and the `revocationNonce` field is empty, consider this VC document invalid.
4. Get latest state for `id`
    1. If you encounter the error [Identity does not exist](https://github.com/iden3/contracts/blob/107ec52213b5f8f402e5645d97a9579926a7de0a/contracts/lib/StateLib.sol#L92), please check whether the `state` parameter from `id` corresponds to the genesis state. 
    
           If the state parameter does not exist or is not the genesis state, return an error.
    
5. Generate revocation proof call method `getRevocationStatusByIdAndState`.
`id` - id extracted from issuer DID.
`state` - latest state or genesis from step 4.
`nonce` - nonce from step 3.
    
    ```json
    const response = await this.onchainContract.getRevocationStatusByIdAndState(id, state, nonce);
    ```
    
    - Use this ABI to make getRevocationStatusByIdAndState call
        
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
                "internalType": "uint256",
                "name": "state",
                "type": "uint256"
              },
              {
                "internalType": "uint64",
                "name": "nonce",
                "type": "uint64"
              }
            ],
            "name": "getRevocationStatusByIdAndState",
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
        
    
    Also, you can use the signature of getRevocationStatusByIdAndState `0xaad72921` instead of ABI.
    
    Example of implementation: [JS](https://github.com/0xPolygonID/js-sdk/blob/5ffd319f0e01a95963364a4622d98c970ef0ec59/src/credentials/status/on-chain-revocation.ts), [GO](https://github.com/0xPolygonID/c-polygonid/blob/16c1705655ddbb1ef9f2247d33bc5f8952983fd7/inputs_sig.go#L1372)
