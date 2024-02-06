
type: `/revocation/1.0/request-status`

This message enables querying the revocation status of a nonce.

```json
{
	"revocation_nonce": "<revocation_nonce>"
}
```

| Field | Description | Type | Required |
| --- | --- | --- | --- |
| revocation_nonce | revocation nonce | interger | ✅ |

- **Example of revocation status request:**
    
    ```json
    {
        "id": "1924af5a-7d63-4850-addf-0177cdc34786",
        "thid": "1924af5a-7d63-4850-addf-0177cdc34786",
        "type": "https://iden3-communication.io/revocation/1.0/request-status",
        "to": "did:polygonid:polygon:mumbai:2qJUZDSCFtpR8QvHyBC4eFm6ab9sJo5rqPbcaeyGC4",
        "from": "did:iden3:polygon:mumbai:x3HstHLj2rTp6HHXk2WczYP7w3rpCsRbwCMeaQ2H2",
        "typ": "application/iden3comm-plain-json",
        "body": {
            "revocation_nonce": 12314436336
        }
    }
    ```
