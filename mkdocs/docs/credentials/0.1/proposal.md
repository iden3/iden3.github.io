
type: `/credentials/1.0/proposal`

Proposals message represents set of instructions how to obtain a Verifiable Credential of certain type

```json
{
  "proposals": [
    {
      "credentials": [
        {
          "type": "LivenessProof",
          "context": "<context_url>"
        },
        {
          "type": "KYC",
          "context": "<context_url>"
        }
      ],
      "type": "WebVerificationForm",
      "url": "https://<issuer-agent-url>/verify?anyUniqueIdentifierOfSession=55",
      "expiration": "timestamp",
      "description":"you can pass the verification on our KYC provider by following the next link",
    }
  ]
}
```

| Field                      | Description                                   | Type   | Required |
|----------------------------|-----------------------------------------------|--------|----------|
| proposals                  | List of proposals that issuer offers to user   | list   |    ✅    |
| proposals[i].url           | URL to HTML verification form                  | string |    ✅    |
| proposals[i].credentials   | List of credentials that user requests for     | list   |    ✅    |
| proposals[i].credentials[j].type   | Type of VC                                   | string |    ✅    |
| proposals[i].credentials[j].context| JSON-LD of VC                                | string |    ✅    |
| proposals[i].type          | Type of proposal object                        | string |    ✅    |
| proposals[i].expiration    | Expiration timestamp                          | timestamp as string | ❌ |	
| proposals[i].description   | Description of the proposal                    | string | ❌ |	


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
                 "context": "<context_url>"
                },
                {
                 "type": "KYC",
                 "context": "<context_url>"
                }
               ],
           "type": "WebVerificationForm",
           "url": "https://<issuer-agent-url>/verify?anyUniqueIdentifierOfSession=55",
           "expiration": "timestamp",
           "description":"you can pass the verification on our KYC provider by following the next link",
         }
       ]
    },
    "to": "did:polygonid:polygon:mumbai:2qJUZDSCFtpR8QvHyBC4eFm6ab9sJo5rqPbcaeyGC4",
    "from": "did:iden3:polygon:mumbai:x3HstHLj2rTp6HHXk2WczYP7w3rpCsRbwCMeaQ2H2"
  }
```
