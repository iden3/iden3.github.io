
type: `/credentials/0.1/encrypted-issuance-response`

The issuer uses this type of response if it wants to return the encrypted credentials to the user.

```json
{
  "context": "https://raw.githubusercontent.com/iden3/claim-schema-vocab/main/schemas/json-ld/kyc-v3.json-ld",
  "data": {
    "protected": "eyJhbGciOiJSU0EtT0FFUC0yNTYiLCJlbmMiOiJBMjU2R0NNIiwia2lkIjoiZGlkOmV4YW1wbGU6YWxpY2Uja2V5LTEifQ",
    "header": {
      "alg": "RSA-OAEP-256",
      "kid": "did:example:alice#key-1"
    },
    "encrypted_key": "qMBHtC4ZBhYznjVIK_lov42utXT_jWs7O33bC_AqODjltL76vVNhfn4rT2QNw9xbMMZEL0s7TABX3E9fRTBXr_qGbhVlgVs7fuoIms3T-uausP-6_PyElMWWPQ84586XXL2CoDOgAeNAaN7MnV37QlvlvPRrB_A2BJxyNdLEbq-Z_NWOz4MJBcOZNzLRRu1UPiBYOeyBXCwLyC4f7y3F73m2xHBQq523OnhaaT_9vZMeVpdBUJM8utfU8WkFdK94JvD8WO7TljWlJD9TN3OQY_CvfXEfSejqElPcN6ydJA8GaPuwNg2cEBKau8GnDs3wYUvyszGXI2t3QQenMbNL5Q",
    "iv": "pXUjHplaJJ1BNeLp",
    "ciphertext": "qPdeTqQ_Fl1FyLiqBLu4jezxTyfiV6IyZwQBYXc1sRZc3O4EvKFYfYi6nEbtzh_xU1gJLFFv4zTk08rQpYwvuDcoeQyUWkilVwTZPempytSdpisPE92-rDi-28kn6jnYBbbKRUjjJqgh4uGZtZPhve7zOgtP3Yk75LnqzaWCAl2mpbkYWXOXiJ5EmQR2T-17vO3GYcfa1SwupVoFJFooCuARJVylK_rxcayjKB_Ql8El9xkmO-Ib8Vtc25WbSotLG6ot82hbsM6ArkL4QMBt2FF79k--VSf5AloITxZOlEcWVamv1wNHMoChbwpV8xwpQTAz2-wslk6Xgse271xBir_VV6Z8yRUg7fCw-X5nqFUr8xjS0NYJCCaESyeqsVyBMQu8a5AqIXL1ceG9umqeqjaS7_f3h1pLtd2NrXfmnotH9cNQhT6OHcf1aA8OuK1JQx0qpFqqKZB_nnS5r6Zi-lgSV0EZKaM_QDpt-af8T6iTHTskXuVgs5PTNQkpK5xKRWYZ_x4GTf3TckfF5nweE2GGsgQkQl1T2gB0_dKqnx04DHrpzNC6JghvKIRgm7l0MatLyLz9BACwBhAL3uf9nkFg8-fZ7g_2x8LrkPWbLGdIphP5n-dA99gZL6q16u0lEGeYztv1Xe5t70pjKUYrOs3KDtnppRknMsOfOw6e_qf09XAbUHNMfEtjeSplOaT8VCG2ikooAeDDURa91LOgIhdjsNmMfww13IytB0TnXSo7YBo1u7Of04cJ0WEUZnw2He3nrvcV9ORqphA7AMKSTLnRa8LrpUCB-0v7nMGlJXKDtFCxuq7FOTg6FsWwfnWyB5ukNKmgg2R_6whZF70qvhkwo0ja5wq7Hxg5aweZjW9-dhbdD9BBtHlVot968Q_FcKOpk6UPkVa6vRNPOo7TkQphsd2v1s_qfjwINEAsr8wLlqLx00p4NLvS2On1QUopi1IDFA31L_R54APXdjVHwrys8UpoPR2NpvBOY3gkGlBCXHjqlxcmvngqsAgs-RHtmzH7t190x0JdzpCnT4qqnDybU1OSHCZIqKfV09W82xjb2HR_RC3VKj-h9kqrhDzyIrPmUIDHtMrB0g77AS1WN6bgSvMetPi-fIcsEJSOex-FJUU00NNLXyZCWOOcjpOjI6kTe-YMN4cCC1UJ358h03OPnTHWXfhRMALI9t7-t5TPFjtb240FPJOISpBTNRn5QgoJ9ta5tOVy9DfUt_f9kmFteRhatyzCmZUKrW3m2xTuzU6eBxHgkvBz",
    "tag": "3eXoXKxOB4rGZTNVb3i3Ew"
  },
  "id": "5b39cfe6-a9cd-11f0-9a17-3ec1cb51743a",
  "proof": [
    {
      "type": "BJJSignature2021",
      "issuerData": {
        "id": "did:polygonid:polygon:amoy:2qXnMYUfndFcM4NVVjbCrzjfMj9eoDYw6Y7zXtHaHR",
        "state": {
          "claimsTreeRoot": "b0ddc3a021388c7547ea62567b105f0b01cfd2f2af0a4b9e3f67eae563796e2d",
          "value": "1075a2a76ea979363f6ae1b96b90a63eed313495c42462e43c12c0fc499d0a11"
        },
        "authCoreClaim": "cca3371a6cb1b715004407e325bd993c0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000004ac5b230672ab2b8406ca0d10eb7936d23195c9ebbc8e286a262d58d3cd06400ec248d78999b7b38007964a3bd2b46255ec41e686141c83d455db2eae5edc0140000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
        "mtp": {
          "existence": true,
          "siblings": []
        },
        "credentialStatus": {
          "id": "https://issuernode-mumbai-protocol.polygonid.me/v2/agent",
          "revocationNonce": 0,
          "type": "Iden3commRevocationStatusV1.0"
        }
      },
      "coreClaim": "c9b2370371b7fa8b3dab2a5ba81b68382a000000000000000000000000000000021204bfd2d528a8a70e276c14fd146df9c133be5dd3a9524db1022a2b530c0010b59b95eb5fa55505513b5b7ea79d46ff3c1cb1c8b50fe22171177bceac660b00000000000000000000000000000000000000000000000000000000000000003e6ae6d00000000046ef72710000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
      "signature": "7117705347cbcf8f32d4147cfc0f4c916303c8c321acbf3173b62b30076ea82d46a96e591680f4c019c897c9c9cc91919dd8973d038e10366bd462290c32df00"
    }
  ],
  "type": "KYCAgeCredential"
}
```

