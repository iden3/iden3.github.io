
type: `/credentials/0.1/payment`

General payment message from user.

```json
{
  "payments": [
    {
      "@context": "https://schema.iden3.io/core/jsonld/payment.jsonld",
      "type": "Iden3PaymentCryptoV1 | Iden3PaymentRailsV1 | Iden3PaymentRailsERC20V1",
      ...
    }
  ]
}
```

Payment message itself defines fields: _payments_ </br>
Payment object itself is also typed.
The possible types for payment object are: _Iden3PaymentCryptoV1_ and _Iden3PaymentRailsV1_; </br>
Corresponding ld context for such types: [https://schema.iden3.io/core/jsonld/payment.jsonld](https://schema.iden3.io/core/jsonld/payment.jsonld)



| Field                        | Description                                               | Type   | Required |
|------------------------------|-----------------------------------------------------------|--------|----------|
| payments                     | List of  payment requests                                 | list   | ✅        |
| payments[i].type             | Payment Type                                              | string | ✅        |



_Iden3PaymentCryptoV1_ is a simple representation of payment response for only one chain.
Type field specification:

| Field            | Description          | Type                   | Required                               |
|------------------|----------------------|------------------------|----------------------------------------|
| id               | Payment id           | string                 | ✅                                      |
| type             | Payment Type         | "Iden3PaymentCryptoV1" | ✅                                      |
| @context         | type  ld context url | string                 | ❌ (historical backward compatibility)  |
| paymentData      | Payment Type         | object                 | ✅                                      |
| paymentData.txId | Transaction hash     | string                 | ✅                                      |


_Iden3PaymentRailsV1_ is a representation of payment data that is result of sending native payment.
Type field specification:

| Field               | Description                             | Type                           | Required |
|---------------------|-----------------------------------------|--------------------------------|----------|
| nonce               | Payment unique nonce                    | string  (non negative integer) | ✅        |
| type                | Payment Type                            | "Iden3PaymentRailsV1"          | ✅        |
| @context            | type  ld context url                    | string                         | ✅        |
| paymentData         | Payment Type                            | object                         | ✅        |
| paymentData.txId    | Transaction hash                        | string                         | ✅        |
| paymentData.chainId | chain id in which payment has been done | string                         | ✅        |



_Iden3PaymentRailsERC20V1_ is a representation of payment data that is result of sending payment using erc20 token.
Type field specification:

| Field                    | Description                             | Type                           | Required |
|--------------------------|-----------------------------------------|--------------------------------|----------|
| nonce                    | Payment unique nonce                    | string  (non negative integer) | ✅        |
| type                     | Payment Type                            | "Iden3PaymentRailsERC20V1"     | ✅        |
| @context                 | type  ld context url                    | string                         | ✅        |
| paymentData              | Payment Type                            | object                         | ✅        |
| paymentData.txId         | Transaction hash                        | string                         | ✅        |
| paymentData.chainId      | chain id in which payment has been done | string                         | ✅        |
| paymentData.tokenAddress | address of token contract               | string                         | ✅        |



**Examples of credential payment responses different payment types:**

??? crypto
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
               "@context": "https://schema.iden3.io/core/jsonld/payment.jsonld",
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


??? native

    ```json
    {
      "id": "36f9e851-d713-4b50-8f8d-8a9382f138ca",
      "thid": "36f9e851-d713-4b50-8f8d-8a9382f138ca",
      "typ": "application/iden3comm-plain-json",
      "type": "https://iden3-communication.io/credentials/0.1/payment",
      "body": {
         "payments": [
              {
               "nonce":"123",
               "type":"Iden3PaymentRailsV1",
               "@context": "https://schema.iden3.io/core/jsonld/payment.jsonld",
                "paymentData": { 
                   "txId": "0x123",
                   "chainId": "123"
                }
             }
          ]
      },
      "to": "did:polygonid:polygon:mumbai:2qJUZDSCFtpR8QvHyBC4eFm6ab9sJo5rqPbcaeyGC4",
      "from": "did:iden3:polygon:mumbai:x3HstHLj2rTp6HHXk2WczYP7w3rpCsRbwCMeaQ2H2"
    }

    ```

??? erc20

    ```json
    {
      "id": "36f9e851-d713-4b50-8f8d-8a9382f138ca",
      "thid": "36f9e851-d713-4b50-8f8d-8a9382f138ca",
      "typ": "application/iden3comm-plain-json",
      "type": "https://iden3-communication.io/credentials/0.1/payment",
      "body": {
         "payments": [
              {
               "nonce":"123",
               "type":"Iden3PaymentRailsERC20V1",
               "@context": "https://schema.iden3.io/core/jsonld/payment.jsonld",
                "paymentData": { 
                   "txId": "0x123",
                   "chainId": "123",
                   "tokenAddress": "0x123" 
                }
             }
          ]
      },
      "to": "did:polygonid:polygon:mumbai:2qJUZDSCFtpR8QvHyBC4eFm6ab9sJo5rqPbcaeyGC4",
      "from": "did:iden3:polygon:mumbai:x3HstHLj2rTp6HHXk2WczYP7w3rpCsRbwCMeaQ2H2"
    }

    ```
