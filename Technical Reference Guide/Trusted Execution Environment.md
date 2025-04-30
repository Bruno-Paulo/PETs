# Trusted Execution Environments

   A Trusted Execution Environment (TEE) is a state-of-the-art hardware
technology that allows sensitive applications to execute in secure
memory regions isolated from the rest of the system, protecting against
unauthorized access and tampering. TEEs enable untrusted third-party
processing of data stored within them. Processing occurs directly on
unencrypted data within the TEE, and after computation, the result is
encrypted before being communicated back to the data controller for
decryption [[1]](#1)[[2]](#2).

## Current and potential applications

   TEE facilitates the deployment of confidential models on untrusted
customer infrastructure, reducing the risk of data leakage. In this
setup, only the processing step that uses the model needs to be hosted
within a TEE, rather than the entire application code and data. A
prominent example is AI vendors that sell access to pre-trained deep
learning models and algorithms. To protect intellectual property, these
models are not provided directly to the customer, but are deployed by
the provider on its servers and are only accessible via an API. TEE can
be used for accessing control and document distribution on enterprise
rights management, establishing secure video conferencing and generation
of one-time passwords to authorize online financial
transactions [[3]](#3).

TEE enhances the security of cloud computing by providing security
properties similar to on-premises environments, making it viable for
sensitive applications. TEE secures the processing of sensitive data
collected by IoT devices and provides trust through attestation. This
includes scenarios where users need to be isolated from the cloud
provider itself, such as intelligence operations where cloud operators
or local authorities may engage in passive data snooping. In addition,
TEE provides a technical solution for multi-party computing by ensuring
secure collaboration on private data sets without relying on
non-technical methods such as trusted third parties. Finally, TEE
facilitates secure data sharing for AI and data mining, especially in
sensitive areas such as medical data [[4]](#4).

## Efficiency and parameters

   Computational overhead, memory limitations, and hardware capabilities
influence the efficiency of TEEs. TEEs like Intel SGX and ARM TrustZone
introduce performance overhead due to the need for context switching
between the secure and normal execution environments. This switching can
slow down applications, particularly those that require frequent
transitions between these states. Additionally, TEEs often have limited
memory resources, which constrains the amount of data that can be
processed in secure memory. This limitation impacts the efficiency of
data-intensive applications running within TEEs. Computational power and
the use of modern hardware, such as GPUs and FPGAs, can significantly
improve the efficiency of TEEs by accelerating cryptographic operations
and other intensive tasks [[5]](#5).

## Primitives and algorithms

   TEE uses cryptographic primitives and security algorithms to ensure
confidentiality, integrity and authenticity of data. Key primitives
include *secure boot*, which verifies the integrity of the system at
startup, and *remote attestation*, which allows remote verification of
the integrity of the TEE and the trustworthiness of its code. The TEE
also uses *isolated execution* to ensure that code and data within the
TEE cannot be accessed or tampered with by the normal execution
environment or other software. Cryptographic hash functions and digital
signatures are used for integrity verification, generating fixed-size
outputs from input data to confirm its unaltered state and provide a
mechanism for authentication. Symmetric and asymmetric encryption
protect the confidentiality of data within the TEE and when
communicating with external entities, with AES and RSA/ECC being
commonly used algorithms. Secure key management practices are essential
to protect cryptographic keys within the TEE, ensuring that they are
only accessible to authorised code. In addition, key exchange protocols
such as Diffie-Hellman or Elliptic Curve Diffie-Hellman (ECDH)
facilitate secure key exchange, while random number generators provide
the unpredictability required for cryptographic
operations [[5]](#5)[[6]](#6)[[7]](#7).

TEEs use secure storage algorithms to encrypt data at rest, access
control mechanisms to restrict access to resources, and
integrity-checking algorithms to detect unauthorised changes.
Homomorphic encryption is sometimes used to perform computations on
encrypted data without the need for decryption, further enhancing
security [[8]](#8). Secure channels and protocols provide secure
communication between the TEE and external entities. Specific to Intel
SGX, additional primitives such as the *Enclave Page Cache (EPC)* for
memory isolation and the *SGX instruction set* for secure execution
further enhance security. Together, these mechanisms ensure that the TEE
provides a robust security environment for sensitive
computations [[6]](#6)[[7]](#7).

## Limitations

   The following limitations underline the need for careful
consideration and evaluation when using TEE in different
applications [[2]](#2)[[5]](#5)[[9]](#9)[[10]](#10):

- **Reliance on trust:** Using TEE requires trust that environments are
  correctly set up. Otherwise, the environment and the computation in it
  will be vulnerable to security risks such as side-channel attacks like
  power analysis or timing information. Successful attacks such as cache
  attacks, branch prediction attacks, speculative execution attacks, and
  fault injection attacks have been documented, demonstrating that TEEs
  do not completely eliminate vulnerabilities.

- **Lack of standardisation:** There is no industry standardised
  approach for interacting with TEEs, leading to vendor-specific APIs
  and potential vendor lock-in for applications leveraging TEEs.

- **Performance overhead:** Hardware-based TEE can introduce a
  performance penalty for computations happening within the secure
  enclave. This penalty can be significant, especially for applications
  exceeding the limited on-chip memory (e.g., 16x slowdown for large
  memory usage in Intel SGX).

- **Memory limitations:** Hardware-based TEEs can have limited memory
  capacity within the enclave, restricting the size and complexity of
  applications that could run efficiently.


### References
<a id="1">[1]</a> 
OECD, “Emerging privacy-enhancing technologies: Current regulatory and policy
approaches,” no. 351, p. 51, 2023.

<a id="2">[2]</a> 
Centre for Data Ethics and Innovation, “Privacy Enhancing Technologies Adoption Guide,” https://cdeiuk.github.io/pets-adoption-guide/privacy-enhancing-
technologies-adoption-guide (Last accessed on May, 2024), 2021.

<a id="3">[3]</a> 
M. Hoekstra and R. Lal and P. Pappachan and V. Phegade and J. Del Cuvillo,
“Using innovative instructions to create trustworthy software solutions.” HASP@
ISCA, vol. 11, no. 10.1145, pp. 2 487 726–2 488 370, 2013.

<a id="4">[4]</a> 
T. Geppert and S. Deml and D. Sturzenegger and N. Ebert, “Trusted Execution Environments: Applications and Organizational Challenges,” Frontiers in
Computer Science, vol. 4, 2022.

<a id="5">[5]</a> 
United Nations, United Nations Guide on Privacy-Enhancing Technologies for
Official Statistics, 2023.

<a id="6">[6]</a> 
S. Chakrabarti, T. Knauth, D. Kuvaiskii, M. Steiner, and M. Vij, “Chapter 8 -
Trusted execution environment with Intel SGX,” in Responsible Genomic Data
Sharing. Academic Press, 2020.

<a id="7">[7]</a> 
V. Costan and S. Devadas, “Intel SGX explained,” Cryptology ePrint Archive,2016.

<a id="8">[8]</a> 
D. Natarajan, A. Loveless, W. Dai, and R. Dreslinski, “Chex-Mix: Combining
Homomorphic Encryption with Trusted Execution Environments for Oblivious
Inference in the Cloud,” in 2023 IEEE 8th European Symposium on Security and
Privacy (EuroSP), 2023.

<a id="9">[9]</a> 
K. Jarmul, Practical Data Privacy. O’Reilly Media, Inc., 2023.

<a id="10">[10]</a> 
A. Nilsson, P. N. Bideh, and J. Brorsson, “A Survey of Published Attacks on Intel
SGX,” ArXiv, vol. abs/2006.13598, 2020.





