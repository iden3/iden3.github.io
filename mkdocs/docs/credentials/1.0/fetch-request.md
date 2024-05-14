
type: `/credentials/1.0/fetch-request`

Request for fetch an VC from an issuer.

```json
{
	"id": "<uuid_of_credential>"
}
```

| Field | Description | Type | Required |
| --- | --- | --- | --- |
| id | UUID of credential that will fetch | string | ✅ |

- **Example of credential fetch request:**
    
    ```json
    {
      "id": "1924af5a-7d63-4850-addf-0177cdc34786",
      "thid": "1924af5a-7d63-4850-addf-0177cdc34786",
      "typ": "application/iden3comm-plain-json",
      "type": "https://iden3-communication.io/credentials/1.0/fetch-request",
      "body": {
        "id": "af9293c5-3c91-40d7-b810-564ae693a578"
      },
      "from": "did:polygonid:polygon:mumbai:2qJG6RYgN1u6v7JAYSdfixSwktnZ7hMzd4t21SCdNu",
      "to": "did:polygonid:polygon:mumbai:2qFroxB5kwgCxgVrNGUM6EW3khJgCdHHnKTr3VnTcp"
    }
    ```
