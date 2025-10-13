
type `/resource-management/0.1/request`

A requester (e.g., a user or a resource) sends a message to return or communicate the status of a previously initiated [permissions request](./permissions-request.md). 
This message does not start a new permission flow but instead communicates via [delivery message](./delivery.md) the current state of an existing request (e.g., pending, approved, or rejected).

```json
{
  "id": "<resource_id>",
  "owner": "<owner_did>"
}
```

| Field     | Description                                                          | Type   | Required |
| --------- | -------------------------------------------------------------------- | ------ | -------- |
| **id**    | Unique identifier of the resource related to the permission request. | string | ✅        |
| **owner** | The DID of the resource owner. If omitted, the `to` field of the message is assumed to represent the owner.                                     | string | ❌        |

- **Example of request:**

 ```json
   {
    "id": "f8aee09d-f592-4fcc-8d2a-8938aa26676c",
    "typ": "application/iden3comm-plain-json",
    "type": "https://iden3-communication.io/resource-management/0.1/request",
    "thid": "f8aee09d-f592-4fcc-8d2a-8938aa26676c",
    "from": "did:iden3:polygon:amoy:bob",
    "to": "did:iden3:polygon:amoy:zkroom",
    "body": {
        "id": "1",
        "owner": "did:iden3:polygon:amoy:alice"
    }
   }
  ```
