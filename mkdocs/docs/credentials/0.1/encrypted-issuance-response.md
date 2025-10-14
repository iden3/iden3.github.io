
type: `/credentials/0.1/encrypted-issuance-response`

The issuer uses this type of response if it wants to return the encrypted credentials to the user.

```json
{
    "context": "https://raw.githubusercontent.com/iden3/claim-schema-vocab/main/schemas/json-ld/kyc-v3.json-ld",
    "data": {
      "ciphertext": "bIQMNMBa9gGBb2S9L6pN543KjcQMk2QwKU1n4IOTYEsL1CPsHahsM8LADOX9InjOmfkwP1anAZaDR1YM2cizW64NgdbZVd13nYSjK9VL5f-LSAMuK-CIUjSunO6JNoNbI7W4KkPIkUZHnB3nWn3gwhCA_AZuE-li6ESAAuSbW5lYRnxn8lhvLCdrg4z1_EnDwJSwpdjR1KVmAGQpJgk98i-1MJ59EP4Zgatn5OkZ-orhdEASHOSQEoA0fGigyLSUsKxYwIz9LpcjYcBVDalz9Ola_0eDa5SkkiTyKLVyDAfGkh9dpdJrxQ08JHAxcOULBv90XHcDbJtGnUPhxz99qhk4aEOfDmB4ZIn3o0S6LRGu3uD4SoFbH_nFj-47TGP-4ekehP0GuegO71ADuedbp5lh6I5eFUno4K2RsM0KAXIJu6P-f7F_k8I_YzhgAlNGtD4u0k7v9dK15TIyhRW7lHol7CzEI68xMo1e5WNylLLUDPNA4DnlXzZeHyB42z5boP-ZxL4anpFQNsNKDVek_R8LEIpxzJBwkC0u120XUQMj9HqSXW95y4gJ_TU0iHePmU15SWR42QK93nnsfHSdWyXIaroArKimPX51deowmRQe7AXK80a5_2pidP6gpevyqueDAVoUefqI7O6b3DHrivHGBC2obeLe8M-ldYc17r8GGVjKbLjChkDT40lE0tq_7Srj1vXmVGK7qcpkIJhCIA-kSzEPxS2Ab2TMDK10lu81Lcp71pp7bcXgyZqNpV5kopy2dpVjhcRIk0XWtDkkvle6BNI84IkCtX1bvlQOO2pcq0N0glYasU4eMWMgYYm6jkrviUsv-mqRyC2sfiBpAiFUT0O8TiA34qvDPd6bugwGl-4sMNuyUbjHPsJQqUjO4DRCDfVQWTCWP6-Fh5AIuOW1-gUsH8-5-139ylVLpMoG8j_eDP--K_WD1k6DzzmZgOOctzbmbPZmYL2zZTS_-_6kZB1ivtbwVZFLdqlGCaPANlnWYBhia-Pp5zX-Xak6CVrHfO9NMs9ZtAomWw-SnqCzvqcGdQO3E29MfnHaqf9jTVIHxKTPy-PBjxdq3J6ZoMgZG0CEA0wydDyD_CD9yiwTSWLU-21TQic88cA30Yz5jITpQUrKnquuVu7BioJ5fCZj8_mQ1WO-OIJi87CdRqKy0tX7p9uwDTx56p2WRyD6yJ2gRIq57siERkdDW10iOfTbd8zxMQuQnh5N1BdWqGhgwzBK58_wKWkGtqKJUwyw8hs-Qg",
      "encrypted_key": "WbBAzrb5mbhMiGIFHII2prO1RJ9OntWypFpjFjD8uZbopfwhgVSAjisCb0HJngBInN3QJ65y4t7a0HFFhzfLUiEQYYVyaMGZw2Rq81XXpGtvgMyBaQX5IpxbLd5Uq33NjMkz_2clQ2B17lU2y8W1Kg4RiK3uE1DEe6IMDS_gIAUPrla1h50XRIhqEn2OgPxRgABr6WXPF1OxtOQqrGRIXa361f4B8412HFk2goeM0YdsvZaN-ZW8KDU8Md3SyFdnfnllTyqWvHQYLlN3uVrGqi7vl-pRU17x5CDk3yN1PJv0zHNXv_0NSZZtBQDTcABir89_wwu-5yx80gzFVMJP7g",
      "iv": "jM-sFRf27lNSAGSU",
      "protected": "eyJhbGciOiJSU0EtT0FFUC0yNTYiLCJlbmMiOiJBMjU2R0NNIiwia2lkIjoiZGlkOmV4YW1wbGU6YWxpY2Uja2V5LTEiLCJ0eXAiOiJhcHBsaWNhdGlvbi9pZGVuM2NvbW0tZW5jcnlwdGVkLWpzb24ifQ",
      "tag": "1pmC4u9s3fK0xVcka25O2w"
    },
    "id": "a6b89dca-a8e8-11f0-9e07-3ec1cb51743a",
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
        "coreClaim": "c9b2370371b7fa8b3dab2a5ba81b68382a0000000000000000000000000000000112af67e0c340aef5540f8979b46a0eed13951c6ce60dad8875d1ab1e940d00e7b6f4a76dcd25ab4899abcd2ce536ce9f8c13c42f639c1cacfcb74dea279d0b0000000000000000000000000000000000000000000000000000000000000000b981ea840000000046ef72710000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
        "signature": "d02fbc1f76fc9d642754ba8a42df45ecd0fdb1de602d54fbda632d51e500408dccc1f170470c006e2f7085290016c7205968cddabf0362f6ef8774223f372c04"
      }
    ],
    "type": "KYCAgeCredential"
},
```

