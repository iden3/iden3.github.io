
type: `/credentials/0.1/proposal-request`

Request for proposal is created by user and sent to issuer to receive instructions how to obtain a Verifiable Credential of certain type
```json
{
  "credentials": [
    {
      "type": "<vc_type>",
      "context": "<vc_ld_context>"
    }
  ],
  "metadata": {
    "type": "TransactionInfo",
    "data": "json1"
  },
  "did_doc": {
    "@context": [
      "..."
    ],
    "id": "did:iden3:polygon:mumbai:x3HstHLj2rTp6HHXk2WczYP7w3rpCsRbwCMeaQ2H2",
    "services": []
  }
}
```

| Field                  | Description                                               | Type   | Required  |
|------------------------|-----------------------------------------------------------|--------|-----------|
| metadata               | Type specific metadata regarding current proposal request | object | ❌        |
| did_doc                | User did document                                         | JSON   | ❌        |
| credentials            | List of  credentials that user requests for               | list   | ✅        |
| credentials[i].type    | type of VC                                                | string | ✅        |
| credentials[i].context | JSON-LD of VC                                             | string | ✅        |

- **Example of credential proposal request:**

```json
    {
      "id": "36f9e851-d713-4b50-8f8d-8a9382f138ca",
      "thid": "36f9e851-d713-4b50-8f8d-8a9382f138ca",
      "typ": "application/iden3comm-plain-json",
      "type": "https://iden3-communication.io/credentials/0.1/proposal-request",
      "body": {
        "credentials": [
          {
            "type": "LivenessProof",
            "context": "context_url"
          },
          {
            "type": "KYC",
            "context": "<context_url>"
          }
        ],
        "metadata": {
          "type": "TransactionInfo",
          "data": "json1"
        },
        "did_doc": {
          "@context": [
            "..."
          ],
          "id": "did:iden3:polygon:mumbai:x3HstHLj2rTp6HHXk2WczYP7w3rpCsRbwCMeaQ2H2",
          "services": [
            {
              "id": "did:iden3:polygon:mumbai:x3HstHLj2rTp6HHXk2WczYP7w3rpCsRbwCMeaQ2H2/mobile",
              "type": "Iden3Mobile"
            },
            {
              "id": "did:iden3:polygon:mumbai:x3HstHLj2rTp6HHXk2WczYP7w3rpCsRbwCMeaQ2H2/push",
              "type": "PushNotificationService"
            }
          ]
        }
      },
      "to": "did:polygonid:polygon:mumbai:2qJUZDSCFtpR8QvHyBC4eFm6ab9sJo5rqPbcaeyGC4",
      "from": "did:iden3:polygon:mumbai:x3HstHLj2rTp6HHXk2WczYP7w3rpCsRbwCMeaQ2H2"
    } 
```
