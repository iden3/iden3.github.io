
type: `/credentials/1.0/issuance-request`

Request for the issuance of a verifiable credential to a user.

```json
{
	"schema": "<schema_hash>",
	"data": "<verifiable_credential_content>",
	"expiration": "<expiration_time>"
}
```

| Field | Description | Type | Required |
| --- | --- | --- | --- |
| schema | The hash of the JSON schema employed in creating the content of the verifiable credential. | string | ✅ |
| data | JSON reprecendation of credential content  | JSON | ✅ |
| expiration | The time until which VC is considered valid | UNIX timestamp(int64) | ✅ |

- **Example of credential issuance request:**
    
    ```json
    {
      "id": "890d5eff-f931-482a-8c31-7540ef7bcffb",
      "thid": "890d5eff-f931-482a-8c31-7540ef7bcffb",
      "typ": "application/iden3comm-plain-json",
      "type": "https://iden3-communication.io/credentials/1.0/issuance-request",
      "body": {
        "data": {
          "birthday": 19960424,
          "documentType": 1
        },
        "expiration": 1660914469,
        "schema": {
          "type": "KYCAgeCredential",
          "url": "https://raw.githubusercontent.com/iden3/claim-schema-vocab/main/schemas/json/KYCAgeCredential-v3.json"
        }
      },
      "from": "did:polygonid:polygon:mumbai:2qFroxB5kwgCxgVrNGUM6EW3khJgCdHHnKTr3VnTcp",
      "to": "did:polygonid:polygon:mumbai:2qJG6RYgN1u6v7JAYSdfixSwktnZ7hMzd4t21SCdNu"
    }
    ```
