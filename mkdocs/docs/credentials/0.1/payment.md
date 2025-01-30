
type: `/credentials/0.1/payment`

General payment message from user.

```json
{
  "goal_code": "iden3comm.credentials.v1-1.proposal-request",
  "payments": [
    {
      "@context": "https://schema.iden3.io/core/jsonld/payment.jsonld",
      "type": "Iden3PaymentCryptoV1 | Iden3PaymentRailsV1 | Iden3PaymentRailsERC20V1 | Iden3PaymentPermitV1 | Iden3PaymentPermitERC20V1",
      ...
    }
  ]
}
```

Payment message itself defines fields: _payments_ </br>
Payment object itself is also typed.
The possible types for payment object are: _Iden3PaymentCryptoV1_ , _Iden3PaymentRailsV1_ , _Iden3PaymentRailsERC20V1_ , _Iden3PaymentPermitV1_ , _Iden3PaymentPermitERC20V1_. </br>
Corresponding ld context for such types: [https://schema.iden3.io/core/jsonld/payment.jsonld](https://schema.iden3.io/core/jsonld/payment.jsonld)



| Field            | Description                                        | Type   | Required |
|------------------|----------------------------------------------------|--------|----------|
| goal_code        | Goal code when the payment information can be used | string | ❌        |
| payments         | List of  payment requests                          | list   | ✅        |
| payments[i].type | Payment Type                                       | string | ✅        |



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

_Iden3PaymentPermitV1_ is a representation of payment permit that is meant to be sent by verifier to issuer through the user as an attachment to authorization request.
Although it can be sent as a separate message with a specifying of paymentReference.
Type field specification:

| Field                              | Description                                                                                                                  | Type                           | Required |
|------------------------------------|------------------------------------------------------------------------------------------------------------------------------|--------------------------------|----------|
| type                               | Payment Type                                                                                                                 | "Iden3PaymentPermitV1"         | ✅        |
| @context                           | ld context of payment type                                                                                                   | string                         | ✅        |
| paymentData.credentials            | credentials for which payment has been made                                                                                  | object                         | ✅        |
| paymentData.credentials[i].type    | type of prepaid credentials                                                                                                  | string                         | ✅        |
| paymentData.credentials[i].context | ld context of prepaid credential                                                                                             | string                         | ✅        |
| paymentData.nonce                  | Payment unique nonce for the issuer                                                                                          | string  (non negative integer) | ✅        |
| paymentData.recipient              | withdrawal address of the issuer                                                                                             | string                         | ✅        |
| paymentData.tokenAddress           | address of the token contract                                                                                                | string                         | ✅        |
| paymentData.amount                 | Specify amounts in the smallest unit of the currency or token (e.g., WEI for ETH or the smallest decimal for ERC-20 tokens). | string (non negative integer)  | ✅        |
| paymentData.expirationDate         | expiration of specific payment permit                                                                                        | string (ISO format)            | ✅        |
| paymentData.proof                  | w3c security proof                                                                                                           | object[] or object             | ✅        |
| paymentData.metadata               | any additional payment permit metadata                                                                                       | string (hex)                   | ✅        |

EIP712 domains for payment permit proof are defined [Iden3PaymentPermitV1](https://github.com/iden3/claim-schema-vocab/blob/main/core/json/Iden3PaymentPermitV1.json), where `verifyingContract` is address of contract that accepts permits, name is `SponsorPayment` and version is ` 1.0.0`.  <br />

_Iden3PaymentPermitERC20V1_ is a representation of payment permit in erc 20 token that is meant to be sent by verifier to issuer through the user as an attachment to authorization request.
Although it can be sent as a separate message with a specifying of paymentReference.
Type field specification:

| Field                              | Description                                                                                                                  | Type                           | Required |
|------------------------------------|------------------------------------------------------------------------------------------------------------------------------|--------------------------------|----------|
| type                               | Payment Type                                                                                                                 | "Iden3PaymentPermitV1"         | ✅        |
| @context                           | ld context of payment type                                                                                                   | string                         | ✅        |
| paymentData.credentials            | credentials for which payment has been made                                                                                  | object                         | ✅        |
| paymentData.credentials[i].type    | type of prepaid credentials                                                                                                  | string                         | ✅        |
| paymentData.credentials[i].context | ld context of prepaid credential                                                                                             | string                         | ✅        |
| paymentData.nonce                  | Payment unique nonce for the issuer                                                                                          | string  (non negative integer) | ✅        |
| paymentData.recipient              | withdrawal address of the issuer                                                                                             | string                         | ✅        |
| paymentData.amount                 | Specify amounts in the smallest unit of the currency or token (e.g., WEI for ETH or the smallest decimal for ERC-20 tokens). | string (non negative integer)  | ✅        |
| paymentData.expirationDate         | expiration of specific payment permit                                                                                        | string (ISO format)            | ✅        |
| paymentData.proof                  | w3c security proof                                                                                                           | object[] or object             | ✅        |
| paymentData.metadata               | any additional payment permit metadata                                                                                       | string (hex)                   | ✅        |


EIP712 domains for payment permit proof are defined [Iden3PaymentPermitERC20V1](https://github.com/iden3/claim-schema-vocab/blob/main/core/json/Iden3PaymentPermitERC20V1.json), where `verifyingContract` is address of contract that accepts permits, name is `SponsorPayment` and version is ` 1.0.0`.  <br />


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

??? payment permit erc20


    ```json
    {
      "id": "36f9e851-d713-4b50-8f8d-8a9382f138ca",
      "thid": "36f9e851-d713-4b50-8f8d-8a9382f138ca",
      "typ": "application/iden3comm-plain-json",
      "type": "https://iden3-communication.io/credentials/0.1/payment",
      "body": {
        "goal_code": "iden3comm.credentials.v1-1.proposal-request",
        "payments": [
          {
            "nonce": "3008",
            "type": "Iden3PaymentPermitERC20V1",
            "@context": "https://schema.iden3.io/core/jsonld/payment.jsonld",
            "paymentData": {
              "credentials": [
                {
                  "type": "LivenessProof",
                  "context": "http://example.com"
                }
              ],
              "tokenAddress": "0x2FE40749812FAC39a0F380649eF59E01bccf3a1A",
              "recipient": "0xE9D7fCDf32dF4772A7EF7C24c76aB40E4A42274a",
              "amount": "40",
              "expirationDate": "2024-10-28T16:02:36.816Z",
              "metadata": "0x",
              "paymentReference": "did:iden3:polygon:amoy:xACpATtbyUyWBAnhaqrmEVhE84k14ACBHcNQnjAQK",
              "proof": [
                {
                  "type": "EthereumEip712Signature2021",
                  "proofPurpose": "assertionMethod",
                  "proofValue": "0xc3d9d6fa9aa7af03863943f7568ce61303e84221e3e29277309fd42581742024402802816cca5542620c19895331f4bdc1ea6fed0d0c6a1cf8656556d3acfde61b",
                  "verificationMethod": "did:pkh:eip155:80002:0xE9D7fCDf32dF4772A7EF7C24c76aB40E4A42274a#blockchainAccountId",
                  "created": "2024-10-28T15:02:36.946Z",
                  "eip712": {
                    "types": "https://schema.iden3.io/core/json/Iden3PaymentPermitERC20V1.json",
                    "primaryType": "Iden3PaymentPermitERC20V1",
                    "domain": {
                      "name": "SponsorPayment",
                      "version": "1.0.0",
                      "chainId": "80002",
                      "verifyingContract": "0x6f742EBA99C3043663f995a7f566e9F012C07925"
                    }
                  }
                }
              ]
            }
          }
        ]
      },
      "to": "did:polygonid:polygon:mumbai:2qJUZDSCFtpR8QvHyBC4eFm6ab9sJo5rqPbcaeyGC4",
      "from": "did:iden3:polygon:mumbai:x3HstHLj2rTp6HHXk2WczYP7w3rpCsRbwCMeaQ2H2"
    }
    ```

