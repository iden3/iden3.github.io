
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
| scope.params | circuit specific params| map) | ❌|
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
      "from": "did:polygonid:polygon:mumbai:2qFroxB5kwgCxgVrNGUM6EW3khJgCdHHnKTr3VnTcp",
      "body": {
        "scope": [
          {
            "id": 1,
            "circuitId": "credentialAtomicQuerySigV2",
            "query": {
              "allowedIssuers": ["*"],
              "context": "https://raw.githubusercontent.com/iden3/claim-schema-vocab/main/schemas/json-ld/kyc-v3.json-ld",
              "type": "KYCAgeCredential",
              "credentialSubject": {
                "birthday": {
                  "$lt": 2000101
                }
              }
            }
          }
        ],
    		"transaction_data": {
    			"contract_address": "0xe826f870852d7eeeb79b2c030298f9b5daa8c8a3",
    			"method_id":"b68967e2",
    			"chain_id": 80001,
    			"network": "polygon-mumbai"
    		}
      }
    }
    ```
