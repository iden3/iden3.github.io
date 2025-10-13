
type `/resource-management/0.1/permissions-update`

A resource owner (e.g., a client or user) sends this message in response to a [/resource-management/0.1/permissions-update-request](./permissions-update-request.md).
It confirms which DIDs are granted or rejected for access to a specific resource.
Attachments may also be included to share encrypted authorization data or other contextual information from the owner.

```json
{
  "id": "<resource_id>",
  "grant": ["<list_of_dids_with_granted_access>"],
  "reject": ["<list_of_dids_with_rejected_access>"]
}
```

| Field      | Description                                                                                                                                         | Type     | Required |
| ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- |
| **id**     | Unique identifier of the resource for which permissions are being updated. In the current implementation, this corresponds to the configuration ID. | string   | ✅        |
| **grant**  | List of DIDs that have been granted access to the resource.                                                                                         | string[] | ❌        |
| **reject** | List of DIDs that were explicitly denied access. This field can be omitted if no rejections are needed.                                             | string[] | ❌        |


- **Example of permissions-update:**

 ```json
 {
  "id": "f8aee09d-f592-4fcc-8d2a-8938aa26676c",
  "typ": "application/iden3comm-plain-json",
  "type": "https://iden3-communication.io/resource-management/0.1/permissions-update",
  "thid": "f8aee09d-f592-4fcc-8d2a-8938aa26676c",
  "from": "did:iden3:polygon:amoy:alice",
  "to": "did:iden3:polygon:amoy:zkroom",
  "body": {
    "id": "1",
    "grant": [
      "did:iden3:polygon:amoy:bob",
      "did:iden3:polygon:amoy:john"
    ],
    "reject": [
      "did:iden3:polygon:amoy:alex"
    ]
  },
  "attachments": [
    {
      "id": "urn:uuid:1",
      "description": "encrypted auth response of Alice profile as attachment",
      "media_type": "application/iden3-encrypted-json",
      "data": {
        "json": {
          "ciphertext": "encrypted alice profile",
          "iv": "cNpGtrRQRiYOBy0TyD6-dA",
          "protected": "eyJlbmMiOiJBMjU2Q0JDLUhTNTEyIn0",
          "recipients": [
            {
              "encrypted_key": "E1qedVZsQFcXrE7d7veV-uKPFw7In8137FfRO3vFvXjkDcdi3MxS7tF4vWYVRh6zZf3HjYs2BJJks_ZRlc7hahtUC1eByXGcp0QHUIIDZ9dkqcULnH93jCWA8vIBcpMHBvEp71uHAflduwnkXUrTQhqwucDEzMeIqsiOW65LrxSfes02CJUtYkMGU6RR9nhDexbp8cuJUcQ1KKe4kQgF3LKyxk9Usmvzr8ijsK0LKUQBLaIlQALEYEhEcYvA8QNsgaKc7_d4ehdwCLdhZjIOWtvS8ItRr1_2Zikkh20YznNGOPjGeV6gGeMq4-Ns5TnRcmFqXWe9N7FvuGJVBh3vVQ",
              "header": {
                "alg": "RSA-OAEP-256",
                "kid": "did:iden3:polygon:amoy:zkroom#encryption-key-1"
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