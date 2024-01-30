# Refresh service

## Description

In some cases, having mechanisms to refresh issued credentials can be helpful. A refresh service allows credentials to be updated by the user client. This approach ensures that users are consistently using the updated information provided by the issuer, such as a user balance, a game score, or other data that can be frequently updated.

## Example

Consider an example of balance credentials, where a user proves his balance to get some benefits. The balance can be changed a lot during a short period. In this case, the user needs to interact with the issuer every time they need to use the credential. This is where the refresh service comes in handy. The refresh service can handle necessary data updates on the background of the user client without additional interaction between the issuer and the user.

## Changes in the verifiable credential

In protocol level, the revocation service is integrated into the W3C verifiable credential:

```json
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://schema.iden3.io/core/jsonld/iden3proofs.jsonld"
    ...
  ],
  ...
  "refreshService": {
	  "id": "https://refreshService.example", // iden3comm agent endpoint
    "type": "Iden3RefreshService2023"
  }
}
```

The data model of `refershService`:

| Field name | Data type | Description | Required |
| --- | --- | --- | --- |
| type | string | Type of refresh service. | ✅ |
| id | string | URL to [iden3comm](https://iden3-communication.io/) agent endpoint | ✅ |

Supported types:

1. Iden3RefreshService2023. [Type definition](https://github.com/iden3/claim-schema-vocab/blob/main/core/jsonld/iden3proofs.jsonld#L284).

## Client communication with refresh service

If the `refreshService` section within a verifiable credential is of type **Iden3RefreshService2023**, the client is required to construct a [refresh iden3comm message](https://iden3-communication.io/credentials/1.0/refresh/) wrapped in JWZ token. This token should then be sent to the agent endpoint specified by `refreshService.id`.

## Integration examples

1. Golang integration:
    1. [Issuer-node](https://github.com/0xPolygonID/issuer-node).
2. JS integration:
    1. [JS-SDK](https://github.com/0xPolygonID/js-sdk).
