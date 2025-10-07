
type `/resource-management/0.1/permissions-list-fetch`

A requester (typically a user or agent) sends this message to retrieve a [list](./permissions-list.md) of permission requests that have been sent to them by other parties for a specific resource.
It is useful for reviewing and managing pending, approved, or rejected permission requests received from other users.

```json
{
  "id": "<resource_id>"
}
```

| Field  | Description                                                                                              | Type   | Required |
| ------ | -------------------------------------------------------------------------------------------------------- | ------ | -------- |
| **id** | Unique identifier of the resource for which the requester wants to fetch their sent permission requests. | string | ✅        |


- **Example of permissions-list-fetch:**
    ```json
    {
    "id": "f8aee09d-f592-4fcc-8d2a-8938aa26676c",
    "typ": "application/iden3comm-plain-json",
    "type": "https://iden3-communication.io/resource-management/0.1/permissions-list-fetch",
    "thid": "f8aee09d-f592-4fcc-8d2a-8938aa26676c",
    "from": "did:iden3:polygon:amoy:bob",
    "to": "did:iden3:polygon:amoy:zkroom",
    "body": {
        "id": "1"
        }
    }
    ```