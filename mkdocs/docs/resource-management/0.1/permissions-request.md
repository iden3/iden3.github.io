
type `/resource-management/0.1/permissions-request`

A requester (e.g., a user or a resource) initiates a permissions request or provides a status for a request to access or manage a specific resource.
This message allows requesting permission from the resource owner (or another authorized entity) to access or share the resource, such as a profile or configuration. It can also include attachments containing additional information about the requester (e.g., encrypted authorization response).

```json
{
  "id": "<resource_id>",
  "reason": "<reason_for_permission_request>",
  "owner": "<owner_did>"
}
```

| Field      | Description                                                                                                                                     | Type   | Required |
| ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | ------ | -------- |
| **id**     | Unique identifier of the resource for which permissions are requested. In the current implementation, this corresponds to the configuration ID. | string | ✅        |
| **reason** | A human-readable explanation of why access is being requested.                                                                                  | string | ❌        |
| **owner**  | The DID of the resource owner. If omitted, the `to` field of the message is assumed to represent the owner.                                     | string | ❌        |

- **Example of permissions-request:**

 ```json
   {
    "id": "f8aee09d-f592-4fcc-8d2a-8938aa26676c",
    "typ": "application/iden3comm-plain-json",
    "type": "https://iden3-communication.io/resource-management/0.1/permissions-request",
    "thid": "f8aee09d-f592-4fcc-8d2a-8938aa26676c",
    "from": "did:iden3:polygon:amoy:bob",
    "to": "did:iden3:polygon:amoy:zkroom",
    "body": {
        "id": "1",
        "reason": "request for profile sharing",
        "owner": "did:iden3:polygon:amoy:alice"
    },
    "attachments": [
        {
        "id": "urn:uuid:1",
        "description": "encrypted auth response of Bob email profile as attachment",
        "media_type": "application/iden3-encrypted-json",
        "data": {
            "json": {
            "ciphertext": "encrypted bob profile",
            "iv": "cNpGtrRQRiYOBy0TyD6-dA",
            "protected": "eyJlbmMiOiJBMjU2Q0JDLUhTNTEyIn0",
            "recipients": [
                {
                "encrypted_key": "E1qedVZsQFcXrE7d7veV-uKPFw7In8137FfRO3vFvXjkDcdi3MxS7tF4vWYVRh6zZf3HjYs2BJJks_ZRlc7hahtUC1eByXGcp0QHUIIDZ9dkqcULnH93jCWA8vIBcpMHBvEp71uHAflduwnkXUrTQhqwucDEzMeIqsiOW65LrxSfes02CJUtYkMGU6RR9nhDexbp8cuJUcQ1KKe4kQgF3LKyxk9Usmvzr8ijsK0LKUQBLaIlQALEYEhEcYvA8QNsgaKc7_d4ehdwCLdhZjIOWtvS8ItRr1_2Zikkh20YznNGOPjGeV6gGeMq4-Ns5TnRcmFqXWe9N7FvuGJVBh3vVQ",
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
