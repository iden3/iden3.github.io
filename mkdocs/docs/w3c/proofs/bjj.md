This specification describes the BabyJubjub 2021 Signature Suite, created in 2021 for the Verifiable Credentials Data Integrity Proof specification. The Signature Suite is designed to be zk-friendly, allowing the implementation of an additional security layer that can offer enhence privacy through zero-knowledge signature proofs.

This document is a draft specification developed by 0kims association and is provided for public review and feedback. The current version of the document is a work in progress and may be subject to changes or updates based on community input, technical advancements, or further research. The specification has not yet been submitted to, reviewed, or approved by any formal standards organization such as the W3C. However, it is intended to align closely with the existing W3C recommendations, specifications, and best practices related to decentralized identifiers, verifiable credentials, and digital signatures.

##Introduction
------------

This specification presents the BabyJubjub 2021 Signature Suite. The suite employs EdDSA on the BabyJubJub curve as the signature algorithm, providing an efficient structure for signing and verifying credentials while being zk-friendly. Although the signature suite itself does not actively involve zero-knowledge proofs, its design is conducive to privacy-preserving computations and can be easily integrated with zkSNARKs and other zero-knowledge proof systems. This document details the components, structure, and implementation guidance for the BabyJubjub 2021 Signature Suite, catering to developers, implementers, and users.

##Terminology
-----------
The following terms are used to describe concepts involved in the generation and verification of the Linked Data Proof signature suite.

