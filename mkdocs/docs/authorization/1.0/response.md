
type: `/authorization/1.0/response`

Authorization response to verification proof in a resource.

```json
{
	"did_doc": "<user_did_document>",
	"message": "<authorization_request_payload>",
	"scope": ["<list_of_proofs>"]
}
```

| Field                   | Description                                                                                   | Type             | Required |
|-------------------------|-----------------------------------------------------------------------------------------------|------------------|----------|
| did_doc                 | User`s DID documen                                                                            | JSON             | ❌        |
| message                 | Payload for an authorization request                                                          | string           | ❌        |
| scope                   | List of objects with zkproo f and public inputs                                               | *list of objects | ✅        |
| scope.id                | Unique id to present unique authorization request                                             | uint32           | ✅        |
| scope.circuitId         | Information that circuit was used for generating zk proof                                     | string           | ✅        |
| scope.vp                | Information that user wants to disclosure                                                     | JSON             | ❌        |
| scope[i].proof          | proof                                                                                         | JSON             | ✅        |
| scope[i].public_signals | A list of public inputs was utilized in the generation of the Zero-Knowledge Proof (ZKProof). | list of strings  | ✅        |

The `scope` field contains a list of zero-knowledge proofs and public inputs for authorization on a resource. More about scope contnet: https://github.com/iden3/go-circuits

- **Example of authorization response:**
    
    ```json
    {
      "id": "7f38a193-0918-4a48-9fac-36adfdb8b542",
      "typ": "application/iden3comm-plain-json",
      "type": "https://iden3-communication.io/authorization/1.0/response",
      "thid": "7f38a193-0918-4a48-9fac-36adfdb8b542",
      "body": {
        "message": "test",
    	  "did_doc": {},
        "scope": [
          {
            "id": 1,
            "circuitId": "credentialAtomicQueryMTP",
            "proof": {
              "pi_a": [
                "9742806134969392226546322490560630802447930806537100408086160321763928272376",
                "21455791203277003434494375277451189817937636213176444019767120099596514163982",
                "1"
              ],
              "pi_b": [
                [
                  "10380825203862480352812509276126714433521593951138343399902602814224203230644",
                  "3258713202006941217475014546591342349864153477480289203741647764981122849969"
                ],
                [
                  "1822645146824926970539316997069683858010941097218414131904374790154170166572",
                  "10353710770765315368364178270577963995559055291780726291909607243297495512681"
                ],
                [
                  "1",
                  "0"
                ]
              ],
              "pi_c": [
                "9484567403290042082168690530225028055268796074940883562365588128103915644358",
                "6661326208907807355087503512595101570698136414120018064634575604679380099060",
                "1"
              ],
              "protocol": "groth16"
            },
            "pub_signals": [
              "379949150130214723420589610911161895495647789006649785264738141299135414272",
              "18656147546666944484453899241916469544090258810192803949522794490493271005313",
              "1",
              "17339270624307006522829587570402128825147845744601780689258033623056405933706",
              "26599707002460144379092755370384635496563807452878989192352627271768342528",
              "17339270624307006522829587570402128825147845744601780689258033623056405933706",
              "1642074362",
              "106590880073303418818490710639556704462",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0",
              "0"
            ]
          }
        ]
      },
      "from": "did:polygonid:polygon:mumbai:2qJG6RYgN1u6v7JAYSdfixSwktnZ7hMzd4t21SCdNu",
      "to": "did:polygonid:polygon:mumbai:2qFroxB5kwgCxgVrNGUM6EW3khJgCdHHnKTr3VnTcp"
    }
    ```
