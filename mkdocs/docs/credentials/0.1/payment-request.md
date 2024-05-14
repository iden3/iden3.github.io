
type: `/credentials/0.1/payment-request`

Request for payment from user.

```json
{
  "agent": "https://issuer.com",
  "payments": [
    {
      "credentials": [
        {
          "type": "AML",
          "context": "http://test.com"
        }
      ],
      "type":"PaymentRequest",
      "data":{
        "type":"Iden3PaymentRequestCryptoV1",
        "amount":10,
        "id": "1", 
        "chainID": "80002",
        "address": "123" 
      },
      "expiration": "timestamp", // expiration time of payment-request
      "description":"you can pass the verification on our KYC provider by following the next link",
    }
  ]
}
```

| Field                           | Description                                               | Type                                    | Required |
|---------------------------------|-----------------------------------------------------------|-----------------------------------------|----------|
| metadata                        | Type specific metadata regarding current proposal request | object                                  | ❌        |
| did_doc                         | User did document                                         | JSON                                    | ❌        |
| agent                           | Issuer URL to send payment response                       | string                                  | ✅ |
| payments                        | List of  payment requests                                 | list                                    | ✅        |
| payments[i].type                | Type of payment request                                   | list                                    | ✅        |
| payments[i].credentials         | List of  credentials that user requests for               | list                                    | ✅        |
| payments[i].credentials.type    | type of VC                                                | string                                  | ✅        |
| payments[i].credentials.context | JSON-LD of VC                                             | string                                  | ✅        |
| payments[i].data                | Payment request specific details                          | object                                  | ✅        |
| payments[i].data.id             | Payment id                                                | string                                  | ✅        |
| payments[i].data.type           | Payment Type                                              | string                                  | ✅        |
| payments[i].data.chainId        | Payment id                                                | string                                  | ✅        |
| payments[i].data.address        | smart-contract address or reciever address                | string  | ✅        |
| payments[i].data.amount         | Payment amount                                            | integer                                 | ✅        |


- **Example of credential payment request:**

    ```json
    {
      "id": "36f9e851-d713-4b50-8f8d-8a9382f138ca",
      "thid": "36f9e851-d713-4b50-8f8d-8a9382f138ca",
      "typ": "application/iden3comm-plain-json",
      "type": "https://iden3-communication.io/credentials/0.1/payment-request",
      "body": {
         "agent": "https://issuer.com", 
         "payments": [
          {
             "credentials": [
              {
               "type": "AML",
               "context": "http://test.com"
              }
             ],
             "type":"PaymentRequest",
             "data":{
                 "type":"Iden3PaymentRequestCryptoV1",
                 "amount":10, 
                 "id": "ox",
                 "chainID": "80002", 
                 "address": "0xpay1"
             },
            "expiration": "timestamp", // expiration time of payment-request
            "description":"you can pass the verification on our KYC provider by following the next link",
            }
          ]
      },
      "to": "did:polygonid:polygon:mumbai:2qJUZDSCFtpR8QvHyBC4eFm6ab9sJo5rqPbcaeyGC4",
      "from": "did:iden3:polygon:mumbai:x3HstHLj2rTp6HHXk2WczYP7w3rpCsRbwCMeaQ2H2"
    }

    ```
