
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
        "from": "119tqceWdRd2F6WnAyVuFQRFjK3WUXq2LorSPyG9LJ",
        "to": "114vgnnCupQMX4wqUBjg5kUya3zMXfPmKc9HNH4TSE"
        "typ": "application/iden3comm-plain-json",
        "body": {
            "revocation_nonce": 12314436336
        }
    }
    ```
