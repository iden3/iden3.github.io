
type: `/credentials/1.0/proposal`

Proposals message represents set of instructions how to obtain a Verifiable Credential of certain type

```json
{
  "proposals": [
    {
      "credentials": [
        {
          "type": "LivenessProof",
          "context": "http://test.com"
        },
        {
          "type": "KYC",
          "context": "http://test.com"
        }
      ],
      "type": "WebVerificationForm",
      "url": "http://issuer-agent.com/verify?anyUniqueIdentifierOfSession=55",
      "expiration": "timestamp",
      "description":"you can pass the verification on our KYC provider by following the next link",
    }
  ]
}
```

| Field                    | Description                                   | Type   | Required |
|--------------------------|-----------------------------------------------|--------| --- |
| url                      | Issuer URL for fetch credential               | string | ✅ |
| proposals                | List of  proposals that issuer offers to user | list   | ✅        |
| proposals[i].credentials | List of  credentials that user requests for   | list   | ✅        |
| proposals[i]credentials.type        | type of VC                                    | string | ✅        |
| proposals[i]credentials.context     | JSON-LD of VC                                 | string | ✅        |
| proposals[i].type | type of proposal object                       | string | ✅        |


- **Example of credential proposal:**

```json
  {
    "id": "36f9e851-d713-4b50-8f8d-8a9382f138ca",
    "thid": "36f9e851-d713-4b50-8f8d-8a9382f138ca",
    "typ": "application/iden3comm-plain-json",
    "type": "https://iden3-communication.io/credentials/0.1/proposal",
    "body": {
       "proposals": [
         {
           "credentials": [
                {
                 "type": "LivenessProof",
                 "context": "http://test.com"
                },
                {
                 "type": "KYC",
                 "context": "http://test.com"
                }
               ],
           "type": "WebVerificationForm",
           "url": "http://issuer-agent.com/verify?anyUniqueIdentifierOfSession=55",
           "expiration": "timestamp",
           "description":"you can pass the verification on our KYC provider by following the next link",
         }
       ]
    },
    "to": "did:polygonid:polygon:mumbai:2qJUZDSCFtpR8QvHyBC4eFm6ab9sJo5rqPbcaeyGC4",
    "from": "did:iden3:polygon:mumbai:x3HstHLj2rTp6HHXk2WczYP7w3rpCsRbwCMeaQ2H2"
  }
```
