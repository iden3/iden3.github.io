This specification describes the Iden3SparseMerkleTreeProof Signature Suite, created in 2021 for the Verifiable Credentials Data Integrity Proof specification.
The Signature Suite is designed to be zk-friendly, allowing the implementation of an additional security layer that can offer enhence security based in merkle tree data structures. 
This document is a draft specification developed by ZK Labs and is provided for public review and feedback. The current version of the document is a work in progress and may be subject to changes or updates based on community input, technical advancements, or further research. The specification has not yet been submitted to, reviewed, or approved by any formal standards organization such as the W3C. However, it is intended to align closely with the existing W3C recommendations, specifications, and best practices related to decentralized identifiers, verifiable credentials, and digital signatures.

##Introduction
------------
This specification presents the Iden3 Sparse Merkle Tree Signature Suite. The suite employs a novel technique for proving and verifying credentials while being zk-friendly.
Although the signature suite itself does not actively involve zero-knowledge proofs, its design is conducive to privacy-preserving computations and can be easily integrated with zkSNARKs and other zero-knowledge proof systems. 
This document details the components, structure, and implementation guidance for the Iden3 Sparse Merkle Tree Signature Suite, catering to developers, implementers, and users.

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

    Iden3SparseMerkleTreeProof
    
    The `type` of the linked data proof for the Iden3 Sparse Merkle Tree Signature Suite.
     
    **Iden3StateInfo2023**
    
    The `type` representing state information, a method for maintaining the issuer's state information and validating proofs against this data to ensure secure and efficient identity management within decentralized systems.**


Suite Definition
----------------

The BabyJubjub 2021 signature suite MUST be used in conjunction with the signing and verification algorithms in the Linked Data Signatures [specification](https://w3c.github.io/vc-data-integrity/). The suite consists of the following algorithms:


| Parameter      | Value                               | Specification                                                                                                                                            |
| ----------- |-------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| canonicalizationAlgorithm      | https://w3id.org/security#URDNA2015 | [RDF Dataset Normalization 1.0](https://www.w3.org/TR/rdf-canon/)                                                                                        |
| digestAlgorithm     | Poseidon                            | [POSEIDON: A New Hash Function for Zero-Knowledge Proof Systems](https://eprint.iacr.org/2019/458.pdf)                                                   |
| signatureAlgorithm| SMT proof                           | [Inclusion of core claim info to Issuer merkle tree](https://docs.iden3.io/getting-started/mt/) |

### Modification to Algorithms

The hash function in the signature algorithm has been repleaced to [Poseidon](https://eprint.iacr.org/2019/458.pdf) hash function.

### Document Merklization Algorithm

More about jsonld merklization can be found [here](../bjj.md#Document Merklization Algorithm).


### Iden3SparseMerkleTreeProof

All verifiable credentials issued with the Iden3 Sparse Merkle Tree Signature Suite must include a proof object with "Iden3SparseMerkleTreeProof" as the proof type.
The Iden3SparseMerkleTreeProof contains the `issuerData`, `coreClaim`, and the `mtp` (the merkle tree proof of inclusion of the core claim to the issuer claim tree root) of the relevant credential in the issuer's state tree. The following example demonstrates a Iden3SparseMerkleTree proof:

            {
                "type": "Iden3SparseMerkleProof",
                "issuerData": {
                    "id": "did:iden3:polygon:mumbai:wz7EXpsG9jdQC4edi3kyXC5SroZfqbcPKTYaJc5t6",
                    ...
                },
                "coreClaim": "c9b2370371b7fa8b3dab2a5ba81b68382a00000000000000000000000000000001129e344820de5301d7ae7f88ba5143f4ab9a9506e82331ec7ae8b21a830d006059621a4a3ed91795fc7919557e41c793ddbe93a30bc970f005cc72f89760270000000000000000000000000000000000000000000000000000000000000000c913b95700000000281cdcdf0200000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
                "mtp": {
                    "existence": true,
                    "siblings": [
                        "12337778158204247406578936191019732894620603082018578837880614994697897821924",
                        "0",
                        "0",
                        "0",
                        "21666974695683480301917255007901264320661483352297531017037182795057172235134"
                    ]
                }
            }

The claim gets added to the issuer’s state. This action modifies the structure of the Merkle Tree and, therefore, the state has to be updated with the new Merkle root. The proof of issuance is the inclusion of the claim iself inside the issuer’s Claims Tree.

#### Proof Generation


The Iden3SparseMerkleTreeProof proof generation process follows a specific algorithm to ensure the integrity and authenticity of JSON-LD documents. The steps of the algorithm are as follows:

1.  Expand the JSON-LD document using the [JSON-LD 1.1 Processing Algorithms.](https://www.w3.org/TR/json-ld11-api/#expansion)
2.  Canonicalize the document using the URDNA2015 algorithm.
3.  Apply the [Document Merklization Algorithm](https://docs.iden3.io/w3c/merklization/#conclusion) to create a Merkle tree from the canonicalized document.
4.  Create a core claim representation from W3C credential according to the core protocol. Document Root is written into one of the data slots.
5.  Add the core claim hash index and hash value  to issuer’s tree state and update the state accordign to the protocol [rules](https://docs.iden3.io/getting-started/mt/)


#### Proof Verification


To verify the authenticity and integrity of the credential, the following steps should be performed:

1.  Retrieve the issuer's DID document and locate the Iden3StateInfo2023 object [issuer did document example](../#did-document) containing the state root and other relevant information. Check that state value in proof is published onchain or is genesis one.
2.  Check the validity of mtp proof of  the `coreClaim`, which has been included in the requested state with merkletree proof generation.
3.  Obtain the root of the Merklized credential from the `coreClaim`. see [documentation](https://docs.iden3.io/w3c/merklization/)
4.  Reconstruct the Merkle tree root of credential using the json ld merklization procedure and compare with an extracted root  the `coreClaim`.

#### Implementations

[Golang](https://github.com/iden3/go-schema-processor/blob/4490032d21c0a3faf5c546666058cd90d1a3f81b/verifiable/credential.go#L39)
[JS](https://github.com/0xPolygonID/js-sdk/blob/ff5663b8c974268cb8d2dc683993610292babc0a/src/verifiable/credential.ts#L152)
