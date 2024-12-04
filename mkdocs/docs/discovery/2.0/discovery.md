

type: `https://didcomm.org/discover-features/2.0/queries`

Message to discover supported features by agent. This message follows the DIDComm protocol. 

```json
{
  "type": "https://didcomm.org/discover-features/2.0/queries",
  "id": "6f269888-0f93-4012-9f9d-e1da9896f261",
  "body": {
    "queries": [
      { "feature-type": "accept" }
    ]
  }
}
```

| Field         | Description      | Type   | Required |
|---------------|------------------|--------|----------|
| queries       | List of queries  | string | ✅        |

- **Example of report problem message:**
    
```json
    {
        "id": "6f269888-0f93-4012-9f9d-e1da9896f261",
        "thid": "6f269888-0f93-4012-9f9d-e1da9896f261",
        "typ": "application/iden3comm-plain-json",
        "type": "https://didcomm.org/discover-features/2.0/queries",
        "body": {
          "queries": [
            { "feature-type": "accept" }
          ]
        },
        "from": "did:polygonid:polygon:amoy:2qaPod1Qxo9UKTzR7K3Yo63gNRFHBm98bh1k1SEY6x",
        "to": "did:polygonid:polygon:mumbai:2qFroxB5kwgCxgVrNGUM6EW3khJgCdHHnKTr3VnTcp"
    }
```

Now only one feature that is accepted as a query param is `accept`.
Example of response

```json
{
    "id": "6f269888-0f93-4012-9f9d-e1da9896f262",
    "thid": "6f269888-0f93-4012-9f9d-e1da9896f261",
    "type": "https://didcomm.org/discover-features/2.0/disclose",
    "body":{
        "disclosures": [
            {
                "feature-type": "accept",
                "accept": [
                  "iden3comm/v1;env=application/iden3-zkp-json;circuitId=authV2;alg=groth16"
                ]
            }
        ]
    },
  "to": "did:polygonid:polygon:amoy:2qaPod1Qxo9UKTzR7K3Yo63gNRFHBm98bh1k1SEY6x",
  "from": "did:polygonid:polygon:mumbai:2qFroxB5kwgCxgVrNGUM6EW3khJgCdHHnKTr3VnTcp"
}
```

See possible accept profiles [here](../../media-types/overview.md)