??? terms

    **signature suite**
    
    A specified set of cryptographic primitives typically consisting of a canonicalization algorithm, a message digest algorithm, and a signature algorithm that are bundled together by cryptographers for developers for the purposes of safety and convenience.
    
    **canonicalization algorithm**
    
    An algorithm that takes an input document that has more than one possible representation and always transforms it into a canonical form. This process is sometimes also called normalization.
    
    **message digest algorithm**
    
    An algorithm that takes a message, preferably in some canonical form and produces a cryptographic output called a digest that is often many orders of magnitude smaller than the input message. These algorithms are often 1) very fast, 2) non-reversible, 3) cause the output to change significantly when even one bit of the input message changes, and 4) make it infeasible to find two different inputs for the same output.
    
    **canonical form**
    
    The output of applying a canonicalization algorithm to an input document.
    
    **signature algorithm**
    
    An algorithm that takes an input message and produces an output value where the receiver of the message can mathematically verify that the message has not been modified in transit and came from someone possessing a particular secret.
    
    **linked data document**
    
    A document comprised of linked data.
    
    **linked data proof**
    
    A [proof](https://www.w3.org/TR/vc-data-integrity/#proofs) which is a set of attributes that represent a linked data digital proof and the parameters required to verify it as defined by RDF-N-Quads.
    
    **linked data proof document**
    
    A linked data document featuring one or more linked data proofs.
    
    **BJJSignature2021**
    
    The `type` of the linked data proof for the signature suite BabyJubjub 2021.
    
    **Iden3StateInfo2023**
    
    The `type` representing state information, a method for maintaining the issuer's state information and validating proofs against this data to ensure secure and efficient identity management within decentralized systems.**


Suite Definition
----------------

The BabyJubjub 2021 signature suite MUST be used in conjunction with the signing and verification algorithms in the Linked Data Signatures [specification](https://w3c.github.io/vc-data-integrity/). The suite consists of the following algorithms:


| Parameter      | Value                              | Specification                                                                                                                                                              |
| ----------- |------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| canonicalizationAlgorithm      |  https://w3id.org/security#URDNA2015 | [RDF Dataset Normalization 1.0](https://www.w3.org/TR/rdf-canon/)                                                                                                          |
| digestAlgorithm     | Poseidon | [POSEIDON: A New Hash Function for Zero-Knowledge Proof Systems](https://eprint.iacr.org/2019/458.pdf)                                                                     |
| signatureAlgorithm|  EdDSA-BabyJubJub | [EdDSA For Baby Jubjub Elliptic Curve with MiMC-7 Hash](https://iden3-docs.readthedocs.io/en/latest/_downloads/a04267077fb3fdbf2b608e014706e004/Ed-DSA.pdf)                |

### Modification to Algorithms

The hash function in the signature algorithm has been repleaced to [Poseidon](https://eprint.iacr.org/2019/458.pdf) hash function.

### Document Merklization Algorithm


The signature suite incorporates a Document Merklization algorithm to provide enhanced zero-knowledge compatibility support. This feature enables efficient querying of individual entries within JSON-LD documents in the context of zk-SNARK proofs. By constructing a Sparse Merkle Tree from the document, the algorithm supports selective disclosure of Verifiable Credential (VC) entries, efficiently prove membership, non-membership, and other predicate satisfactions related to the JSON-LD document, while maintaining the privacy and integrity of the data.

Prior to applying the Merklization algorithm, the document must be in its expanded and canonicalized form.

The Merklization algorithm works as follow:

1.  Obtain a list of RDF Quads from the canonicalized document.
2.  For each Quad, construct a key-value pair where the key represents the complete type path, and the value corresponds to the entry's value.
3.  Insert each key-value pair into the Merkle Tree, with the key serving as the path in the tree and the leaf's value being the hash of the pair's value, computed using the designated message digest algorithm.
4.  For each key-value pair, first hash the key using the designated message digest algorithm, and use the hashed key as the path in the Merkle Tree. Then, hash the value using the same message digest algorithm, and set the resulting hash as the value of the corresponding leaf node in the tree.

Supported ld data types for merklization:

??? datatypes


    1. xsd:integer ( from prime / 2 to prime / 2)
    2. xsd:positiveInteger ( from 1 to prime)
    3. xsd:string ( sponge hash of string bytes)
    4. xsd:double ( Canonical representation IEEE is hashed as string )
    5. xsd:nonNegativeInteger ( from 0 to prime)
    6. xsd:negativeInteger  (from -prime to -1)
    7. xsd:datetime (nanoseconds of unix timestamp, date after 1970-01-01 is supported )
    8. xsd:boolean (Poseidon hash of 1 or 0) 

    prime number is specific to each hash algorithm, for current Poseidon it is `21888242871839275222246405745257275088548364400416034343698204186575808495617`

More about jsonld merklization can be found [here](https://docs.iden3.io/w3c/merklization/#conclusion). 
  

#### Field proof example

To better comprehend how the signature suite enables field proof, let us examine the underlying mechanism. 
In this process, a credential undergoes Merklization, during which each entry of the document is stored in a leaf.
Subsequently, the merkle root of jsonld document as a part of core claim representation is signed by the issuer. 
To facilitate the proof check, the prover can share the following information with the verifier:

1.  The core claim representation of the verifiable credential.
2.  The issuer's signature on the of it.
3.  The relevant authentication paths for the proving the validity of the issuer key.

By providing this information, the prover demonstrates the possession of a valid credential containing specific entries without revealing the entire credential content. Consequently, this enables the prover to confirm the issuance of a credential of a particular type that contains specific values while preserving the confidentiality of other credential details. This approach aligns with W3C's official specifications and ensures data privacy during the verification process.

### BJJSignature2021

All verifiable credentials issued with the BabyJubjub 2021 signature suite must include a proof object with "BJJSignature2021" as the proof type. The BJJSignature2021 proof contains the issuer's data, the core claim, and a signature created using the issuer's private key. The following example demonstrates a BJJSignature2021 proof:


        {
            "type": "BJJSignature2021",
            "issuerData": {
                "id": "did:polygonid:polygon:mumbai:2qHHBynUfh5UU7VimmwCT7MUtBhEcxXLm8ucEpkNMA",
                "state": {
                    "claimsTreeRoot": "c40193ee97ce84705e63b7989fc303dde5a0f1e5648568cfafea37393728aa15",
                    "value": "1a76fb92056a01afa69f8d1181b25079be70024e81fb48c3c25fdc5d8887a326"
                },
                "authCoreClaim": "cca3371a6cb1b715004407e325bd993c000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000d9780102f9811e3efdade2afc5af9b5385a8f889a6b56ba8508c9896daf8040700623c34180136b3316f5012721f456ac2560e35acf53b32bf8b4de595f2b1170000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
                "mtp": {
                    "existence": true,
                    "siblings": []
                },
                "credentialStatus": {
                    "id": "http://example.com/v1/did%3Apolygonid%3Apolygon%3Amumbai%3A2qHHBynUfh5UU7VimmwCT7MUtBhEcxXLm8ucEpkNMA/claims/revocation/status/0",
                    "revocationNonce": 0,
                    "type": "SparseMerkleTreeProof"
                }
            },
            "coreClaim": "19ad4768b6f32694530c34cc187260702a0000000000000000000000000000000212b146402879cb0c89aee16ee6f3433f440c552c0559f0e50ee57f223c0c0002124436c8baf3d426bb6a9b32870cbc090174521431f29f3d2280a7aeca302f0000000000000000000000000000000000000000000000000000000000000000dfd04e04000000005f9b83650000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
            "signature": "cc917d9f4cf89b57b23228dbdced7a052619457f29123b09e2bd9d4bef9cf70e5bda110c9baa3756cf6ad6e76030c9b802e55c617be35aafdd3e261e12c08f00"
        }

Where: 

   *  `coreClaim` is a signed hex of core claim representation of W3C credential.
   * `signature` is a hex value of BJJ compressed signature produced by the issuer public key.
   *  The issuer stores their public key in the state tree. In proof it is represented a `authCoreClaim` hex in the `issuerData` property. `mtp` property contains merkle tree proof of inclusion to the issuer claims tree.
   *  `issuerData` contains information about how to check the credential status of the issuer key. More details regarding `credentialStatus` can be found [here](../status/overview.md).
   * `state` object represents the roots of issuer's trees  at the time of auth key has been issued.


The proof contains the signature of the coreClaim which is a serialization of the whole VC document except for the proof. The signature is created using the issuer's private key.

#### Proof Generation

The BJJSignature2021 proof generation process follows a specific algorithm to ensure the integrity and authenticity of JSON-LD documents. The steps of the algorithm are as follows:

1.  Expand the JSON-LD document using the [JSON-LD 1.1 Processing Algorithms.](https://www.w3.org/TR/json-ld11-api/#expansion)
2.  Canonicalize the document using the URDNA2015 algorithm.
3.  Apply the [Document Merklization Algorithm](https://docs.iden3.io/w3c/merklization/#conclusion) to create a Merkle tree from the canonicalized document.
4.  Create a core claim representation from W3C credential according to the core protocol. Document Root is written into one of the data slots.
5.  Sign the hex of core claim using the associated private key.




To see an example of Iden3StateInfo2023 object in a DID document, please refer to the [example](#did-document) provided in the Examples section of this document.

#### Proof Verification

During the verification of the verifiable credential, the verifier must check not only the signature of credential but also that the public key used to sign the document. 


To verify the authenticity and integrity of signature, the following steps should be performed:

1.  Retrieve the issuer's DID document and locate the Iden3StateInfo2023 object [issuer did document example](#did-document) containing the state root and other relevant information. Check that state value in proof is published onchain or is genesis one.
2.  Verify that the issuer's public key, which signed the document, has been included in requested state with merkletree proof generation
3.  Obtain the core claim of the Merkleized credential, the issuer's signature on it from proof object.
4.  Validate the issuer's signature on the VC root using the issuer's public key.
5.  Validate that issuer's public key is not revoked. 
6.  Obtain the root of the Merklized credential from the `coreClaim`. see [documentation](https://docs.iden3.io/w3c/merklization/)
7.  Reconstruct the Merkle tree root of credential using the json ld merklization procedure and compare with an extracted root  the `coreClaim`.

#### Implementations

[Golang](https://github.com/iden3/go-schema-processor/blob/4490032d21c0a3faf5c546666058cd90d1a3f81b/verifiable/credential.go#L39)
[JS](https://github.com/0xPolygonID/js-sdk/blob/ff5663b8c974268cb8d2dc683993610292babc0a/src/verifiable/credential.ts#L152)

######  resolved did document of issuer
??? example

        {
            "@context": [
            "https://www.w3.org/ns/did/v1",
            "https://schema.iden3.io/core/jsonld/auth.jsonld"
            ],
            "id": "did:polygonid:polygon:mumbai:2qFGtDk2SyTLJgUx576mn2peqeFtWmhsSvWLoAnom4",
            "verificationMethod": [
                {
                    "id": "did:polygonid:polygon:mumbai:2qFGtDk2SyTLJgUx576mn2peqeFtWmhsSvWLoAnom4#stateInfo",
                    "type": "Iden3StateInfo2023",
                    "controller": "did:polygonid:polygon:mumbai:2qFGtDk2SyTLJgUx576mn2peqeFtWmhsSvWLoAnom4",
                    "stateContractAddress": "80001:0x134B1BE34911E39A8397ec6289782989729807a4",
                    "published": true,
                    "info": {
                        "id": "did:polygonid:polygon:mumbai:2qFGtDk2SyTLJgUx576mn2peqeFtWmhsSvWLoAnom4",
                        "state": "78d9e333fbede1722f53a6a059cba0b36c0ee62f60871f0d1761eda0aeb5b928",
                        "replacedByState": "0000000000000000000000000000000000000000000000000000000000000000",
                        "createdAtTimestamp": "1707399475",
                        "replacedAtTimestamp": "0",
                        "createdAtBlock": "45691433",
                        "replacedAtBlock": "0"
                    },
                    "global": {
                        "root": "61c52f21698f424e473113723729e28c9c895360b78c930a97875da04ef4242f",
                        "replacedByRoot": "0000000000000000000000000000000000000000000000000000000000000000",
                        "createdAtTimestamp": "1707418701",
                        "replacedAtTimestamp": "0",
                        "createdAtBlock": "45700072",
                        "replacedAtBlock": "0"
                    }
                }
            ]
        }

