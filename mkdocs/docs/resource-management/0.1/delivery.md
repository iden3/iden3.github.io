
type `/resource-management/0.1/delivery`

This message is used to deliver data or responses related to a specific resource between parties.
An agent sends it to transfer a payload (e.g., an encrypted profile or authorization response) as an attachment, along with its current delivery status.
The status field indicates whether the delivery is pending, completed, or rejected.

```json
    {
        "id": "<resource_id>",
        "attachment_id": "<attachment_id>",
        "status": "pending | completed | rejected"
    }
```

| Field             | Description                                                                                                                               | Type   | Required |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------- | ------ | -------- |
| **id**            | Unique identifier of the resource associated with this delivery. In the current implementation, this corresponds to the configuration ID. | string | ✅        |
| **attachment_id** | Identifier of the attachment being delivered. Must match the attachment object’s `id`.                                                    | string | ✅        |
| **status**        | Current delivery status: `pending`, `completed`, or `rejected`.                                                                           | string | ✅        |

- **Example of delivery:**
    ```json
    {
        "id": "f8aee09d-f592-4fcc-8d2a-8938aa26676c",
        "typ": "application/iden3comm-plain-json",
        "type": "https://iden3-communication.io/resource-management/0.1/delivery",
        "thid": "f8aee09d-f592-4fcc-8d2a-8938aa26676c",
        "from": "did:iden3:polygon:amoy:bob",
        "to": "did:iden3:polygon:amoy:zkroom",
        "body": {
            "id": "1",
            "attachment_id": "urn:uuid:1",
            "status": "pending"
        },
        "attachments": [
            {
            "id": "urn:uuid:1",
            "description": "encrypted auth response of Alice profile as attachment",
            "media_type": "application/iden3-encrypted-json",
            "data": {
                "json": {
                "ciphertext": "encrypted profile",
                "iv": "cNpGtrRQRiYOBy0TyD6-dA",
                "protected": "eyJlbmMiOiJBMjU2Q0JDLUhTNTEyIn0",
                "recipients": [
                    {
                    "encrypted_key": "E1qedVZsQFcXrE7d7veV-uKPFw7In8137FfRO3vFvXjkDcdi3MxS7tF4vWYVRh6zZf3HjYs2BJJks_ZRlc7hahtUC1eByXGcp0QHUIIDZ9dkqcULnH93jCWA8vIBcpMHBvEp71uHAflduwnkXUrTQhqwucDEzMeIqsiOW65LrxSfes02CJUtYkMGU6RR9nhDexbp8cuJUcQ1KKe4kQgF3LKyxk9Usmvzr8ijsK0LKUQBLaIlQALEYEhEcYvA8QNsgaKc7_d4ehdwCLdhZjIOWtvS8ItRr1_2Zikkh20YznNGOPjGeV6gGeMq4-Ns5TnRcmFqXWe9N7FvuGJVBh3vVQ",
                    "header": {
                        "alg": "RSA-OAEP-256",
                        "kid": "did:iden3:polygon:amoy:bob#encryption-key-1"
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