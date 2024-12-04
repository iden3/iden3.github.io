# Media types for iden3comm protocol

Media type of message defines the format of the envelope that is used in messaging. More read at [DIDComm](https://identity.foundation/didcomm-messaging/spec/#iana-media-types) specification.

###  Supported media types of envelope

-  `application/iden3-zkp-json`
-  `application/iden3comm-plain-json`
-  `application/iden3comm-signed-json`
-  `application/iden3comm-encrypted-json`

Each media type shows how envelope of the message is created and present in the payload as a `typ` field.

### When to use:
- `application/iden3-zkp-json` corresponds to jwz envelope about which you can read more [here](../proposals/jwz/overview.md). <br />
- `application/iden3comm-signed-json` corresponds to [JWS](https://www.rfc-editor.org/rfc/rfc7515.html) envelope.  <br />
- `application/iden3comm-plain-json` represents simple json message with a property 'typ'.  <br />
- `application/iden3comm-encrypted-json` is a media type for encrypted envelops  <br />

In our protocol corresponding packers are implemented in [golang](https://github.com/iden3/iden3comm/tree/main/packers) and [typescript](https://github.com/0xPolygonID/js-sdk/tree/main/src/iden3comm/packers).


To determine which envelope to use, the sender can specify the `accept` header, allowing the responder to choose one of the supported profiles for authentication.
Profile is a combination of media type and specific parameters for this media type.


For ZKP profile `circuits` param could be added (optional):

- authV2

For ZKP, Signed and Encrypted profiles `alg` param could be added (optional)

ZKP profole params:

- groth16

Signing algorithms:

- ES256K
- ES256K-R

Encryption algorimts:

- anoncrypt ( ECDH-ES + AES key wrap; AES-CBC + HMAC-SHA512)

Currently `accept` header is only applicable for authorization request message.
Possible example:
```
[
  "iden3comm/v1;env=application/iden3-zkp-json;circuitId=authV2;alg=groth16",
  "iden3comm/v1;env=application/iden3comm-signed-json;alg=ES256K-R"
]
```

If `accept` header is omitted - default value is:

```
[
  "iden3comm/v1;env=application/iden3-zkp-json;circuitId=authV2;alg=groth16"
]
```

So default response will always use auth v2 circuit, groth 16 proof generator and jwz envelope.


In case user initiates a communication, for example with embedded issuer and doesn't know what kind of profiles issuer agent accepts it should use discovery protocol.
