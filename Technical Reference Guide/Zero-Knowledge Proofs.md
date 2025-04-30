# Zero Knowledge Proofs

   A zero-knowledge proof (ZKP) is a cryptographic protocol that allows
one party (the prover) to demonstrate to another party (the verifier)
that a statement is true without revealing any (potentially secret)
information. Besides the fact that the statement is true, ZKP can be
*interactive*, where back-and-forth interaction is required between the
prover and the verifier, or *non-interactive*, where the prover
generates the proof and sends it to the verifier, who can check it
independently [[1]](#1)[[2]](#2)[[3]](#3).

ZKP facilitates privacy compliance by minimising the disclosure of data.
ZKP enhances security by allowing information that is considered
confidential, such as actual age in some cases, to remain undisclosed to
other parties [[1]](#1). ZKP focus on proving specific statements while
disclosing minimal information, offering three key properties:
completeness (ensuring acceptance of true statements), soundness
(rejection of false statements), and zero-knowledge (preservation of
confidentiality during verification) [[4]](#4)[[5]](#5).

## Current and potential applications

   Current applications of ZKP include age verification without
revealing the birth date, asset ownership verification without revealing
past transactions, and support for biometric authentication methods on
mobile devices [[1]](#1)[[5]](#5). ZKP is also used in cryptocurrency
transactions, allowing encrypted transactions to be added to ledgers
while proving their compliance with ledger policies, such as preventing
double-spending attacks. ZeroCash [[6]](#6) is a protocol providing a
privacy-preserving version of Bitcoin and was among the pioneers in
adopting ZKP. Furthermore, ZKP can be used in authentication systems,
where a user needs to prove their identity without revealing their
password or other secret information, and electronic
voting [[7]](#7). ZKP is gaining traction in authentication systems
like Direct Anonymous Attestation [[8]](#8), where they safeguard
authentication credentials by allowing the holder of a credential to
create unlinkable ZKP each time they present the credential.

ZKPs can be used to prevent cheating in computations on encrypted data
in the context of homomorphic encryption [[9]](#9). For
example, a service provider could exploit this by altering computations
based on encrypted input data, but ZKPs can audit these computations and
confirm that they were done honestly. Similarly, in multi-party
scenarios such as auctions or elections, ZKPs can ensure that
participants don't manipulate or duplicate inputs.

In machine learning, ZKPs can verify that a model has been trained
correctly and that the results are legitimate, ensuring the integrity of
the process without exposing the data itself. This can also be extended
to non-ML computations, where proofs of the inputs or processes can be
published or validated, creating an audit trail similar to signed
software binaries [[9]](#9).

## Efficiency and parameters

   ZKP systems have various costs to consider, including efficiency in
proof generation and verification, proof size, number of rounds,
parameter loading, and the need for interaction between the prover and
verifier [[5]](#5). For instance, *Succinct Non-Interactive
Argument* (SNARKs) systems offer small constant-sized proofs with
efficient verification, but they require significant computation
overhead for the prover. Other types of ZKP systems may require
interaction between the prover and verifier or have longer proofs, but
they often impose less overhead on the prover, which can be advantageous
when the prover's computation is the application's bottleneck [[4]](#4).

## Primitives and algorithms

   ZKP relies on cryptographic primitives and algorithms to validate
statements without revealing additional information. *Commitment
schemes* allow parties to commit to a value without disclosing it until
later, ensuring both integrity and confidentiality. However, they often
face a trade-off between the binding and hiding properties, can be
computationally intensive, and may involve large commitments, affecting
efficiency. Another primitive is *Bilinear pairings*, which involves
mathematical operations on groups that allow efficient cryptographic
computations. These pairings are integral to advanced cryptographic
constructions, including *zk-SNARKs* (Zero-Knowledge Succinct
Non-Interactive Argument of Knowledge) and *zk-STARKs* (Zero-Knowledge
Scalable Transparent ARguments of Knowledge). Nonetheless, bilinear
pairings rely on hard mathematical problems for security making it
computationally expensive [[7]](#7).

The *Fiat-Shamir heuristic* is a transformative algorithm that converts
interactive proof systems into non-interactive ones, making ZKP more
practical for real-world applications. This heuristic simulates the
interaction between a prover and a verifier while preserving the
security properties of the original protocol. However, its reliance on
the random oracle model can introduce security issues when replaced with
hash functions. The *Fiat-Shamir heuristic* is particularly significant
in the context of zk-SNARKs and zk-STARKs. zk-SNARKs require a trusted
setup phase, which, if compromised, can undermine the security of the
entire system. Generating and verifying zk-SNARKs can be computationally
expensive, and the size of the proofs, though succinct, may still be
limited in systems with stringent storage or bandwidth constraints.
zk-STARKs enhance efficiency by eliminating the need for a trusted setup
and interaction between parties, but they typically produce larger
proofs and have significant computational overhead. Additionally,
*Bulletproofs* provide an efficient zero-knowledge range proof system
without requiring a trusted setup because of their small proof sizes and
efficient verification. This is valuable for blockchain and distributed
ledger technologies, providing secure and practical zero-knowledge range
proofs. Despite their small proof sizes, Bulletproofs have longer
verification times compared to zk-SNARKs and involve complex
cryptographic operations, which can challenge scalability in
high-frequency use cases [[7]](#7).

## Limitations

   The following limitations underline the need for careful
consideration and evaluation when using ZKP in different
applications [[2]](#2)[[4]](#4):

- **Complexity:** Human problems are hard to translate into a
  mathematically proven statement under a given scheme. The
  cryptographic tools used in ZKPs themselves are built on advanced
  mathematical concepts.

- **Efficiency:** ZKP is only efficient for simple proof statements,
  like transaction statements. More complex statements such as which
  properties are present in a software are not possible yet.

- **Concurrency:** ZKP may not guarantee the preservation of security
  properties in concurrent executions, where many proofs are being
  executed at the same time.

- **Use cases:** While ZKPs have found niche applications in
  cryptocurrency contexts, the broader landscape offers substantial
  opportunities for expansion and development.


### References
<a id="1">[1]</a> 
Information Comissioner’s Office, “Privacy-enhancing technologies (PETs),”
https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/data-
sharing/privacy-enhancing-technologies/ (Last accessed on May, 2024), 2023.

<a id="2">[2]</a> 
OECD, “Emerging privacy-enhancing technologies: Current regulatory and policy
approaches,” no. 351, p. 51, 2023.

<a id="3">[3]</a> 
European Union Agency for Cybersecurity, M. Adamczyk, P. Drogkaris, “Data
protection engineering: from theory to practice.” ENISA, Tech. Rep. January, 2022.

<a id="4">[4]</a> 
United Nations, United Nations Guide on Privacy-Enhancing Technologies for
Official Statistics, 2023.

<a id="5">[5]</a> 
D. Benarroch and L. Brand˜ao and M. Maller and E. Tromer, ZKProof Community
Reference, 2022.

<a id="6">[6]</a> 
E. B. Sasson, A. Chiesa, C. Garman, M. Green, I. Miers, E. Tromer, and M. Virza,
“Zerocash: Decentralized Anonymous Payments from Bitcoin,” in 2014 IEEE
Symposium on Security and Privacy, 2014.

<a id="7">[7]</a> 
E. Morais, T. Koens, and A. K. C. van Wijk, “A survey on zero knowledge range
proofs and applications,” SN Applied Sciences, vol. 1, p. 946, 2019.

<a id="8">[8]</a> 
T. Zoo, “Direct anonymous attestation,” https://tokenzoo.github.io/ (Last accessed on May, 2024).

<a id="9">[9]</a> 
K. Jarmul, Practical Data Privacy. O’Reilly Media, Inc., 2023.


