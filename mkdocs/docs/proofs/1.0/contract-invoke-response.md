
type: `/proofs/1.0/contract-invoke-response`

Response to contract invoke request with a zero-knowledge proof that could be sent or not.
In case proof response has been sent, then txHash property MUST be included to scope object of the generated proof. 


```json
{
  	"did_doc": "<did_doc>",
	"scope": ["<generated zero knowledge proofs with or without txHash>"],
	"transaction_data": "{<information_about_smart_contract>}"
}
```

| Field                             | Description                                                                        | Type             | Required |
|-----------------------------------|------------------------------------------------------------------------------------|------------------|----------|
| did_doc                           | Resource did doc                                                                   | JSON             | ❌        |
| scope                             | List of objects with zkpoorf and public inputs                                     | list of objects  | ✅        |
| scope.id                          | Unique id to present unique authorization request                                  | uint32           | ✅        |
| scope.circuitId                   | Information that circuit was used for generating zk proof                          | string           | ✅        |
| scope.vp                          | Information that user wants to disclosure                                          | JSON             | ❌        |
| scope.txHash                      | transaction hash if proof is sent to chain                                         | JSON             | ❌        |
| scope[i].proof                    | zero-knowledge proof                                                               | JSON             | ✅        |
| scope[i].pub_signals              | A list of public inputs was utilized in the generation of the Zero-Knowledge Proof | list of strings  | ✅        |
| transaction_data.contract_address | Smart contract address                                                             | string           | ✅        |
| transaction_data.method_id        | Smart contract method (function signature                                          | string           | ✅        |
| transaction_data.chain_id         | Chain identification                                                               | string           | ✅        |
| transaction_data.network          | Chain network                                                                      | string           | ✅        |

- **Example of contract invoke response:**
    
    ```json
    {
      "id": "f8aee09d-f592-4fcc-8d2a-8938aa26676c",
      "typ": "application/iden3comm-plain-json",
      "type": "https://iden3-communication.io/proofs/1.0/contract-invoke-response",
      "thid": "f8aee09d-f592-4fcc-8d2a-8938aa26676c",
      "from": "did:polygonid:polygon:mumbai:2qFroxB5kwgCxgVrNGUM6EW3khJgCdHHnKTr3VnTcp",
      "body": {
    	  "transaction_data": {
    			"contract_address": "0x13d67dc5f3ef3f5327b60b824d66f27c9b03316862ec27a330ccab5ea3b28cc1",
    			"method_id":"b68967e2",
    			"chain_id": 80002,
    			"network": "polygon-amoy"
    	  },
          "scope": [
           {
            "id": 1,
            "circuitId": "credentialAtomicQuerySigV2",
            "txHash": "0xe826f870852d7eeeb79b2c030298f9b5daa8c8a3",
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
          }]
      }
    }
    ```
