
type: `/credentials/1.0/onchain-offer`

The onchain offer message comprises information regarding the available verifiable credentials (VCs) from an onchain issuer.

```json
{
	"transaction_data": "{<information_about_smart_contract>}",
	"credentials": [
		{
			"id": "<vc_uuid>",
			"description": "<vc_description>"
		}
	]
}
```

| Field | Description | Type | Required |
| --- | --- | --- | --- |
| credentials | List of available credentials on onchain issuer for fetch | list | ✅ |
| credentials.id | ID of onchain credential | string | ✅ |
| credentials.description | Additional description of VC | string | ❌ |
| transaction_data.contract_address | Smart contract address | string | ✅ |
| transaction_data.method_id | Smart contract method (hash from sc method name) | string | ✅ |
| transaction_data.chain_id | Chain identification | string | ✅ |
| transaction_data.network | Chain network | string | ✅ |

- **Example of credential onchain offer:**
    
    ```json
    {
      "id": "36f9e851-d713-4b50-8f8d-8a9382f138ca",
      "thid": "36f9e851-d713-4b50-8f8d-8a9382f138ca",
      "typ": "application/iden3comm-plain-json",
      "type": "https://iden3-communication.io/credentials/1.0/onchain-offer",
      "body": {
        "credentials": [
          {
            "description": "NonZeroBalance",
            "id": "1"
          }
        ],
        "transaction_data": {
            "contract_address": "0xe826f870852d7eeeb79b2c030298f9b5daa8c8a3",
            "method_id":"0x37c1d9ff",
            "chain_id": 80001,
            "network": "polygon-mumbai"
        }
      },
      "to": "did:polygonid:polygon:mumbai:2qJUZDSCFtpR8QvHyBC4eFm6ab9sJo5rqPbcaeyGC4"
    }
    ```
