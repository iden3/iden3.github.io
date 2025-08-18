
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
        "type":"Iden3PaymentRequestCryptoV1 | Iden3PaymentRailsRequestV1 | Iden3PaymentRailsERC20RequestV1",
        ...
      }],
      "description":"you can pass the verification on our KYC provider by following the next link",
    }
  ]
}
```

Payment Request itself defines fields: _agent_, _payments_,   _description_, _type_, _credentials_ and _data_. </br>
Payment Data itself is also typed. 
The possible types for data are: _Iden3PaymentRequestCryptoV1_, _Iden3PaymentRailsRequestV1_, _Iden3PaymentRailsERC20RequestV1_, _Iden3PaymentRailsSolanaRequestV1_, _Iden3PaymentRailsSolanaSPLRequestV1_; </br>
Corresponding ld context for such types: [https://schema.iden3.io/core/jsonld/payment.jsonld](https://schema.iden3.io/core/jsonld/payment.jsonld)



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

| Field          | Description                                | Type                           | Required                               |
|----------------|--------------------------------------------|--------------------------------|----------------------------------------|
| id             | Payment id                                 | string                         | ✅                                      |
| type           | Payment Type                               | "Iden3PaymentRequestCryptoV1"  | ✅                                      |
| @context       | context for ld type                        | string                         | ❌ (historical backward compatibility)  |
| chainId        | chain id                                   | string                         | ✅                                      |
| address        | smart-contract address that collects funds | string                         | ✅                                      |
| amount         | Payment amount                             | string                         | ✅                                      |
| currency       | chosen currency                            | string (non negative integer)  | ✅                                      |
| expiration     | expiration of specific payment request     | string (ISO format)            | ❌ (historical backward compatibility)  |


_Iden3PaymentRailsRequestV1_ is a representation of payment data that can be used for setting request to multiple chains to pay only in native currency.
Type field specification:

| Field          | Description                            | Type                              | Required |
|----------------|----------------------------------------|-----------------------------------|----------|
| nonce          | Payment unique nonce for the issuer    | string  (non negative integer)    | ✅        |
| type           | Payment Type                           | "Iden3PaymentRailsRequestV1"      | ✅        |
| @context       | context for ld type                    | string                            | ✅        |
| recipient      | withdrawal address of the issuer       | string                            | ✅        |
| amount         |Specify amounts in the smallest unit of the currency or token (e.g., WEI for ETH or the smallest decimal for ERC-20 tokens).| string (non negative integer)                                    | ✅        |
| expirationDate | expiration of specific payment request | string (ISO format)               | ✅        |
| proof          | w3c security proof                     | object[] or object                | ✅        |
| metadata       | any additional request metadata        | string (hex)                      | ✅        |


For now only support proof type is [EIP 712 signature suite](https://w3c-ccg.github.io/ethereum-eip712-signature-2021-spec/). <br />
EIP712 domains are defined [here](https://github.com/iden3/claim-schema-vocab/blob/main/core/json/Iden3PaymentRailsRequestV1.json), where `verifyingContract` is address of contract that accepts payments, name is `MCPayment` and version is ` 1.0.0`.  <br />

??? EIP712
    ```json
        {
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

_Iden3PaymentRailsERC20RequestV1_ is a representation of payment data that can be used for setting request to multiple chains to pay only in ERC20 tokens.
It has the same ideology with _Iden3PaymentRailsRequestV1_, but also it defines two additional fields: `tokenAddress` and `features`.
Token address can be the address of any ERC20 token. Current recommended flow for client is to call function 'approve' on token contract and then _payERC20_ on payment contract, so it will send funds to recipient address. Features field can contain a list of EIPs that contract support. Now, on the client level only supported feature is Permit [EIP-2612](https://eips.ethereum.org/EIPS/eip-2612). In this case iw will be two calls to signer client but only one transaction to invoke the `payERC20Permit` function. 

Type field specification:

| Field          | Description                                                          | Type                            | Required |
|----------------|----------------------------------------------------------------------|---------------------------------|----------|
| nonce          | Payment unique nonce for the issuer                                  | string  (non negative integer)  | ✅        |
| type           | Payment Type                                                         | "Iden3PaymentRailsERC20RequestV1"    | ✅        |
| @context       | context for ld type                                                  | string                          | ✅        |
| recipient      | withdrawal address of the issuer                                     | string                          | ✅        |
| tokenAddress   | address of the token contract                                        | string                          | ✅        |
| features       | list of features supported by token contract( now only ["EIP-2612"]) | string[]                        | ❌        |
| amount         |Specify amounts in the smallest unit of the currency or token (e.g., WEI for ETH or the smallest decimal for ERC-20 tokens).| string (non negative integer)   | ✅        |
| expirationDate | expiration of specific payment request                               | string (ISO format)             | ✅        |
| proof          | w3c security proof                                                   | object[] or object              | ✅        |
| metadata       | any additional request metadata                                      | string (hex)                    | ✅        |


EIP712 domains for proof creation are defined [here](https://github.com/iden3/claim-schema-vocab/blob/main/core/json/Iden3PaymentRailsERC20RequestV1.json), where `verifyingContract` is address of contract that accepts payments, name is `MCPayment` and version is ` 1.0.0`.  <br />

??? EIP712
    ```json
        {
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
          "Iden3PaymentRailsRequestERC20V1": [ 
            {
              "name": "tokenAddress",
              "type": "address"
            },
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
  
_Iden3PaymentRailsSolanaRequestV1_ is a representation of payment data that can be used for setting request to Solana chain to pay only in native currency.
Type field specification:

| Field          | Description                            | Type                              | Required |
|----------------|----------------------------------------|-----------------------------------|----------|
| nonce          | Payment unique nonce for the issuer    | string  (non negative integer)    | ✅        |
| type           | Payment Type                           | "Iden3PaymentRailsSolanaRequestV1"| ✅        |
| @context       | context for ld type                    | string                            | ✅        |
| recipient      | withdrawal address of the issuer       | string                            | ✅        |
| amount         | amounts in lamports.                   | string (non negative integer)     | ✅        |
| expirationDate | expiration of specific payment request | string (ISO format)               | ✅        |
| proof          | w3c security proof                     | object[] or object                | ✅        |
| metadata       | any additional request metadata        | string (hex)                      | ✅        |


For now only support proof type is [SolanaEd25519Signature2025](https://schema.iden3.io/core/jsonld/solanaEd25519.jsonld). <br />


_Iden3PaymentRailsSolanaSPLRequestV1_ is a representation of payment data that can be used for setting request to Solana chain to pay only in SPL tokens.
It has the same ideology with _Iden3PaymentRailsSolanaRequestV1_, but also it defines two additional fields: `tokenAddress` and `features`.
Token address can be the address of any SPL token. Currently, no feature is supported at the client level.

Type field specification:

| Field          | Description                                                          | Type                            | Required |
|----------------|----------------------------------------------------------------------|---------------------------------|----------|
| nonce          | Payment unique nonce for the issuer                                  | string  (non negative integer)  | ✅        |
| type           | Payment Type                                                         | "Iden3PaymentRailsSolanaSPLRequestV1"    | ✅        |
| @context       | context for ld type                                                  | string                          | ✅        |
| recipient      | withdrawal address of the issuer                                     | string                          | ✅        |
| tokenAddress   | address of the token contract                                        | string                          | ✅        |
| features       | list of features supported by token contract                         | string[]                        | ❌        |
| amount         | smallest decimal for SPL tokens.                                      |  string (non negative integer)   | ✅        |
| expirationDate | expiration of specific payment request                               | string (ISO format)             | ✅        |
| proof          | w3c security proof                                                   | object[] or object              | ✅        |
| metadata       | any additional request metadata                                      | string (hex)                    | ✅        |

For now only support proof type is [SolanaEd25519Signature2025](https://schema.iden3.io/core/jsonld/solanaEd25519.jsonld). <br />

**Examples of Iden3PaymentRequest with different data**

??? crypto
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

??? native
    ``` json
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

??? erc20 
    ```json
    {
      "id": "54782ed3-8d83-427b-856d-eac57a9aa94a",
      "thid": "54782ed3-8d83-427b-856d-eac57a9aa94a",
      "from": "did:iden3:polygon:amoy:xCRp75DgAdS63W65fmXHz6p9DwdonuRU9e46DifhX",
      "to": "did:iden3:polygon:amoy:x7Z95VkUuyo6mqraJw2VGwCfqTzdqhM1RVjRHzcpK",
      "typ": "application/iden3comm-plain-json",
      "type": "https://iden3-communication.io/credentials/0.1/payment-request",
      "body": {
        "agent": "",
        "payments": [
          {
            "data": [
              {
                "type": "Iden3PaymentRailsERC20RequestV1",
                "@context": [
                  "https://schema.iden3.io/core/jsonld/payment.jsonld#Iden3PaymentRailsERC20RequestV1",
                  "https://w3id.org/security/suites/eip712sig-2021/v1"
                ],
                "tokenAddress": "0x2FE40749812FAC39a0F380649eF59E01bccf3a1A",
                "recipient": "0xE9D7fCDf32dF4772A7EF7C24c76aB40E4A42274a",
                "amount": "40",
                "expirationDate": "2024-10-28T16:02:36.816Z",
                "nonce": "3008",
                "metadata": "0x",
                "proof": [
                  {
                    "type": "EthereumEip712Signature2021",
                    "proofPurpose": "assertionMethod",
                    "proofValue": "0xc3d9d6fa9aa7af03863943f7568ce61303e84221e3e29277309fd42581742024402802816cca5542620c19895331f4bdc1ea6fed0d0c6a1cf8656556d3acfde61b",
                    "verificationMethod": "did:pkh:eip155:80002:0xE9D7fCDf32dF4772A7EF7C24c76aB40E4A42274a#blockchainAccountId",
                    "created": "2024-10-28T15:02:36.946Z",
                    "eip712": {
                      "types": "https://schema.iden3.io/core/json/Iden3PaymentRailsRequestV1.json",
                      "primaryType": "Iden3PaymentRailsRequestV1",
                      "domain": {
                        "name": "MCPayment",
                        "version": "1.0.0",
                        "chainId": "80002",
                        "verifyingContract": "0x6f742EBA99C3043663f995a7f566e9F012C07925"
                      }
                    }
                  }
                ]
              }
            ],
            "credentials": [
              {
                "type": "AML",
                "context": "http://test.com"
              }
            ],
            "description": "Iden3PaymentRailsRequestV1 payment-request integration test"
          }
        ]
      }
    }
    ```

??? eip-2612
    ```json
    {
      "id": "54782ed3-8d83-427b-856d-eac57a9aa94a",
      "thid": "54782ed3-8d83-427b-856d-eac57a9aa94a",
      "from": "did:iden3:polygon:amoy:xCRp75DgAdS63W65fmXHz6p9DwdonuRU9e46DifhX",
      "to": "did:iden3:polygon:amoy:x7Z95VkUuyo6mqraJw2VGwCfqTzdqhM1RVjRHzcpK",
      "typ": "application/iden3comm-plain-json",
      "type": "https://iden3-communication.io/credentials/0.1/payment-request",
      "body": {
        "agent": "agent.example.com",
        "payments": [
          {
            "data": [
              {
                "type": "Iden3PaymentRailsERC20RequestV1",
                "@context": [
                  "https://schema.iden3.io/core/jsonld/payment.jsonld#Iden3PaymentRailsERC20RequestV1",
                  "https://w3id.org/security/suites/eip712sig-2021/v1"
                ],
                "tokenAddress": "0x2FE40749812FAC39a0F380649eF59E01bccf3a1A",
                "features": ["EIP-2612"],
                "recipient": "0xE9D7fCDf32dF4772A7EF7C24c76aB40E4A42274a",
                "amount": "40",
                "expirationDate": "2024-10-28T16:02:36.816Z",
                "nonce": "3008",
                "metadata": "0x",
                "proof": [
                  {
                    "type": "EthereumEip712Signature2021",
                    "proofPurpose": "assertionMethod",
                    "proofValue": "0xc3d9d6fa9aa7af03863943f7568ce61303e84221e3e29277309fd42581742024402802816cca5542620c19895331f4bdc1ea6fed0d0c6a1cf8656556d3acfde61b",
                    "verificationMethod": "did:pkh:eip155:80002:0xE9D7fCDf32dF4772A7EF7C24c76aB40E4A42274a#blockchainAccountId",
                    "created": "2024-10-28T15:02:36.946Z",
                    "eip712": {
                      "types": "https://schema.iden3.io/core/json/Iden3PaymentRailsRequestV1.json",
                      "primaryType": "Iden3PaymentRailsRequestV1",
                      "domain": {
                        "name": "MCPayment",
                        "version": "1.0.0",
                        "chainId": "80002",
                        "verifyingContract": "0x6f742EBA99C3043663f995a7f566e9F012C07925"
                      }
                    }
                  }
                ]
              }
            ],
            "credentials": [
              {
                "type": "AML",
                "context": "http://test.com"
              }
            ],
            "description": "Iden3PaymentRailsRequestV1 payment-request integration test"
          }
        ]
      }
    }
    ```

??? solana native 
    ```json
    {
		"id": "84523aa3-1b1b-4cde-9b18-6662d796a020",
		"thid": "84523aa3-1b1b-4cde-9b18-6662d796a020",
		"from": "did:iden3:polygon:amoy:x6x5sor7zpyZX9yNpm8h1rPBDSN9idaEhDj1Qm8Q9",
		"to": "did:iden3:polygon:amoy:x7Z95VkUuyo6mqraJw2VGwCfqTzdqhM1RVjRHzcpK",
		"typ": "application/iden3comm-plain-json",
		"type": "https://iden3-communication.io/credentials/0.1/payment-request",
		"body": {
		  "agent": "https://agent-url.com",
		  "payments": [
			{
			  "data": [
				{
				  "type": "Iden3PaymentRailsSolanaRequestV1",
				  "@context": [
					"https://schema.iden3.io/core/jsonld/payment.jsonld#Iden3PaymentRailsSolanaRequestV1",
					"https://schema.iden3.io/core/jsonld/solanaEd25519.jsonld"
				  ],
				  "recipient": "HcCoHQFPjU2brBFW1hAZvEtZx7nSrYCBJVq4vKsjo6jf",
				  "amount": "44000000",
				  "expirationDate": "2025-08-12T14:03:26.728Z",
				  "nonce": "31231231233",
				  "metadata": "0x",
				  "proof": [
					{
					  "type": "SolanaEd25519Signature2025",
					  "proofPurpose": "assertionMethod",
					  "proofValue": "024e6579f78669c7d456ea4b286d5c33ee85b2def2ee77a9287e1c79f0b757422df86ae5df5b9d892c9a97484fa9587349cd13ca9c8ff39f8a6e6042ca7e6107",
					  "created": "2025-08-12T13:03:26.762Z",
					  "verificationMethod": "did:pkh:solana:103:CTZbbbcSpZy4pxpFwhQGdf8u3hxPWKRh5ywRHuNzn2Aa",
					  "domain": {
						"version": "SolanaEd25519NativeV1",
						"chainId": "103",
						"verifyingContract": "Hys6CpX8McHbPBaPKbRYGVdXVxor1M5pSZUDMMwakGmM"
					  }
					}
				  ]
				}
			  ],
			  "credentials": [
				{
				  "type": "AML",
				  "context": "http://test.com"
				}
			  ],
			  "description": "Iden3PaymentRailsRequestSolanaV1 payment-request"
			}
		  ]
		},
		"created_time": 1755003806
	}
    ```

??? solana SPL 
    ```json
    {
		"id": "70574bc1-2472-4fa0-b7b1-b79a84376fab",
		"thid": "70574bc1-2472-4fa0-b7b1-b79a84376fab",
		"from": "did:iden3:polygon:amoy:x6x5sor7zpyZX9yNpm8h1rPBDSN9idaEhDj1Qm8Q9",
		"to": "did:iden3:polygon:amoy:x7Z95VkUuyo6mqraJw2VGwCfqTzdqhM1RVjRHzcpK",
		"typ": "application/iden3comm-plain-json",
		"type": "https://iden3-communication.io/credentials/0.1/payment-request",
		"body": {
		  "agent": "https://agent-url.com",
		  "payments": [
			{
			  "data": [
				{
				  "type": "Iden3PaymentRailsSolanaSPLRequestV1",
				  "@context": [
					"https://schema.iden3.io/core/jsonld/payment.jsonld#Iden3PaymentRailsSolanaSPLRequestV1",
					"https://schema.iden3.io/core/jsonld/solanaEd25519.jsonld"
				  ],
				  "recipient": "HcCoHQFPjU2brBFW1hAZvEtZx7nSrYCBJVq4vKsjo6jf",
				  "amount": "500000000",
				  "expirationDate": "2025-08-12T14:14:54.421Z",
				  "nonce": "11212312003",
				  "metadata": "0x",
				  "proof": [
					{
					  "type": "SolanaEd25519Signature2025",
					  "proofPurpose": "assertionMethod",
					  "proofValue": "378f2941ef5f87b85445b803405620f8e300a05b627e07f51edbf886610cddc4f1dbdbaf6fa1693d975953d1783cbf5dbe0f9e0b5708978eef1fec1e7964a90a",
					  "created": "2025-08-12T13:14:54.453Z",
					  "verificationMethod": "did:pkh:solana:103:CTZbbbcSpZy4pxpFwhQGdf8u3hxPWKRh5ywRHuNzn2Aa",
					  "domain": {
						"version": "SolanaEd25519SPLV1",
						"chainId": "103",
						"verifyingContract": "Hys6CpX8McHbPBaPKbRYGVdXVxor1M5pSZUDMMwakGmM"
					  }
					}
				  ],
				  "tokenAddress": "4MjRhSkDaXmgdAL9d9UM7kmgJrWYGJH66oocUN2f3VUp"
				}
			  ],
			  "credentials": [
				{
				  "type": "AML",
				  "context": "http://test.com"
				}
			  ],
			  "description": "Iden3PaymentRailsRequestSolanaSPLV1 payment-request integration test"
			}
		  ]
		},
		"created_time": 1755004494
	  }	
    ```



??? multiple 
    
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
                "type": "Iden3PaymentRailsERC20RequestV1",
                "@context": [
                  "https://schema.iden3.io/core/jsonld/payment.jsonld#Iden3PaymentRailsERC20RequestV1",
                  "https://w3id.org/security/suites/eip712sig-2021/v1"
                ],
                "tokenAddress": "0x2FE40749812FAC39a0F380649eF59E01bccf3a1A",
                "features": [
                  "EIP-2612"
                ],
                "recipient": "0xE9D7fCDf32dF4772A7EF7C24c76aB40E4A42274a",
                "amount": "40",
                "expirationDate": "2024-10-28T16:02:36.816Z",
                "nonce": "3008",
                "metadata": "0x",
                "proof": [
                  {
                    "type": "EthereumEip712Signature2021",
                    "proofPurpose": "assertionMethod",
                    "proofValue": "0xc3d9d6fa9aa7af03863943f7568ce61303e84221e3e29277309fd42581742024402802816cca5542620c19895331f4bdc1ea6fed0d0c6a1cf8656556d3acfde61b",
                    "verificationMethod": "did:pkh:eip155:80002:0xE9D7fCDf32dF4772A7EF7C24c76aB40E4A42274a#blockchainAccountId",
                    "created": "2024-10-28T15:02:36.946Z",
                    "eip712": {
                      "types": "https://schema.iden3.io/core/json/Iden3PaymentRailsRequestV1.json",
                      "primaryType": "Iden3PaymentRailsRequestV1",
                      "domain": {
                        "name": "MCPayment",
                        "version": "1.0.0",
                        "chainId": "80002",
                        "verifyingContract": "0x6f742EBA99C3043663f995a7f566e9F012C07925"
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
              },
              {
                "type": "Iden3PaymentRailsSolanaRequestV1",
                "@context": [
                "https://schema.iden3.io/core/jsonld/payment.jsonld#Iden3PaymentRailsSolanaRequestV1",
                "https://schema.iden3.io/core/jsonld/solanaEd25519.jsonld"
                ],
                "recipient": "HcCoHQFPjU2brBFW1hAZvEtZx7nSrYCBJVq4vKsjo6jf",
                "amount": "44000000",
                "expirationDate": "2025-08-12T14:03:26.728Z",
                "nonce": "31231231233",
                "metadata": "0x",
                "proof": [
                {
                  "type": "SolanaEd25519Signature2025",
                  "proofPurpose": "assertionMethod",
                  "proofValue": "024e6579f78669c7d456ea4b286d5c33ee85b2def2ee77a9287e1c79f0b757422df86ae5df5b9d892c9a97484fa9587349cd13ca9c8ff39f8a6e6042ca7e6107",
                  "created": "2025-08-12T13:03:26.762Z",
                  "verificationMethod": "did:pkh:solana:103:CTZbbbcSpZy4pxpFwhQGdf8u3hxPWKRh5ywRHuNzn2Aa",
                  "domain": {
                  "version": "SolanaEd25519NativeV1",
                  "chainId": "103",
                  "verifyingContract": "Hys6CpX8McHbPBaPKbRYGVdXVxor1M5pSZUDMMwakGmM"
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
