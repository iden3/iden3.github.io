
type `/resource-management/0.1/permissions-list`

A requester (typically a user or agent) receives this message to communicate the current permission state for a specific resource.

It provides lists of users (by their DIDs) who have been granted, rejected, or whose requests are still pending.
This message is commonly used as a response to [/resource-management/0.1/permissions-requests-list-fetch](./permissions-requests-list-fetch.md).  or [/resource-management/0.1/permissions-list-fetch](./permissions-list-fetch.md)

```json
{
  "id": "<resource_id>",
  "granted": ["<list_of_dids_with_granted_access>"],
  "pending": ["<list_of_dids_with_pending_requests>"],
  "rejected": ["<list_of_dids_with_rejected_requests>"]
}
```


| Field        | Description                                                                 | Type     | Required |
| ------------ | --------------------------------------------------------------------------- | -------- | -------- |
| **id**       | Unique identifier of the resource whose permission state is being reported. | string   | ✅        |
| **granted**  | List of DIDs that have been granted access to the resource.                 | string[] | ❌        |
| **pending**  | List of DIDs whose permission requests are awaiting approval.               | string[] | ❌        |
| **rejected** | List of DIDs whose permission requests were explicitly rejected.            | string[] | ❌        |


- **Example of permissions-list:**

    ```json
   {
    "id": "f8aee09d-f592-4fcc-8d2a-8938aa26676c",
    "typ": "application/iden3comm-plain-json",
    "type": "https://iden3-communication.io/resource-management/0.1/permissions-list",
    "thid": "f8aee09d-f592-4fcc-8d2a-8938aa26676c",
    "from": "did:iden3:polygon:amoy:zkroom",
    "to": "did:iden3:polygon:amoy:alice",
    "body": {
            "id": "1",
            "granted": [
            "did:iden3:polygon:amoy:bob"
            ],
            "pending": [
            "did:iden3:polygon:amoy:emma"
            ],
            "rejected": [
            "did:iden3:polygon:amoy:john"
            ]
        }
    }
    ```