
type: `/devices/1.0/registration`

`push token` registration method. To send a silent push notification later.

```json
{
	"app_id": "<notification_service_app_id>",
	"push_token": "<firebase_ios_android_token>"
}
```

| Field | Description | Type | Required |
| --- | --- | --- | --- |
| app_id | Notification server app_id | string | ✅ |
| push_token | Token for send notificaiton from firebase | string | ✅ |

- **Example of device registration request:**
    
    ```json
    {
      "id": "005a39c5-5d56-4286-9b48-f1d80772c3e7",
      "thid": "005a39c5-5d56-4286-9b48-f1d80772c3e7",
      "typ": "application/iden3comm-plain-json",
      "type": "https://iden3-communication.io/devices/1.0/registration"
      "body": {
        "app_id": "example.com",
        "push_token": "ceWdRd2F6WnAyVuFQRFjK3WUXq2LorSPyG9LJ=="
      },
      "from": "114vgnnCupQMX4wqUBjg5kUya3zMXfPmKc9HNH4TSE"
    }
    ```
