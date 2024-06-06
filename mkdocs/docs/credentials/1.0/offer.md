
type: `/credentials/1.0/offer`

The offer message comprises information regarding the available verifiable credentials (VCs) from an issuer.

```json
{
	"url": "<issuer_url>",
	"credentials": [
		{
			"id": "<vc_uuid>",
			"description": "<vc_description>",
            "status": "pending | completed | rejected"
		}
	]
}
```

| Field                   | Description                                                              | Type | Required |
|-------------------------|--------------------------------------------------------------------------| --- | --- |
| url                     | Issuer URL for fetch credential                                          | string | ✅ |
| credentials             | List of available credentials on issuer for fetch                        | list | ✅ |
| credentials.id          | ID of VC                                                                 | string | ✅ |
| credentials.description | Additional description of VC                                             | string | ❌ |
| credentials.status      | Status of the offer for VC. If omitted should be considered as completed | string | ❌ |


- **Example of credential offer:**
    
    ```json
    {
      "id": "36f9e851-d713-4b50-8f8d-8a9382f138ca",
      "thid": "36f9e851-d713-4b50-8f8d-8a9382f138ca",
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
      "to": "did:polygonid:polygon:mumbai:2qJUZDSCFtpR8QvHyBC4eFm6ab9sJo5rqPbcaeyGC4",
      "from": "did:iden3:polygon:mumbai:x3HstHLj2rTp6HHXk2WczYP7w3rpCsRbwCMeaQ2H2"
    }
    ```
