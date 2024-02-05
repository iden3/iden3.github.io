# Display method

## Description

To improve credential usage, a client needs to be able to customize the presentation of credentials in user wallets. A standard must be established that will guide the wallet in displaying credit cards. This will improve the user experience and allow issuers to present their own special presentation for credentials.

## Changes in the verifiable credential

In protocol level, the display method is integrated into the W3C verifiable credential:

```json
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://raw.githubusercontent.com/iden3/claim-schema-vocab/main/core/jsonld/displayMethod.jsonld"
    ...
  ],
  ...
  "displayMethod": {
    "id": "ipfs://QmY5ab9FAMEFtdG1VHBXhHANRscUTbDzrG6LC2FWqicc5J",
    "type": "Iden3BasicDisplayMethodV1"
  }
}
```

The data model of `displayMethod`:

| Field name | Data type | Description | Required |
| --- | --- | --- | --- |
| id | string | IPFS link or URL to metadata | ✅ |
| type | string | Type of refresh service. | ✅ |

Supported types:

1. Iden3BasicDisplayMethodV1. [Type definition](https://github.com/iden3/claim-schema-vocab/blob/main/core/jsonld/displayMethod.jsonld#L15). The type supports the metadata format:
    ```json
    {
      "title": "KYC Country of Residence",
      "description": "Know you customer verification",
      "issuerName": "PolygonID Issuer",
      "titleTextColor": "#000000",
      "descriptionTextColor": "#000000",
      "issuerTextColor": "#000000",
      "backgroundImageUrl": "ipfs://Qmagkvd9Bz8yXXupWZtBC69RqGfRex72Qou1XjUNvC7fLB",
      "logo": {
        "uri": "ipfs://QmWkSgmHbKRfhndWqHwVgfVpZSrWNiWZMTHb6k5KxY8ySc",
        "alt": "Logo PolygonID issuer"
      }
    }
    ```

    | Attribute | Purpose | Data type | Required |
    | --- | --- | --- | --- |
    | title | Credential title | string | ❌ |
    | description | Description | string < 120 characters | ❌ |
    | issuerName | Issuer name | string | ❌ |
    | titleTextColor | Text color for title and issueName | hex | ❌ |
    | descriptionTextColor | Text color for description | hex | ❌ |
    | issuerTextColor | Text color for issuer name | hex | ❌ |
    | backgroundColor | Background color | hex | ❌ |
    | backgroundImageUrl | Background image url | IPFS or URL (.svg, .png) | ❌ |
    | logo.uri | Logo URL | IPFS or URL 32x32 (.svg, .png) | ❌ |
    | logo.alt | Logo text | string | ❌ |
