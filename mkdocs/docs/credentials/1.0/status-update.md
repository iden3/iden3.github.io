
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
      "from": "11tbD2cY9ZuZc8oQWN5bhtvNVrqmf1zdnES3emJET",
      "to": "118he3vAmZTWPaD7cyFYKz8ztjXceRGBPYgiuz8CQX",
      "body": {
    		"id": "118he3vAmZTWPaD7cyFYKz8ztjXceRGBPYgiuz8CQX",
    		"reason": "issuer key was revoked"
      }
    }
    ```
