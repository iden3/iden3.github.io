
type `/resource-management/0.1/permissions-list`

A requester (typically a user or agent) receives this message to communicate the current permission state for a specific resource.

It provides lists of users (by their DIDs) who have been granted, rejected, or whose requests are still pending.
This message is commonly used as a response to [/resource-management/0.1/permissions-requests-list-fetch](./permissions-requests-list-fetch.md), or [/resource-management/0.1/permissions-list-fetch](./permissions-list-fetch.md)

```json
{
  "id": "<resource_id>",
  "granted": [{"did": "<did>", "timestamp": <unix_timestamp>}],
  "pending": [{"did": "<did>", "timestamp": <unix_timestamp>}],
  "rejected": [{"did": "<did>", "timestamp": <unix_timestamp>}]
}
```


| Field        | Description                                                                                                                                                              | Type     | Required |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------- | -------- |
| **id**       | Unique identifier of the resource whose permission state is being reported.                                                                                              | string   | ✅        |
| **granted**  | List of objects representing users who have been granted access to the resource. Each entry includes the user’s DID and the timestamp when access was granted.           | object[] | ❌        |
| **pending**  | List of objects representing users whose permission requests are awaiting approval. Each entry includes the user’s DID and the timestamp when the request was received.  | object[] | ❌        |
| **rejected** | List of objects representing users whose permission requests were explicitly rejected. Each entry includes the user’s DID and the timestamp when the rejection occurred. | object[] | ❌        |


| Field         | Description                                                                      | Type   | Required |
| ------------- | -------------------------------------------------------------------------------- | ------ | -------- |
| **did**       | Decentralized Identifier (DID) of the user.                                      | string | ✅        |
| **timestamp** | Unix timestamp (in seconds) representing when the permission state was recorded. | number | ❌        |


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
        {
          "did": "did:iden3:polygon:amoy:bob",
          "timestamp": 1738860452
        }
      ],
      "pending": [
        {
          "did": "did:iden3:polygon:amoy:emma",
          "timestamp": 1738860400
        }
      ],
      "rejected": [
        {
          "did": "did:iden3:polygon:amoy:john",
          "timestamp": 1738859900
        }
      ]
    }
   }
  ```