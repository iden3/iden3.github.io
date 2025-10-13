
type `/resource-management/0.1/permissions-update-request`

An agent (e.g., a service or resource controller) sends this message to a client or resource owner to update permission records associated with a specific resource.
It communicates the current state of access permissions and may include new entries to add or existing entries to remove.
Attachments can also be included to share encrypted information about the requester or related authorization data.

```json
{
  "id": "<resource_id>",
  "current": ["<list_of_current_dids_with_access>"],
  "add": ["<list_of_dids_to_grant_access>"],
  "remove": ["<list_of_dids_to_revoke_access>"]
}
```

| Field       | Description                                                                                                                                         | Type     | Required |
| ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- |
| **id**      | Unique identifier of the resource for which permissions are being updated. In the current implementation, this corresponds to the configuration ID. | string   | ✅        |
| **current** | List of DIDs that currently have access to the resource. Must always be present, even if empty.                                                     | string[] | ✅        |
| **add**     | List of DIDs to which access should be newly granted.                                                                                               | string[] | ❌        |
| **remove**  | List of DIDs whose access should be revoked.                                                                                                        | string[] | ❌        |



- **Example of permissions-update-request:**

 ```json
    {
    "id": "f8aee09d-f592-4fcc-8d2a-8938aa26676c",
    "typ": "application/iden3comm-plain-json",
    "type": "https://iden3-communication.io/resource-management/0.1/permissions-update-request",
    "thid": "f8aee09d-f592-4fcc-8d2a-8938aa26676c",
    "from": "did:iden3:polygon:amoy:zkroom",
    "to": "did:iden3:polygon:amoy:alice",
    "body": {
        "id": "1",
        "current": [
        "did:iden3:polygon:amoy:john",
        "did:iden3:polygon:amoy:emma"
        ],
        "add": [
        "did:iden3:polygon:amoy:bob"
        ],
        "remove": [
        "did:iden3:polygon:amoy:alex"
        ]
    },
    "attachments": [
        {
        "id": "urn:uuid:1",
        "description": "encrypted auth response of Bob’s email profile as attachment",
        "media_type": "application/iden3-encrypted-json",
        "data": {
            "json": {
            "ciphertext": "encrypted bob profile",
            "iv": "cNpGtrRQRiYOBy0TyD6-dA",
            "protected": "eyJlbmMiOiJBMjU2Q0JDLUhTNTEyIn0",
            "recipients": [
                {
                "encrypted_key": "E1qedVZsQFcXrE7d7veV-65LrxSfes02CJUtYkMGU6RRxbp8cuJUcQ1KKe4kQgF3LKyxk9Usmvzr8ijsK0LKUQBLaIlQALEYEhEcYvA8QNsgaKc7_d4ehdwCLdhZjIOWtvS8ItRr1_2Zikkh20YzOPjGeV6gGeMq4-Ns5TnRcmFqXWe9N7FvuGJVBh3vVQ...",
                "header": {
                    "alg": "RSA-OAEP-256",
                    "kid": "did:iden3:polygon:amoy:alice#encryption-key-1"
                }
                }
            ],
            "tag": "utaXyGDjPb5FsoTUjxByia7vmhirN6Td-vDyt7K4HbU"
            }
        }
        }
    ]
  }
 ```