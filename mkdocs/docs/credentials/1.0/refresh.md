
type: `/credentials/1.0/refresh`

The refresh message contains information about the credential that need to be refreshed.

```json
{
	"id": "<resource_id>",
    "reason": "<reason>"
}
```

| Field | Description | Type | Required |
| --- | --- | --- | --- |
| id | Credential identifier | string | ✅ |
| reason | Reason of refresh | string | ✅ |

- **Example of credential refresh:**
    
    ```json
    {
      "id": "36f9e851-d713-4b50-8f8d-8a9382f138ca",
      "thid": "36f9e851-d713-4b50-8f8d-8a9382f138ca",
      "typ": "application/iden3comm-plain-json",
      "type": "https://iden3-communication.io/credentials/1.0/offer",
      "body": {
        "id": "c7b66a79-b930-49d1-9a97-66ab8fd792ac",
        "reason": "expired"
      },
      "to": "did:polygonid:polygon:mumbai:2qJUZDSCFtpR8QvHyBC4eFm6ab9sJo5rqPbcaeyGC4",
      "from": "did:iden3:polygon:mumbai:x3HstHLj2rTp6HHXk2WczYP7w3rpCsRbwCMeaQ2H2"
    }
    ```
