
type: `/credentials/1.0/status-update`

The message contains information about the credential status.

```json
{
	"id": "<credential_id>",
	"reason": "<text_to_display>"
}
```

| Field | Description | Type | Required |
| --- | --- | --- | --- |
| id | Credential ID | string | ✅ |
| reason | Description of the status | string | ✅ |

- **Example of status update message:**
    
    ```json
    {
      "id": "f4b6f1a3-ebf4-49a7-8c2d-5d2649b1e65d",
      "typ": "application/iden3comm-plain-json",
      "type": "https://iden3-communication.io/credentials/1.0/status",
      "to": "did:polygonid:polygon:mumbai:2qJUZDSCFtpR8QvHyBC4eFm6ab9sJo5rqPbcaeyGC4",
      "from": "did:iden3:polygon:mumbai:x3HstHLj2rTp6HHXk2WczYP7w3rpCsRbwCMeaQ2H2",
      "body": {
    		"id": "118he3vAmZTWPaD7cyFYKz8ztjXceRGBPYgiuz8CQX",
    		"reason": "issuer key was revoked"
      }
    }
    ```
