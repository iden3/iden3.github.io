
type: `/revocation/1.0/status`

The message regarding the revocation status. This message has information about MTP proof and information about the issuer state that was used for generating this proof.

```json
{
	"issuer": {
		"state": "<issuer_state>",
		"rootOfRoots": "<issuer_root_of_roots_tree_root",
		"claimsTreeRoot": "<issuer_claim_tree_root>",
		"revocationTreeRoot": "<issuer_revocation_tree_root>"
	},
	"mtp": "<obj_with_mtp_proof>"
}
```

| Field | Description | Type | Required |
| --- | --- | --- | --- |
| info.issuer.state | Issuer state | string | ✅ |
| issuer.rootOfRoots | Issuer root of roots tree root | string | ❌ |
| issuer.claimsTreeRoot | Issuer claim tree root | string | ✅ |
| issuer.revocationTreeRoot | Issuer revocation tree root | string | ❌ |
| mtp | Merkle tree proof. This proof for exists or non-exists revocation nonce in issuer`s revication tree | *object | ✅ |

More about `mtp` field: [https://github.com/iden3/claim-schema-vocab/blob/main/proofs/SparseMerkleTreeProof.md](https://github.com/iden3/claim-schema-vocab/blob/main/proofs/SparseMerkleTreeProof.md)

- **Example of revocation status response:**
    
    ```json
    {
      "id": "f4b6f1a3-ebf4-49a7-8c2d-5d2649b1e65d",
      "typ": "application/iden3comm-plain-json",
      "type": "https://iden3-communication.io/revocation/1.0/status",
      "from": "11tbD2cY9ZuZc8oQWN5bhtvNVrqmf1zdnES3emJET",
      "to": "118he3vAmZTWPaD7cyFYKz8ztjXceRGBPYgiuz8CQX",
      "body": {
        "issuer": {
          "claims_tree_root": "29570142accabef4e58cbdcd38b0ecb22bb9b75ef19503dc47986c2f3aec4712",
          "revocation_tree_root": "0000000000000000000000000000000000000000000000000000000000000000",
          "root_of_roots": "a5ec315235e69f56080d21ac4b85986cdfa51b90667d496234de1ba48bbe020f",
          "state": "c8097eb17e33ef531c9de363f20167c88c09d0ca7ab9ce57b27fecb451b1c320"
        },
        "mtp": {
          "existence": false,
          "siblings": []
        }
      }
    }
    ```