| Field | Description | Type | Required |
| --- | --- | --- | --- |
| id | ID of VC | string | ✅ |
| context | Context of credential | string | ✅ |
| type | Types of credential | strings | ✅ |
| data | JWE token in JSON format | object | ✅ |
| proof | List of proofs that the VC has | *list of object | ✅ |

The content of `credentials.data` is an encrypted [W3Credential](https://www.w3.org/TR/vc-data-model/) without the proof part.


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
    "context": "https://raw.githubusercontent.com/iden3/claim-schema-vocab/main/schemas/json-ld/kyc-v3.json-ld",
    "data": {
      "ciphertext": "bIQMNMBa9gGBb2S9L6pN543KjcQMk2QwKU1n4IOTYEsL1CPsHahsM8LADOX9InjOmfkwP1anAZaDR1YM2cizW64NgdbZVd13nYSjK9VL5f-LSAMuK-CIUjSunO6JNoNbI7W4KkPIkUZHnB3nWn3gwhCA_AZuE-li6ESAAuSbW5lYRnxn8lhvLCdrg4z1_EnDwJSwpdjR1KVmAGQpJgk98i-1MJ59EP4Zgatn5OkZ-orhdEASHOSQEoA0fGigyLSUsKxYwIz9LpcjYcBVDalz9Ola_0eDa5SkkiTyKLVyDAfGkh9dpdJrxQ08JHAxcOULBv90XHcDbJtGnUPhxz99qhk4aEOfDmB4ZIn3o0S6LRGu3uD4SoFbH_nFj-47TGP-4ekehP0GuegO71ADuedbp5lh6I5eFUno4K2RsM0KAXIJu6P-f7F_k8I_YzhgAlNGtD4u0k7v9dK15TIyhRW7lHol7CzEI68xMo1e5WNylLLUDPNA4DnlXzZeHyB42z5boP-ZxL4anpFQNsNKDVek_R8LEIpxzJBwkC0u120XUQMj9HqSXW95y4gJ_TU0iHePmU15SWR42QK93nnsfHSdWyXIaroArKimPX51deowmRQe7AXK80a5_2pidP6gpevyqueDAVoUefqI7O6b3DHrivHGBC2obeLe8M-ldYc17r8GGVjKbLjChkDT40lE0tq_7Srj1vXmVGK7qcpkIJhCIA-kSzEPxS2Ab2TMDK10lu81Lcp71pp7bcXgyZqNpV5kopy2dpVjhcRIk0XWtDkkvle6BNI84IkCtX1bvlQOO2pcq0N0glYasU4eMWMgYYm6jkrviUsv-mqRyC2sfiBpAiFUT0O8TiA34qvDPd6bugwGl-4sMNuyUbjHPsJQqUjO4DRCDfVQWTCWP6-Fh5AIuOW1-gUsH8-5-139ylVLpMoG8j_eDP--K_WD1k6DzzmZgOOctzbmbPZmYL2zZTS_-_6kZB1ivtbwVZFLdqlGCaPANlnWYBhia-Pp5zX-Xak6CVrHfO9NMs9ZtAomWw-SnqCzvqcGdQO3E29MfnHaqf9jTVIHxKTPy-PBjxdq3J6ZoMgZG0CEA0wydDyD_CD9yiwTSWLU-21TQic88cA30Yz5jITpQUrKnquuVu7BioJ5fCZj8_mQ1WO-OIJi87CdRqKy0tX7p9uwDTx56p2WRyD6yJ2gRIq57siERkdDW10iOfTbd8zxMQuQnh5N1BdWqGhgwzBK58_wKWkGtqKJUwyw8hs-Qg",
      "encrypted_key": "WbBAzrb5mbhMiGIFHII2prO1RJ9OntWypFpjFjD8uZbopfwhgVSAjisCb0HJngBInN3QJ65y4t7a0HFFhzfLUiEQYYVyaMGZw2Rq81XXpGtvgMyBaQX5IpxbLd5Uq33NjMkz_2clQ2B17lU2y8W1Kg4RiK3uE1DEe6IMDS_gIAUPrla1h50XRIhqEn2OgPxRgABr6WXPF1OxtOQqrGRIXa361f4B8412HFk2goeM0YdsvZaN-ZW8KDU8Md3SyFdnfnllTyqWvHQYLlN3uVrGqi7vl-pRU17x5CDk3yN1PJv0zHNXv_0NSZZtBQDTcABir89_wwu-5yx80gzFVMJP7g",
      "iv": "jM-sFRf27lNSAGSU",
      "protected": "eyJhbGciOiJSU0EtT0FFUC0yNTYiLCJlbmMiOiJBMjU2R0NNIiwia2lkIjoiZGlkOmV4YW1wbGU6YWxpY2Uja2V5LTEiLCJ0eXAiOiJhcHBsaWNhdGlvbi9pZGVuM2NvbW0tZW5jcnlwdGVkLWpzb24ifQ",
      "tag": "1pmC4u9s3fK0xVcka25O2w"
    },
    "id": "a6b89dca-a8e8-11f0-9e07-3ec1cb51743a",
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
        "coreClaim": "c9b2370371b7fa8b3dab2a5ba81b68382a0000000000000000000000000000000112af67e0c340aef5540f8979b46a0eed13951c6ce60dad8875d1ab1e940d00e7b6f4a76dcd25ab4899abcd2ce536ce9f8c13c42f639c1cacfcb74dea279d0b0000000000000000000000000000000000000000000000000000000000000000b981ea840000000046ef72710000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
        "signature": "d02fbc1f76fc9d642754ba8a42df45ecd0fdb1de602d54fbda632d51e500408dccc1f170470c006e2f7085290016c7205968cddabf0362f6ef8774223f372c04"
      }
    ],
    "type": "KYCAgeCredential"
  }
}
```
