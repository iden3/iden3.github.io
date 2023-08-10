
type: `/authorization/1.0/request`

A resource initiates a request to a user. The user is required to generate a zero-knowledge proof and include this proof within the authorization response in order to log in to the resource.

```json
{
	"callbackUrl": "<url_for_send_user`s_authorization_response>",
	"reason": "<reason_for_the_request>",
	"message": "<authorization_request_payload>",
	"did_doc": "<did_doc>",
	"scope": "[<list_of_asked_information_from_user>]"
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
| scope.optional | ? | boolean | ❌ |
| scope.query | Information about what information the user must prove with ZKPproof | map | ✅ |

`scope.query` - can be emty object.

- **Example of authorization request:**
    
    ```json
    {
      "id": "f8aee09d-f592-4fcc-8d2a-8938aa26676c",
      "typ": "application/iden3comm-plain-json",
      "type": "https://iden3-communication.io/authorization/1.0/request",
      "thid": "f8aee09d-f592-4fcc-8d2a-8938aa26676c",
      "from": "1125GJqgw6YEsKFwj63GY87MMxPL9kwDKxPUiwMLNZ",
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
