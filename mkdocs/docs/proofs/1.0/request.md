
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
      "from": "1125GJqgw6YEsKFwj63GY87MMxPL9kwDKxPUiwMLNZ"
      "body": {
        "scope": [
          {
          "id": 1,
          "circuitId": "credentialAtomicQueryMTP",
            "query": {
              "allowedIssuers": [
                "*"
              ],
              "req": {
                "$lt": "24042000"
              },
              "schema": {
                "url": "http://schema.url",
                "type": "KYCAgeCredential"
              }
            }
          }
        ]
      }
    }
    ```