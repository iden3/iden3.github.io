
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
  "to": "did:polygonid:polygon:mumbai:2qJUZDSCFtpR8QvHyBC4eFm6ab9sJo5rqPbcaeyGC4",
  "from": "did:iden3:polygon:mumbai:x3HstHLj2rTp6HHXk2WczYP7w3rpCsRbwCMeaQ2H2",
  "body": {
    "credential": {
      "id": "urn:53a608cb-b5b6-4cc9-96a8-c230ff955554",
      "@context": [
        "https://www.w3.org/2018/credentials/v1",
        "https://schema.iden3.io/core/jsonld/iden3proofs.jsonld",
        "https://raw.githubusercontent.com/iden3/claim-schema-vocab/main/schemas/json-ld/kyc-v3.json-ld"
      ],
      "type": [
        "VerifiableCredential",
        "KYCAgeCredential"
      ],
      "credentialSubject": {
        "id": "did:polygonid:polygon:mumbai:2qJUZDSCFtpR8QvHyBC4eFm6ab9sJo5rqPbcaeyGC4",
        "birthday": 19960424,
        "documentType": 99,
        "type": "KYCAgeCredential"
      },
      "issuer": "did:iden3:polygon:mumbai:x3HstHLj2rTp6HHXk2WczYP7w3rpCsRbwCMeaQ2H2",
      "expirationDate": "2058-07-10T11:33:20.000Z",
      "issuanceDate": "2023-09-07T14:36:48.074Z",
      "credentialSchema": {
        "id": "https://raw.githubusercontent.com/iden3/claim-schema-vocab/main/schemas/json/KYCAgeCredential-v3.json",
        "type": "JsonSchema2023"
      },
      "credentialStatus": {
        "id": "https://rhs-staging.polygonid.me",
        "revocationNonce": 1000,
        "type": "Iden3ReverseSparseMerkleTreeProof"
      },
      "proof": [
        {
          "type": "BJJSignature2021",
          "issuerData": {
            "id": "did:iden3:polygon:mumbai:x3HstHLj2rTp6HHXk2WczYP7w3rpCsRbwCMeaQ2H2",
            "state": {
              "rootOfRoots": "0000000000000000000000000000000000000000000000000000000000000000",
              "revocationTreeRoot": "0000000000000000000000000000000000000000000000000000000000000000",
              "claimsTreeRoot": "5e5dca21a62dfbbd8b984a997dd9d666b6710d5499906301b19fb6996bfc1a02",
              "value": "139042475daf67e0c340aef5540f8979b46a0eed13951c6ce60dad8875d1ab1e"
            },
            "authCoreClaim": "cca3371a6cb1b715004407e325bd993c0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000007cc77af06d6ea9f91434ce69e46821371cc341eb9e190262a16f46d15410ce0d1a090d38ded1e32a74e5fa0908764606adbcb917edff84b6ca60968d8a8d79090000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
            "mtp": {
              "existence": true,
              "siblings": []
            },
            "credentialStatus": {
              "id": "https://rhs-staging.polygonid.me",
              "revocationNonce": 0,
              "type": "Iden3ReverseSparseMerkleTreeProof"
            }
          },
          "coreClaim": "c9b2370371b7fa8b3dab2a5ba81b68382a00000000000000000000000000000002128459e997f3d9402b75af3fb9ad1e2db8f3288d3f5b6a13fa833621070d0069dee7de22463f48d75e219aed6cebcaadde18c1aacce28cd53db0317d1e9d2b0000000000000000000000000000000000000000000000000000000000000000e80300000000000080d481a60000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
          "signature": "4fb847963a0903ead57a45bcf511f84067b092aa5b21e95349ad3cf284f2678b8522765989e807ec7ab36ca541dab96a0604abc1a1ea27db1bf59a23f0686f04"
        }
      ]
    }
  }
}
    ```
