
type: `/messages/1.0/fetch`

Message for fetch a message for known resource

```json
{
	"id": "<message_id>"
}
```

| Field | Description | Type | Required |
| --- | --- | --- | --- |
| id | The ID of the message to be received | string | ✅ |

- **Example of fetch message:**
    
    ```json
    {
      "id": "005a39c5-5d56-4286-9b48-f1d80772c3e7",
      "thid": "005a39c5-5d56-4286-9b48-f1d80772c3e7",
      "typ": "application/iden3comm-plain-json",
      "type": "https://iden3-communication.io/messages/1.0/fetch"
      "body": {
        "id": "ceWdRd2F6WnAyVuFQRFjK3WUXq2LorSPyG9LJ"
      },
      "from": "114vgnnCupQMX4wqUBjg5kUya3zMXfPmKc9HNH4TSE"
    }
    ```
