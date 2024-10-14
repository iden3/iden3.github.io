
type: `/credentials/0.1/payment-request`

General request format for payment from user.

```json
{
  "agent": "<issuer-agent-url>",
  "payments": [
    {
      "credentials": [
        {
          "type": "AML",
          "context": "<context-url>"
        }
      ],
      "data":[{
        "@context": "https://schema.iden3.io/core/jsonld/payment.jsonld",
        "type":"Iden3PaymentRequestCryptoV1 | Iden3PaymentRailsRequestV1",
        ...
      }],
      "description":"you can pass the verification on our KYC provider by following the next link",
    }
  ]
}
```

Payment Request itself defines fields: _agent_, _payments_,   _description_, _type_, _credentials_ and _data_. </br>
Payment Data itself is also typed. 
The possible types for data are: _Iden3PaymentRequestCryptoV1_ and _Iden3PaymentRailsRequestV1_; </br>
Corresponding ld context for such types: [https://schema.iden3.io/core/jsonld/payment.jsonld]( **https://schema.iden3.io/core/jsonld/payment.jsonld)



| Field                           | Description                                 | Type                       | Required |
|---------------------------------|---------------------------------------------|----------------------------|---------|
| agent                           | Issuer URL to send payment response         | string                     | ✅       |
| payments                        | List of  payment requests                   | list                       | ✅       |
| payments[i].type                | Type of payment request (old version only)  | string                     | ❌       |
| payments[i].credentials         | List of  credentials that user requests for | list                       | ✅       |
| payments[i].description         | description of payment                      | string                     | ✅       |
| payments[i].credentials.context | JSON-LD context url for credential          | string                     | ✅       |
| payments[i].credentials.type    | Type in the given JSON-LD context           | string                     | ✅       |
| payments[i].data                | Payment request specific details            | object or array of objects | ✅       |


_Iden3PaymentRequestCryptoV1_ is a simple representation of payment request for only one chain.
Type field specification: 

| Field          | Description                                | Type                          | Required                               |
|----------------|--------------------------------------------|-------------------------------|----------------------------------------|
| id             | Payment id                                 | string                        | ✅                                      |
| type           | Payment Type                               | string                        | ✅                                      |
| @context       | context for ld type                        | string                        | ❌ (historical backward compatibility)  |
| chainId        | Payment id                                 | string                        | ✅                                      |
| address        | smart-contract address that collects funds | string                        | ✅                                      |
| amount         | Payment amount                             | string                        | ✅                                      |
| currency       | chosen currency                            | string (non negative integer) | ✅                                      |
| expirationDate | expiration of specific payment request     | string (unix timestamp)       | ❌ (historical backward compatibility)  |


_Iden3PaymentRailsRequestV1_ is a representation of payment data that can be used for setting request to multiple chains.
Type field specification:

| Field          | Description                            | Type                            | Required |
|----------------|----------------------------------------|---------------------------------|----------|
| nonce          | Payment unique nonce for the issuer    | string  (non negative integer)  | ✅        |
| type           | Payment Type                           | string                          | ✅        |
| @context       | context for ld type                    | string                          | ✅        |
| recipient      | withdrawal address of the issuer       | string                          | ✅        |
| amount         | Payment amount                         | string (non negative integer)   | ✅        |
| expirationDate | expiration of specific payment request | string (unix timestamp)         | ✅        |
| proof          | w3c security proof                     | object[] or object              | ✅        |
| metadata       | any additional request metadata        | string (hex)                    | ✅        |
| currency       | chosen currency                        | string (ETHWEI / ETH / ETHGWEI) | ✅        |


For now only support proof type is [EIP 712 signature suite](https://w3c-ccg.github.io/ethereum-eip712-signature-2021-spec/). <br />
EIP712 domains are defined [here](https://github.com/iden3/claim-schema-vocab/blob/main/core/json/Iden3PaymentRailsRequestV1.json), where `verifyingContract` is address of contract that accepts payments, name is `MCPayment` and version is ` 1.0.0`.
```json{
  "EIP712Domain": [
    {
      "name": "name",
      "type": "string"
    },
    {
      "name": "version",
      "type": "string"
    },
    {
      "name": "chainId",
      "type": "uint256"
    },
    {
      "name":  "verifyingContract",
      "type:": "address"
    }
  ],
  "Iden3PaymentRailsRequestV1": [
    {
      "name": "recipient",
      "type": "address"
    },
    {
      "name": "amount",
      "type": "uint256"
    },
    {
      "name": "expirationDate",
      "type": "uint256"
    },
    {
      "name": "nonce",
      "type": "uint256"
    },
    {
      "name": "metadata",
      "type": "bytes"
    }
  ]
}
```



- **Example of credential payment request with Iden3PaymentRequestCryptoV1 payment data type:**

    ```json
    {
      "id": "36f9e851-d713-4b50-8f8d-8a9382f138ca",
      "thid": "36f9e851-d713-4b50-8f8d-8a9382f138ca",
      "typ": "application/iden3comm-plain-json",
      "type": "https://iden3-communication.io/credentials/0.1/payment-request",
      "body": {
         "agent": "<issuer-agent-url>", 
         "payments": [
          {
             "credentials": [
              {
               "type": "AML",
               "context": "<context_url>"
              }
             ],
             "data": [{
                 "type":"Iden3PaymentRequestCryptoV1",
                 "amount":"10", 
                 "id": "ox",
                 "chainId": "80002", 
                 "address": "0xpay1",
                 "currency": "ETH",
                 "expiration": "<timestamp>"
             }],
            "description":"you can pass the verification on our KYC provider by following the next link",
            }
          ]
      },
      "to": "did:polygonid:polygon:mumbai:2qJUZDSCFtpR8QvHyBC4eFm6ab9sJo5rqPbcaeyGC4",
      "from": "did:iden3:polygon:mumbai:x3HstHLj2rTp6HHXk2WczYP7w3rpCsRbwCMeaQ2H2"
    }

    ```

- **Example of credential payment request with Iden3PaymentRequestCryptoV1 payment data type:**

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
        "data": [
          {
            "@context": [
              "https://schema.iden3.io/core/jsonld/payment.jsonld#Iden3PaymentRailsRequestV1",
              "https://w3id.org/security/suites/eip712sig-2021/v1"
            ],
            "type": "Iden3PaymentRailsRequestV1",
            "recipient": "0xaddress",
            "amount": "100",
            "currency": "ETHWEI",
            "expirationDate": "ISO string",
            "nonce": "25",
            "metadata": "0x",
            "proof": [
              {
                "type": "EthereumEip712Signature2021",
                "proofPurpose": "assertionMethod",
                "proofValue": "0xa05292e9874240c5c2bbdf5a8fefff870c9fc801bde823189fc013d8ce39c7e5431bf0585f01c7e191ea7bbb7110a22e018d7f3ea0ed81a5f6a3b7b828f70f2d1c",
                "verificationMethod": "did:pkh:eip155:0:0x3e1cFE1b83E7C1CdB0c9558236c1f6C7B203C34e#blockchainAccountId",
                "created": "2024-09-26T12:28:19.702580067Z",
                "eip712": {
                  "types": "https://schema.iden3.io/core/json/Iden3PaymentRailsRequestV1.json",
                  "primaryType": "Iden3PaymentRailsRequestV1",
                  "domain": {
                    "name": "MCPayment",
                    "version": "1.0.0",
                    "chainId": "0x0",
                    "verifyingContract": "0x0000000000000000000000000000000000000000",
                    "salt": ""
                  }
                }
              }
            ]
          }
        ],
        "description": "you can pass the verification on our KYC provider by following the next link"
      }
    ]
  },
  "to": "did:polygonid:polygon:mumbai:2qJUZDSCFtpR8QvHyBC4eFm6ab9sJo5rqPbcaeyGC4",
  "from": "did:iden3:polygon:mumbai:x3HstHLj2rTp6HHXk2WczYP7w3rpCsRbwCMeaQ2H2"
}
```


- **Example of credential payment request with multiple Iden3PaymentRailsRequestV1 payment data type:**

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
        "data": [
          {
            "@context": [
              "https://schema.iden3.io/core/jsonld/payment.jsonld#Iden3PaymentRailsRequestV1",
              "https://w3id.org/security/suites/eip712sig-2021/v1"
            ],
            "type": "Iden3PaymentRailsRequestV1",
            "recipient": "0xaddress",
            "amount": "100",
            "currency": "ETHWEI",
            "expirationDate": "ISO string",
            "nonce": "25",
            "metadata": "0x",
            "proof": [
              {
                "type": "EthereumEip712Signature2021",
                "proofPurpose": "assertionMethod",
                "proofValue": "0xa05292e9874240c5c2bbdf5a8fefff870c9fc801bde823189fc013d8ce39c7e5431bf0585f01c7e191ea7bbb7110a22e018d7f3ea0ed81a5f6a3b7b828f70f2d1c",
                "verificationMethod": "did:pkh:eip155:0:0x3e1cFE1b83E7C1CdB0c9558236c1f6C7B203C34e#blockchainAccountId",
                "created": "2024-09-26T12:28:19.702580067Z",
                "eip712": {
                  "types": "https://schema.iden3.io/core/json/Iden3PaymentRailsRequestV1.json",
                  "primaryType": "Iden3PaymentRailsRequestV1",
                  "domain": {
                    "name": "MCPayment",
                    "version": "1.0.0",
                    "chainId": "0x0",
                    "verifyingContract": "0x0000000000000000000000000000000000000000",
                    "salt": ""
                  }
                }
              }
            ]
          },
          {
            "@context": [
              "https://schema.iden3.io/core/jsonld/payment.jsonld#Iden3PaymentRailsRequestV1",
              "https://w3id.org/security/suites/eip712sig-2021/v1"
            ],
            "type": "Iden3PaymentRailsRequestV1",
            "recipient": "0xaddress2",
            "amount": "200",
            "currency": "ETHWEI",
            "expirationDate": "ISO string",
            "nonce": "25",
            "metadata": "0x",
            "proof": [
              {
                "type": "EthereumEip712Signature2021",
                "proofPurpose": "assertionMethod",
                "proofValue": "0xa05292e9874240c5c2bbdf5a8fefff870c9fc801bde823189fc013d8ce39c7e5431bf0585f01c7e191ea7bbb7110a22e018d7f3ea0ed81a5f6a3b7b828f70f2d1c",
                "verificationMethod": "did:pkh:eip155:0:0x3e1cFE1b83E7C1CdB0c9558236c1f6C7B203C34e#blockchainAccountId",
                "created": "2024-09-26T12:28:19.702580067Z",
                "eip712": {
                  "types": "https://schema.iden3.io/core/json/Iden3PaymentRailsRequestV1.json",
                  "primaryType": "Iden3PaymentRailsRequestV1",
                  "domain": {
                    "name": "MCPayment",
                    "version": "1.0.0",
                    "chainId": "0x1",
                    "verifyingContract": "0x0000000000000000000000000000000000000002",
                    "salt": ""
                  }
                }
              }
            ]
          }
        ],
        "description": "you can pass the verification on our KYC provider by following the next link"
      }
    ]
  },
  "to": "did:polygonid:polygon:mumbai:2qJUZDSCFtpR8QvHyBC4eFm6ab9sJo5rqPbcaeyGC4",
  "from": "did:iden3:polygon:mumbai:x3HstHLj2rTp6HHXk2WczYP7w3rpCsRbwCMeaQ2H2"
}
```
