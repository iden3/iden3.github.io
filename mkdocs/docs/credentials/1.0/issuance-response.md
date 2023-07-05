
type: `/credentials/1.0/issuance-response`

Message contains [W3Credential](https://www.w3.org/TR/vc-data-model-2.0/) with iden3 proof inside.

```json
"credential": {
  "issuer": "<issuer_did>",
  "identifier": "<iden3_id>",
  "credential": {
    "id": "<credential_uuid>",
    "@context": ["<list_of_contexts>"],
    "@type": ["<credential_types>"],
    "expiration": "<expiration_time>",
    "updatable": "<is_updatable_credential>",
    "version": "<credential_version>",
    "rev_nonce": "<credential_revocation_nonce>",
    "credentialSubject": {"<credential_subject>"},
    "credentialSchema": {"<credential_schema>"},
    "credentialStatus": {"<credential_status>"},
    "proof": ["<list_of_proofs>"]
  }
}
```

| Field | Description | Type | Required |
| --- | --- | --- | --- |
| issuer | Issuer that issued the credential | string | ✅ |
| identifier | iden3 https://docs.iden3.io/protocol/claims-structure/ | string | ✅ |
| credentials.id | ID of VC | string | ✅ |
| credentials.@context | List of contexts | list of strings | ✅ |
| credentials.@type | Types of credential | list of strings | ✅ |
| credentials.expiration | The time until which VC is considered valid | string | ✅ |
| credentials.updatable | Flag that shows if is possible update the VC credential | boolean | ✅ |
| credentials.version | Version of the VC  | integer | ✅ |
| credentials.rev_nonce | Unique revocation ID of the VC | integer | ✅ |
| credentials.credentialSubject | Information about subject | *object | ✅ |
| credentials.credentialSchema | Information about JSON schema that was used for create the credentials.credentialSubject | object | ✅ |
| credentials.credentialStatus | Information about revocation the V | *object | ✅ |
| credentials.proof | List of proofs that the VC has | *list of object | ✅ |

Content of `credentials.credentialSubject` object depends of `credentials.credentialSchema`.

Allow content for `credentials.credentialStatus`:

1. [Information you can use to obtain revocation status directly from the issuer](https://github.com/iden3/claim-schema-vocab/blob/main/credentials/common-v2.md#credentialstatus).
2. [The information required to obtain an MTP proof from the RHS (RHS) regarding the revocation status of `credentials.rev_nonce`.](https://github.com/iden3/claim-schema-vocab/blob/main/proofs/Iden3ReverseSparseMerkleTreeProof.md)
3. IN PROCESS: onchain information about revocation.

- **Example of credential issuance:**
    
    ```json
    {
      "id": "1924af5a-7d63-4850-addf-0177cdc34786",
      "thid": "1924af5a-7d63-4850-addf-0177cdc34786",
      "typ": "application/iden3comm-plain-json",
      "type": "https://iden3-communication.io/credentials/1.0/issuance-response",
      "to": "119tqceWdRd2F6WnAyVuFQRFjK3WUXq2LorSPyG9LJ",
      "from": "114vgnnCupQMX4wqUBjg5kUya3zMXfPmKc9HNH4TSE",
      "body": {
        "credential": {
          "issuer": "1196RFa2m5Zui1N32JMhEo4V4TsRMPUTsdjWRceEMW",
          "identifier": "11BXYorwd5gw8PXKPJft25h4HKdoPSN96tTmwo1MzB",
          "credential": {
            "id": "812abf03-3f5c-49d9-956f-71046696c7cc",
            "@context": [
              "https://raw.githubusercontent.com/iden3/claim-schema-vocab/main/schemas/json-ld/iden3credential.json-ld",
              "https://raw.githubusercontent.com/iden3/claim-schema-vocab/main/schemas/json-ld/kyc.json-ld"
            ],
            "@type": [
              "Iden3Credential"
            ],
            "expiration": "2361-03-21T21:14:48+02:00",
            "updatable": false,
            "version": 0,
            "rev_nonce": 3093887425188630000,
            "credentialSubject": {
              "birthday": 19960424,
              "document_type": 1,
              "id": "11BXYorwd5gw8PXKPJft25h4HKdoPSN96tTmwo1MzB",
              "type": "KYCAgeCredential"
            },
            "credentialSchema": {
              "@id": "https://raw.githubusercontent.com/iden3/claim-schema-vocab/main/schemas/json/KYCAgeCredential.json",
              "type": "JsonSchemaValidator2018"
            },
            "credentialStatus": {
              "@id": "https://kyc-issuer.com/identities/1196RFa2m5Zui1N32JMhEo4V4TsRMPUTsdjWRceEMW/revocation/status/3093887425188629987",
              "type": "JsonSchemaValidator2018"
            },
            "proof": {
              "@type": "BJJSignature2021",
              "created": 1636990667,
              "issuer_mtp": {
                "@type": "Iden3SparseMerkleProof",
                "state": {
                  "claims_tree_root": "921fb387abe063e926bb56f906ce5406f30d14b49f6c8119b861c41422123012",
                  "value": "c04a7b86bbb247e2aba032a7ece7ad03aff1c933eb568db40a796a4a27861a13"
                },
                "mtp": {
                  "@type": "SparseMerkleProof",
                  "existence": true,
                  "siblings": []
                },
                "issuer": "1196RFa2m5Zui1N32JMhEo4V4TsRMPUTsdjWRceEMW"
              },
              "creator": "1196RFa2m5Zui1N32JMhEo4V4TsRMPUTsdjWRceEMW",
              "verification_method": "ca28a7524c1b110523f300f8aa7b0c4dd3979103075891bf7558467c1f247c9c",
              "proof_value": "da9820d71153c0a437d51b1b7106d166e8a2931d7f7545096386327bf2e5d8128ae01e1b00b45f598542718a63bbb0ef36e2f3126fe8d8548c4285e9bf3a9102",
              "proof_purpose": "Authentication"
            }
          }
        }
      }
    }
    ```
