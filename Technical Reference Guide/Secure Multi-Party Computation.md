# Secure Multi-party Computation

   Secure Multi-Party Computation (SMPC) is a cryptographic technique
that allows multiple parties to jointly compute functions over their
private input data without revealing the data to each other or relying
on a trusted third
party [[1]](#1)[[2]](#2)[[3]](#3)[[4]](#4). It
addresses concerns about input privacy and code assurance by allowing
computation over data while preventing participants from learning
anything beyond the computation's output. Additionally, sMPC ensures
that the function computed on the data aligns with the agreed-upon
function by the parties involved [[5]](#5). *Private set intersection*
is a specific type of SMPC that allows two parties to compute the
intersection of their private sets without revealing any other
information about their
sets [[4]](#4)[[6]](#6)[[7]](#7).

SMPC assumes the presence of mutually distrusting parties, introducing a
new class of adversaries that may control one or more participants in
the computation. These adversaries are categorised based on *honesty*,
*mobility*, and the *proportion of compromised compute parties*. The
*honesty model* ranges from *semi-honest* to malicious adversaries, each
with varying degrees of intent permitted
actions [[4]](#4)[[5]](#5)[[6]](#6)[[8]](#8).
*Semi-honest* adversaries are restricted to inspecting data and have
full knowledge of the computational process. They execute the protocol
as specified, but attempt to learn private information by observing
protocol interactions, often pooling the views of colluding corrupt
parties. *Covert* adversaries can manipulate protocols while aiming to
remain undetected, whereas *malicious* adversaries operate openly, with
no regard for concealment.

Security for these adversaries is formally defined using a real-ideal
paradigm, where security guarantees depend on proving that adversary
actions in the real world are indistinguishable from the ideal world.
Semi-honest adversaries rely on a simulator that reconstructs a view
equivalent to real-world computation. Malicious adversaries require the
simulator to additionally extract inputs for corrupt parties to
replicate their influence on the ideal world.

*Dynamic* adversaries add significant complexity to protocol design
because security assumptions must adapt to adversarial changes
mid-computation. *Mobility* refers to the ability of the adversary to
move between participants during computation, with stationary and
dynamic adversary models considered. Additionally, SMPC adversary
assumptions are divided into *honest majority*, which prioritise
ensuring the correctness and fairness of outputs for the honest parties,
and *dishonest majority* classes, which aim for security with abort,
allowing computation to abort upon detection of adversarial behaviour.

SMPC protocols often rely on indistinguishability from an idealized
scenario where all compute parties send their inputs to a trusted
broker. The number of compromised parties varies depending on the
protocol, with higher defence proportions typically resulting in
increased protocol overheads. Clear communication of the honesty model
is essential to assess its suitability for the intended purpose of
encryption as a risk mitigator.

## Current and potential applications

SMPC enables the sharing of individually identifiable data between
government agencies to calculate statistics and make policy decisions
while maintaining data confidentiality. For example, multiple agencies
in a county government in the USA collaborated to compute answers to
queries about individuals' use of mental health services or public
housing, while maintaining the confidentiality of personal identifiers
and data. For instance, the Italian National Institute of Statistics and
the Bank of Italy used SMPC to perform analytics on joint subsets of
individuals identified by unique tax codes without directly sharing
sensitive data, such as age and mortgage information [[5]](#5).

SMPC can also improve fairness and privacy in auctions, such as
sealed-bid auctions [[4]](#4). It ensures that bids remain
private and protected from manipulation, as demonstrated in the Danish
sugar beet auction [[9]](#9).

SMPC can be used for electronic voting [[4]](#4)[[10]](#10)
or biometric identification [[11]](#11), secure machine
learning [[4]](#4), and is used in blockchain technology to
allow a group of parties, known as *miners*, to collaboratively
determine and reach consensus on the next block to be added to the
blockchain ledger [[12]](#12).

SMPC has also been applied to privacy-preserving network security
monitoring, genomic data analysis, stable matching, contact discovery,
ad conversion, spam filtering in encrypted email, and pay equity
studies [[4]](#4). For example, the Boston Wage Equity
Study [[13]](#13) demonstrated how SMPC can support social initiatives
without compromising sensitive salary information.

## Efficiency and parameters

   The efficiency of SMPC is influenced by the number of parties
involved, the level of security (e.g., cryptographic key sizes), network
bandwidth, and the specific protocol used. These protocols often involve
intensive cryptographic operations such as encryption, decryption and
secure function evaluation, which contribute to the computational
overhead. Communication complexity is another factor, as SMPC protocols
typically require multiple rounds of interaction between the parties,
impacting latency and bandwidth usage. Two-party protocols are typically
more efficient than multi-party protocols. In addition, the type of
adversary (semi-honest or malicious) affects efficiency, with protocols
that are secure against malicious adversaries requiring more resources.

In SMPC, a typical metric for performance is *computational slowdown*,
which is the ratio of the latency of computation in SMPC to the latency
of computation done without SMPC security. The performance is often
benchmarked via metrics such as the number of rounds of communication,
the volume of data communicated, and the complexity or latency of the
computation involved [[5]](#5). Emerging hardware accelerators, such as
GPUs and TPUs, are being explored to reduce these performance
bottlenecks by speeding up cryptographic
primitives [[6]](#6).

## Primitives and algorithms

   SMPC relies on several cryptographic primitives to ensure secure and
private computations, primarily using two main technologies: *circuit
garbling* and *linear secret sharing (LSS)*. Circuit
garbling [[5]](#5)[[14]](#14), typically used for two-party computations,
involves one party (the garbler) encrypting a logic circuit and the
other party (the evaluator) computing on this encrypted circuit without
revealing the actual values, allowing secure function evaluation. The
main limitation is the high computational and memory overhead associated
with creating and evaluating garbled circuits, making it prohibitive for
complex functions.

LSS [[5]](#5)[[10]](#10) is suitable for multiple parties and involves
dividing data into random shares which are distributed to computing
parties who then perform computations on the shares. This method ensures
that the secret can only be reconstructed when a sufficient number of
shares are combined, solving the problem of securely distributing
sensitive information. Techniques such as batched computations and
efficient share management have addressed the challenges of
communication overhead and improved scalability. Open-source
implementations such as ABY and EZPC combine these methods to balance
efficiency and functionality.

In addition, *random oracles* [[4]](#4) cast hash functions as
idealised random functions. This abstraction simplifies the design of
cryptographic protocols, in particular by enabling efficient commitment
schemes and zero-knowledge proofs. Despite being a heuristic, the random
oracle model is widely used because of its practical efficiency.

*Commitment schemes* [[4]](#4) are another basic primitive
that allow a sender to commit to a secret value and reveal it later.
These schemes ensure that the secret remains hidden until revealed
(*hiding*) and cannot be changed after commitment (*binding*). Simple
constructions using hash functions, often based on the random oracle
model, make commitments lightweight and efficient for use in SMPC.

*Oblivious transfer* [[12]](#12) allows a sender to transfer one of
many pieces of information to a receiver without knowing which piece was
chosen, preserving privacy during transactions. This primitive imposes
computational and communication overheads but is essential for keeping
certain information private. Recent advances in oblivious transfer
protocols, such as *one-out-of-many oblivious transfer*, have improved
efficiency by reducing the total number of cryptographic operations
required [[6]](#6). Combining SMPC with HE can further
enhance the privacy and security of computations on sensitive data.

## Limitations

   The following limitations underline the need for careful
consideration and evaluation when using distributed learning in
different
applications [[2]](#2)[[3]](#3)[[4]](#4)[[12]](#12):

- **Tailored protocols:** SMPC protocols often require customization for
  specific data analysis tasks, limiting their scalability to generic
  tasks. Developing hybrid protocols or incorporating techniques such as
  homomorphic encryption can partially address this challenge, but their
  feasibility is still limited for many real-world applications.

- **Communication overhead:** Inter-node communication in SMPC incurs
  overhead compared to centralized computation, making complex protocols
  impractical in setups with distributed nodes. Linear bandwidth scaling
  remains a major limitation, especially in large-scale computing, and
  requires innovative paradigms to improve scalability.

- **Security risks:** Dishonest or colluding parties threaten the
  integrity of SMPC protocols, requiring resilience measures against
  potential attacks. The use of secure hardware such as Intel SGX opens
  up new possibilities, but also raises concerns about vendor
  reliability and system vulnerabilities.

- **Information leakage:** Outputs from SMPC protocols may inadvertently
  reveal information about input data, highlighting the importance of
  understanding participant knowledge and potential risk mitigation
  strategies. Combining SMPC with differential privacy has shown promise
  in limiting output leakage, but this approach remains underexplored
  and requires further research for practical adoption.


### References

<a id="1">[1]</a> 
OECD, “Emerging privacy-enhancing technologies: Current regulatory and policy
approaches,” no. 351, p. 51, 2023.

<a id="2">[2]</a> 
Centre for Data Ethics and Innovation, “Privacy Enhancing Technologies Adoption Guide,” https://cdeiuk.github.io/pets-adoption-guide/privacy-enhancing-
technologies-adoption-guide (Last accessed on May, 2024), 2021.

<a id="3">[3]</a> 
The Royal Society, “From privacy to partnership,” The Royal Society, Tech. Rep.
January, 2023.

<a id="4">[4]</a> 
D. Evans, V. Kolesnikov, and M. Rosulek, “A Pragmatic Introduction to Secure
Multi-Party Computation,” Foundations and Trends® in Privacy and Security,
vol. 2, no. 2-3, pp. 70–246, 2018.

<a id="5">[5]</a> 
United Nations, United Nations Guide on Privacy-Enhancing Technologies for
Official Statistics, 2023.

<a id="6">[6]</a> 
K. Jarmul, Practical Data Privacy. O’Reilly Media, Inc., 2023.

<a id="7">[7]</a> 
Information Comissioner’s Office, “Privacy-enhancing technologies (PETs),”
https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/data-
sharing/privacy-enhancing-technologies/ (Last accessed on May, 2024), 2023.

<a id="8">[8]</a> 
Y. Lindell, “Secure multiparty computation,” Commun. ACM, vol. 64, no. 1, p.
86–96, 2020.

<a id="9">[9]</a> 
P. Bogetoft et al., “Secure Multiparty Computation Goes Live,” in Financial
Cryptography and Data Security, 2009.

<a id="10">[10]</a> 
D. Nair and V. Binu and G. Kumar, “An Improved E-voting scheme using Secret
Sharing based Secure Multi-party Computation,” ArXiv, vol. abs/1502.07469,2015.

<a id="11">[11]</a> 
J. Bringer and H. Chabanne and A. Patey, “Privacy-Preserving Biometric Identification Using Secure Multiparty Computation: An Overview and Recent
Trends,” IEEE Signal Processing Magazine, vol. 30, no. 2, pp. 42–52, 2013.

<a id="12">[12]</a> 
European Union Agency for Cybersecurity, M. Adamczyk, P. Drogkaris, “Data
protection engineering: from theory to practice.” ENISA, Tech. Rep. January, 2022.

<a id="13">[13]</a> 
A. Bestavros, A. Lapets, and M. Varia, “User-centric distributed solutions for
privacy-preserving analytics,” Commun. ACM, vol. 60, no. 2, p. 37–39, 2017.

<a id="14">[14]</a>
X. Wang, S. Ranellucci, and J. Katz, “Global-Scale Secure Multiparty Computation,” in Proceedings of the 2017 ACM SIGSAC Conference on Computer and
Communications Security, 2017.