| Field | Description | Type | Required |
| --- | --- | --- | --- |
| id | ID of VC | string | ✅ |
| context | Context of credential | string | ✅ |
| type | Type of credential | string | ✅ |
| data | JWE token in JSON format | object | ✅ |
| proof | List of proofs that the VC has | *list of objects | ✅ |

The content of `credentials.data` is an encrypted [W3Credential](https://www.w3.org/TR/vc-data-model/) without the proof part.


- **Example of credential issuance:**
    
```json
{
  "id": "1924af5a-7d63-4850-addf-0177cdc34786",
  "thid": "1924af5a-7d63-4850-addf-0177cdc34786",
  "typ": "application/iden3comm-plain-json",
  "type": "https://iden3-communication.io/credentials/0.1/encrypted-issuance-response",
  "to": "did:polygonid:polygon:mumbai:2qCgaRG3nfDsK7X2x9Lnh4DuAQtrGNSRZvHzcDQKA3",
  "from": "did:polygonid:polygon:amoy:2qXnMYUfndFcM4NVVjbCrzjfMj9eoDYw6Y7zXtHaHR",
  "body": {
    "context": "https://raw.githubusercontent.com/iden3/claim-schema-vocab/main/schemas/json-ld/kyc-v3.json-ld",
    "data": {
      "protected": "eyJhbGciOiJSU0EtT0FFUC0yNTYiLCJlbmMiOiJBMjU2R0NNIiwia2lkIjoiZGlkOmV4YW1wbGU6YWxpY2Uja2V5LTEifQ",
      "header": {
        "alg": "RSA-OAEP-256",
        "kid": "did:example:alice#key-1"
      },
      "encrypted_key": "qMBHtC4ZBhYznjVIK_lov42utXT_jWs7O33bC_AqODjltL76vVNhfn4rT2QNw9xbMMZEL0s7TABX3E9fRTBXr_qGbhVlgVs7fuoIms3T-uausP-6_PyElMWWPQ84586XXL2CoDOgAeNAaN7MnV37QlvlvPRrB_A2BJxyNdLEbq-Z_NWOz4MJBcOZNzLRRu1UPiBYOeyBXCwLyC4f7y3F73m2xHBQq523OnhaaT_9vZMeVpdBUJM8utfU8WkFdK94JvD8WO7TljWlJD9TN3OQY_CvfXEfSejqElPcN6ydJA8GaPuwNg2cEBKau8GnDs3wYUvyszGXI2t3QQenMbNL5Q",
      "iv": "pXUjHplaJJ1BNeLp",
      "ciphertext": "qPdeTqQ_Fl1FyLiqBLu4jezxTyfiV6IyZwQBYXc1sRZc3O4EvKFYfYi6nEbtzh_xU1gJLFFv4zTk08rQpYwvuDcoeQyUWkilVwTZPempytSdpisPE92-rDi-28kn6jnYBbbKRUjjJqgh4uGZtZPhve7zOgtP3Yk75LnqzaWCAl2mpbkYWXOXiJ5EmQR2T-17vO3GYcfa1SwupVoFJFooCuARJVylK_rxcayjKB_Ql8El9xkmO-Ib8Vtc25WbSotLG6ot82hbsM6ArkL4QMBt2FF79k--VSf5AloITxZOlEcWVamv1wNHMoChbwpV8xwpQTAz2-wslk6Xgse271xBir_VV6Z8yRUg7fCw-X5nqFUr8xjS0NYJCCaESyeqsVyBMQu8a5AqIXL1ceG9umqeqjaS7_f3h1pLtd2NrXfmnotH9cNQhT6OHcf1aA8OuK1JQx0qpFqqKZB_nnS5r6Zi-lgSV0EZKaM_QDpt-af8T6iTHTskXuVgs5PTNQkpK5xKRWYZ_x4GTf3TckfF5nweE2GGsgQkQl1T2gB0_dKqnx04DHrpzNC6JghvKIRgm7l0MatLyLz9BACwBhAL3uf9nkFg8-fZ7g_2x8LrkPWbLGdIphP5n-dA99gZL6q16u0lEGeYztv1Xe5t70pjKUYrOs3KDtnppRknMsOfOw6e_qf09XAbUHNMfEtjeSplOaT8VCG2ikooAeDDURa91LOgIhdjsNmMfww13IytB0TnXSo7YBo1u7Of04cJ0WEUZnw2He3nrvcV9ORqphA7AMKSTLnRa8LrpUCB-0v7nMGlJXKDtFCxuq7FOTg6FsWwfnWyB5ukNKmgg2R_6whZF70qvhkwo0ja5wq7Hxg5aweZjW9-dhbdD9BBtHlVot968Q_FcKOpk6UPkVa6vRNPOo7TkQphsd2v1s_qfjwINEAsr8wLlqLx00p4NLvS2On1QUopi1IDFA31L_R54APXdjVHwrys8UpoPR2NpvBOY3gkGlBCXHjqlxcmvngqsAgs-RHtmzH7t190x0JdzpCnT4qqnDybU1OSHCZIqKfV09W82xjb2HR_RC3VKj-h9kqrhDzyIrPmUIDHtMrB0g77AS1WN6bgSvMetPi-fIcsEJSOex-FJUU00NNLXyZCWOOcjpOjI6kTe-YMN4cCC1UJ358h03OPnTHWXfhRMALI9t7-t5TPFjtb240FPJOISpBTNRn5QgoJ9ta5tOVy9DfUt_f9kmFteRhatyzCmZUKrW3m2xTuzU6eBxHgkvBz",
      "tag": "3eXoXKxOB4rGZTNVb3i3Ew"
    },
    "id": "5b39cfe6-a9cd-11f0-9a17-3ec1cb51743a",
    "proof": [
      {
        "type": "BJJSignature2021",
        "issuerData": {
          "id": "did:polygonid:polygon:amoy:2qXnMYUfndFcM4NVVjbCrzjfMj9eoDYw6Y7zXtHaHR",
          "state": {
            "claimsTreeRoot": "b0ddc3a021388c7547ea62567b105f0b01cfd2f2af0a4b9e3f67eae563796e2d",
            "value": "1075a2a76ea979363f6ae1b96b90a63eed313495c42462e43c12c0fc499d0a11"
          },
          "authCoreClaim": "cca3371a6cb1b715004407e325bd993c0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000004ac5b230672ab2b8406ca0d10eb7936d23195c9ebbc8e286a262d58d3cd06400ec248d78999b7b38007964a3bd2b46255ec41e686141c83d455db2eae5edc0140000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
          "mtp": {
            "existence": true,
            "siblings": []
          },
          "credentialStatus": {
            "id": "https://issuernode-mumbai-protocol.polygonid.me/v2/agent",
            "revocationNonce": 0,
            "type": "Iden3commRevocationStatusV1.0"
          }
        },
        "coreClaim": "c9b2370371b7fa8b3dab2a5ba81b68382a000000000000000000000000000000021204bfd2d528a8a70e276c14fd146df9c133be5dd3a9524db1022a2b530c0010b59b95eb5fa55505513b5b7ea79d46ff3c1cb1c8b50fe22171177bceac660b00000000000000000000000000000000000000000000000000000000000000003e6ae6d00000000046ef72710000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
        "signature": "7117705347cbcf8f32d4147cfc0f4c916303c8c321acbf3173b62b30076ea82d46a96e591680f4c019c897c9c9cc91919dd8973d038e10366bd462290c32df00"
      }
    ],
    "type": "KYCAgeCredential"
  }
}
```
