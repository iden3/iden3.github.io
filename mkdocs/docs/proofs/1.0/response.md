
type: `/proof/1.0/response`

Proof response to verification proof in a requester side.

```json
{
	"scope": ["<list_of_proofs>"]
}
```

| Field | Description | Type | Required |
| --- | --- | --- | --- |
| scope.id | Unique id to present unique authorization request | uint32  | ✅ |
| scope.circuitId | Information that circuit was used for generating zk proof | string | ✅ |
| scope.vp | Information that user want to disclosure | JSON | ❌ |
| scope.proof | ZKProof | JSON | ✅ |
| scope.pub_signals | A list of public inputs was utilized in the generation of the Zero-Knowledge Proof (ZKProof). | list of strings | ✅ |

The `scope` field contains a list of zero-knowledge proofs and public inputs for authorization on a resource. More about scope contnet: https://github.com/iden3/go-circuits

- **Example of proof response:**
    
    ```json
    {
      "id": "7f38a193-0918-4a48-9fac-36adfdb8b542",
      "typ": "application/iden3comm-plain-json",
      "type": "https://iden3-communication.io/proofs/1.0/response",
      "thid": "7f38a193-0918-4a48-9fac-36adfdb8b542",
      "body": {
        "scope": [
          {
            "id": 1,
            "circuitId": "credentialAtomicQueryMTPV2",
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
      "to": "did:polygonid:polygon:mumbai:2qJUZDSCFtpR8QvHyBC4eFm6ab9sJo5rqPbcaeyGC4",
      "from": "did:iden3:polygon:mumbai:x3HstHLj2rTp6HHXk2WczYP7w3rpCsRbwCMeaQ2H2"
    }
    ```
