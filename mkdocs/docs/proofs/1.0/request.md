
type: `/proof/1.0/request`

A resource initiates a request to a user. The user is required to generate a zero-knowledge proof and include this proof within the proof response.

```json
{
	"scope": "[<list_of_asked_information_from_user>]"
}
```

| Field | Description | Type | Required |
| --- | --- | --- | --- |
| scope.id | Unique request id | uint64 | ✅ |
| scope.circuitId | Information that circuit should use user for generating zk proof | string | ✅ |
| scope.optional | ? | boolean | ❌ |
| scope.query | Information about what information the user must prove with ZKPproof | map | ✅ |

`scope.query` - can be emty object.

- **Example of proof request:**
    
    ```json
    {
      "id": "f8aee09d-f592-4fcc-8d2a-8938aa26676c",
      "typ": "application/iden3comm-plain-json",
      "type": "https://iden3-communication.io/proofs/1.0/request",
      "thid": "f8aee09d-f592-4fcc-8d2a-8938aa26676c",
      "from": "did:iden3:polygon:mumbai:x3HstHLj2rTp6HHXk2WczYP7w3rpCsRbwCMeaQ2H2",
      "body": {
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
