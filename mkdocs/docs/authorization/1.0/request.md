
type: `/authorization/1.0/request`

A resource initiates a request to a user. The user is required to generate a zero-knowledge proof and include this proof within the authorization response in order to log in to the resource.

```json
{
	"callbackUrl": "<url_for_send_user`s_authorization_response>",
	"reason": "<reason_for_the_request>",
	"message": "<authorization_request_payload>",
	"did_doc": "<did_doc>",
	"scope": "[<list_of_requested_proofs_from_user>]"
}
```

| Field | Description | Type | Required |
| --- | --- | --- | --- |
| callbackUrl | User should use this url for send authorization response | string | ✅ |
| reason | Reason for the request | string | ❌ |
| message | Message payload | string | ❌ |
| did_doc | Resource did doc | JSON | ❌ |
| scope.id | Unique request id | uint64 | ✅ |
| scope.circuitId | Information that circuit should use user for generating zk proof | string | ✅ |
| scope.optional | indicates that proof is optional| boolean | ❌ |
| scope.query.skipClaimRevocationCheck | Indicates if revocation check can be omitted during zkp generation | boolean | ❌ |
| scope.query.groupId | group id to create the same link nonce for linked proofs and use the same query | number | ❌ |
| scope.query.proofType | Proof type that must persist in the W3C credential for zkp proof | string | ❌ |
| scope.query | Information about what information the user must prove with ZKPproof | map | ✅ |
| scope.query.allowedIssuers | Credentials only from these issuers will be used for zero-knowledge proof generation | array | ✅ |
| scope.query.type | Credential type | string | ✅ |
| scope.query.context | JSON LD url of credential type context | string | ✅ |
| scope.query.credentialSubject | Credential subject of W3C credential | map | ✅ |
| scope.query.credentialSubject.{field} | Credential subject field of W3C credential | map | ✅ |
| scope.query.credentialSubject.{field}.{operator} | Feild operator for zkp and comparison value | object | ✅ |
| scope.params | circuit specific params| map) | ❌|
| scope.params.nullifierSessionId | nullifier session id to create a nullifier  for V3 circuit| string (bigInt) | ❌|



`scope.query` - can be empty object.
`scope.params` - can be empty object.


- **Example of authorization request:**
    
    ```json
    {
      "id": "f8aee09d-f592-4fcc-8d2a-8938aa26676c",
      "typ": "application/iden3comm-plain-json",
      "type": "https://iden3-communication.io/authorization/1.0/request",
      "thid": "f8aee09d-f592-4fcc-8d2a-8938aa26676c",
      "from": "did:polygonid:polygon:mumbai:2qFroxB5kwgCxgVrNGUM6EW3khJgCdHHnKTr3VnTcp",
      "body": {
        "callbackUrl": "https://test.com/callback",
        "reason": "age verification",
        "message": "test message",
        "scope": [
          {
            "id": 1,
            "circuitId": "credentialAtomicQuerySigV2",
            "query": {
              "allowedIssuers": ["*"],
              "context": "https://raw.githubusercontent.com/iden3/claim-schema-vocab/main/schemas/json-ld/kyc-v101.json-ld",
              "type": "KYCEmployee",
              "credentialSubject": {
                "hireDate": {
                  "$eq": "1996-04-24"
                }
              }
            }
          }
        ]
      }
    }
    ```


- **Example of authorization request with multiple proof queries:**

    ```json
    {
      "id": "f8aee09d-f592-4fcc-8d2a-8938aa26676c",
      "typ": "application/iden3comm-plain-json",
      "type": "https://iden3-communication.io/authorization/1.0/request",
      "thid": "f8aee09d-f592-4fcc-8d2a-8938aa26676c",
      "from": "did:polygonid:polygon:mumbai:2qFroxB5kwgCxgVrNGUM6EW3khJgCdHHnKTr3VnTcp",
      "body": {
        "callbackUrl": "https://test.com/callback",
        "reason": "age verification",
        "message": "test message",
        "scope": [
          {
            "id": 1,
            "circuitId": "credentialAtomicQuerySigV2",
            "query": {
              "allowedIssuers": ["*"],
              "context": "https://raw.githubusercontent.com/iden3/claim-schema-vocab/main/schemas/json-ld/kyc-v101.json-ld",
              "type": "KYCEmployee",
              "credentialSubject": {
                "position": {
                  "$eq": "developer"
                }
              }
            }
          },
          {
            "id": 2,
            "circuitId": "credentialAtomicQuerySigV2",
            "query": {
              "allowedIssuers": ["*"],
              "context": "https://raw.githubusercontent.com/iden3/claim-schema-vocab/main/schemas/json-ld/kyc-v101.json-ld",
              "type": "KYCCountryOfResidenceCredential",
              "credentialSubject": {
                "countryCode": {
                  "$in": [980, 340]
                }
              }
            }
          }
        ]
      }
    }
    ```
- **Example of authorization request without proof queries (basic auth:**

    ```json
    {
      "id": "f8aee09d-f592-4fcc-8d2a-8938aa26676c",
      "typ": "application/iden3comm-plain-json",
      "type": "https://iden3-communication.io/authorization/1.0/request",
      "thid": "f8aee09d-f592-4fcc-8d2a-8938aa26676c",
      "from": "did:polygonid:polygon:mumbai:2qFroxB5kwgCxgVrNGUM6EW3khJgCdHHnKTr3VnTcp",
      "body": {
        "callbackUrl": "https://test.com/callback",
        "reason": "age verification",
        "message": "test message",
        "scope": []
      }
    }
    ```
  
- **Example of request to V3 atomic circuit with / without nullifier and linked proofs**

    ```json
    {
        "id": "f8aee09d-f592-4fcc-8d2a-8938aa26676c",
        "typ": "application/iden3comm-plain-json",
        "type": "https://iden3-communication.io/authorization/1.1/request",
        "thid": "f8aee09d-f592-4fcc-8d2a-8938aa26676c",
        "from": "did:polygonid:polygon:mumbai:2qFroxB5kwgCxgVrNGUM6EW3khJgCdHHnKTr3VnTcp",
        "body": {
          "callbackUrl": "https://test.com/callback",
          "reason": "age verification",
          "message": "test message",
          "scope": [
            {
              "id": 1,
              "circuitId": "credentialAtomicQueryV3",
              "params": {
                "nullifierSessionId" : "123443290439234342342423423423423"
              },
              "query": {
                "groupId": 1,
                "proofType": "BJJSignature",
                "allowedIssuers": ["*"],
                "context": "https://raw.githubusercontent.com/iden3/claim-schema-vocab/main/schemas/json-ld/kyc-v101.json-ld",
                "type": "KYCEmployee",
                "credentialSubject": {
                  "position": {
                    "$eq": "developer"
                  }
                }
              }
            },
            {
              "id": 2,
              "circuitId": "smallCircuit",
              "query": {
                  "groupId" : 1,
                  "credentialSubject": {
                      "bithdate": {
                        "$lt": "20010101"
                    }
                }
              }
            },
            {
              "id": 3,
              "circuitId": "credentialAtomicQueryV3",
              "query": {
                "allowedIssuers": ["*"],
                "context": "https://raw.githubusercontent.com/iden3/claim-schema-vocab/main/schemas/json-ld/kyc-v101.json-ld",
                "type": "KYCCountryOfResidenceCredential",
                "credentialSubject": {
                  "countryCode": {
                    "$in": [980, 340]
                  }
                }
              }
            }
          ]
        }
    }
    ```