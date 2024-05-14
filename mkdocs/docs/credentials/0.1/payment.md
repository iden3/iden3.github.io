
type: `/credentials/0.1/payment`

Payment response with details.

```json
{
  "payments": [
    {
      "id":"123",
      "type":"Iden3PaymentCryptoV1",
      "paymentData":{
        "txId": "0x123"
      }
    }
  ]
}
```

| Field                        | Description                                               | Type   | Required |
|------------------------------|-----------------------------------------------------------|--------|----------|
| payments                     | List of  payment requests                                 | list   | ✅        |
| payments[i].id               | Payment id                                                | string | ✅        |
| payments[i].type             | Payment Type                                              | string | ✅        |
| payments[i].paymentData      | specifc payment data                                      | object | ✅        |
| payments[i].paymentData.txId | transaction id                                            | string | ✅        |


- **Example of credential payment response:**

    ```json
    {
      "id": "36f9e851-d713-4b50-8f8d-8a9382f138ca",
      "thid": "36f9e851-d713-4b50-8f8d-8a9382f138ca",
      "typ": "application/iden3comm-plain-json",
      "type": "https://iden3-communication.io/credentials/0.1/payment",
      "body": {
         "payments": [
              {
               "id":"123",
               "type":"Iden3PaymentCryptoV1",
                "paymentData": { 
                   "txId": "0x123"
                }
             }
          ]
      },
      "to": "did:polygonid:polygon:mumbai:2qJUZDSCFtpR8QvHyBC4eFm6ab9sJo5rqPbcaeyGC4",
      "from": "did:iden3:polygon:mumbai:x3HstHLj2rTp6HHXk2WczYP7w3rpCsRbwCMeaQ2H2"
    }

    ```
