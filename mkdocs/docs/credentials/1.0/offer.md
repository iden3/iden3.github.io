
type: `/credentials/1.0/offer`

The offer message comprises information regarding the available verifiable credentials (VCs) from an issuer.

```json
{
	"url": "<issuer_url>",
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
| url | Issuer URL for fetch credential | string | ✅ |
| credentials | List of available credentials on issuer for fetch | list | ✅ |
| credentials.id | ID of VC | string | ✅ |
| credentials.description | Additional description of VC | string | ❌ |

- **Example of credential offer:**
    
    ```json
    {
      "id": "36f9e851-d713-4b50-8f8d-8a9382f138ca",
      "thid": "36f9e851-d713-4b50-8f8d-8a9382f138ca"
      "typ": "application/iden3comm-plain-json",
      "type": "https://iden3-communication.io/credentials/1.0/offer",
      "body": {
        "credentials": [
          {
            "description": "KYCAgeCredential",
            "id": "c7b66a79-b930-49d1-9a97-66ab8fd792ac"
          }
        ],
        "url": "http://issuer-agent.com/"
      },
      "to": "119tqceWdRd2F6WnAyVuFQRFjK3WUXq2LorSPyG9LJ",
      "from": "114vgnnCupQMX4wqUBjg5kUya3zMXfPmKc9HNH4TSE"
    }
    ```
    