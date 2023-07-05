
type: `/proofs/1.0/contract-invoke-request`

This request allow users to verify zk proof on chain.

```json
{
	"reason": "<reason_for_the_request>",
	"message": "<authorization_request_payload>",
	"did_doc": "<did_doc>",
	"scope": "[<list_of_asked_information_from_user>]",
	"transaction_data": "{<information_about_smart_contract>}"
}
```

| Field | Description | Type | Required |
| --- | --- | --- | --- |
| reason | Reason for the request | string | ❌ |
| message | Message payload | string | ❌ |
| did_doc | Resource did doc | JSON | ❌ |
| scope.id | Unique request id | uint64 | ✅ |
| scope.circuitId | Information that circuit should use user for generating zk proof | string | ✅ |
| scope.optional | ? | boolean | ❌ |
| scope.query | Information about what information the user must prove with ZKPproof | map | ✅ |
| transaction_data.contract_address | Smart contract address | string | ✅ |
| transaction_data.method_id | Smart contract method (hash from sc method name) | string | ✅ |
| transaction_data.chain_id | Chain identification | string | ✅ |
| transaction_data.network | Chain network | string | ✅ |

- **Example of contract invoke:**
    
    ```json
    {
      "id": "f8aee09d-f592-4fcc-8d2a-8938aa26676c",
      "typ": "application/iden3comm-plain-json",
      "type": "https://iden3-communication.io/proofs/1.0/contract-invoke-request",
      "thid": "f8aee09d-f592-4fcc-8d2a-8938aa26676c",
      "from": "1125GJqgw6YEsKFwj63GY87MMxPL9kwDKxPUiwMLNZ"
      "body": {
        "scope": [
          {
            "id": 1,
            "circuit_id": "credentialAtomicQueryMTP",
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
        ],
    		"transaction_data": {
    			"contract_address": "0x...",
    			"method_id":"0x12345",
    			"chain_id": 1,
    			"network": "polygon-mumbai"
    		}
      }
    }
    ```
