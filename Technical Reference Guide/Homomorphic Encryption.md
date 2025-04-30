# Homomorphic Encryption

   The fundamental idea of Homomorphic encryption (HE) is to perform
computations over encrypted data in a way that the results will be valid
even on unencrypted data. This means that the organization holding the
data never sees the actual information, just the encrypted result. Only
the party providing the data possesses the decryption key for the
output. This technique enables data processing to be outsourced to
untrusted third parties or untrusted computing environments, such as
cloud infrastructures [[1]](#1)[[2]](#2)[[3]](#3).

There are three types of HE; namely *fully homomorphic encryption*
(FHE), which allows arbitrary operations on encrypted data, *somewhat
homomorphic encryption* (SHE), which allows some combinations of
specific operations on encrypted data, and *partial homomorphic
encryption* (PHE), which allows only a unique type of operation on
encrypted data [[3]](#3). *Bootstrapping* is an innovation in HE, which
allows FHE to perform arbitrarily many computations by reducing the
noise that accumulates during operations [[4]](#4).

## Current and potential applications

   HE enables third-party service providers to analyse medical data,
such as MRI scans, without directly accessing the patient
data [[1]](#1). HE allows secure computation on encrypted data in the
cloud without exposing the data to the cloud service
provider [[5]](#5). In data storage, HE enables analytics to be
performed on encrypted customer data stored in the cloud, facilitating
computational queries while maintaining data security [[1]](#1).
Moreover, in retail analytics, HE is used to train neural networks on
sensitive product data, ensuring security and privacy throughout the
analysis process [[1]](#1).

## Efficiency and parameters

   The efficiency of HE varies based on key and ciphertext sizes,
computational power, and the choice of homomorphic scheme and hardware.
Larger keys typically enhance security but can adversely affect
computational efficiency and memory usage. The nature of the operations
performed and the specific encryption scheme chosen also influence
efficiency. Utilizing GPUs and FPGAs can enhance the performance of HE
schemes, making them more practical for real-world
applications [[5]](#5).

In practice, most efficient implementations of HE use a *levelled mode*.
This mode configures the encryption scheme to support computations of a
specific or bounded size, usually leading to significant performance
improvements [[1]](#1). Some protocols, such as *CKKS*, bypass the
bootstrapping step by tolerating approximate answers, allowing faster
computations for applications such as machine learning and analytics.

## Primitives and algorithms

   Popular algorithms in HE are based on the *learning with error (LWE)*
and *ring learning with error (RLWE)* problems. The LWE problem involves
solving linear equations that have been perturbed by small random
errors, providing a foundation for constructing secure cryptographic
schemes based on the hardness of decoding noisy linear codes. The RLWE
problem is a variant of LWE that leverages the structure of polynomial
rings, allowing for more efficient computations and storage while
maintaining the security properties of LWE [[6]](#6)[[7]](#7).

The *Brakerski-Gentry-Vaikuntanathan (BGV)* algorithm [[8]](#8) is based on
the LWE problem and supports both addition and multiplication operations
on ciphertexts, allowing for secure computation of encrypted data. The
scheme employs a technique called modulus switching to manage noise
growth, enabling a fixed number of operations (levelled approach). BGV
is suitable for applications requiring secure computations on encrypted
data with exact arithmetic. However, noise accumulates with each
operation and needs significant computational resources, making it less
efficient for large-scale applications or deep computational circuits.
Additionally, the complexity of parameter selection to balance security,
performance, and noise growth can be a challenge.

The *Brakerski-Fan-Vercauteren (BFV)* algorithm [[9]](#9) is based on the
RLWE problem and supports efficient arithmetic operations on encrypted
data, including batching techniques that allow multiple plaintext slots
within a single ciphertext. This enhances parallel processing, making
BFV useful for applications requiring efficient arithmetic on large
datasets. BFV optimizes noise management similarly to BGV but offers
better performance. However, it also faces limitations such as noise
growth with each operation, significant computational overhead, and the
complexity of implementing polynomial ring structures.

The Cheon-Kim-Kim-Song (CKKS) algorithm [[10]](#10) is designed for
approximate homomorphic encryption, unlike BGV and BFV, and supports
arithmetic operations on real or complex numbers, making it suitable for
privacy-preserving machine learning and data analysis. CKKS uses
rescaling to manage noise growth while maintaining the precision of
computations. Its main limitations include approximation errors that
accumulate and affect the accuracy of results, noise growth with each
operation that cannot be completely eliminated by rescaling, and the
need for optimal parameter tuning to balance precision, performance, and
security.

## Limitations

   The following limitations underline the need for careful
consideration and evaluation when using HE in different
applications [[1]](#1)[[3]](#3)[[5]](#5)[[11]](#11):

- **Message expansion:** HE can lead to larger encrypted data compared
  to unencrypted data due to message expansion and encoding inefficiency
  from the encryption scheme, impacting performance and memory storage.
  Because of this expansion, HE is not ideal for encrypting large
  datasets. Instead, only essential data should be encrypted.

- **Computational overhead:** FHE allows arbitrary operations, but
  current schemes are often impractical due to significant computational
  overhead and costly bootstrapping operations.

- **Lack of flexibility:** PHE and SHE schemes offer better performance
  but support only a limited number of operations, requiring prior
  knowledge of the required operations for the selection of an
  appropriate encryption scheme.

- **Adaptability:** HE does not give security guarantees if the
  adversary gets hold of decryptions of selected cypher texts.

- **Debbuging:** When outsourcing data processing to a third party, the
  inability of the third party to read the data complicates error
  identification and code development. In practice, this problem can be
  minimised by agreeing on the data schema in advance and possibly
  sharing a plaintext dummy dataset for code development and testing.

- **Complexity:** Understanding and fully using HE can be complex, often
  requiring specialized expertise and knowledge of encryption libraries
  and parameter selection.

- **Integration:** HE can be hard or impossible to integrate with
  existing systems due to possible required changes in existing data
  pipelines, data manipulation procedures and algorithms, and data
  access policies.

### References

<a id="1">[1]</a> 
United Nations, United Nations Guide on Privacy-Enhancing Technologies for
Official Statistics, 2023.

<a id="2">[2]</a> 
OECD, “Emerging privacy-enhancing technologies: Current regulatory and policy
approaches,” no. 351, p. 51, 2023.

<a id="3">[3]</a> 
Centre for Data Ethics and Innovation, “Privacy Enhancing Technologies Adoption Guide,” https://cdeiuk.github.io/pets-adoption-guide/privacy-enhancing-
technologies-adoption-guide (Last accessed on May, 2024), 2021.

<a id="4">[4]</a> 
K. Jarmul, Practical Data Privacy. O’Reilly Media, Inc., 2023.

<a id="5">[5]</a> 
C. Moore and M. O’Neill and E. O’Sullivan and Y. Dor¨oz and B. Sunar, “Practical
homomorphic encryption: A survey,” in 2014 IEEE International Symposium on
Circuits and Systems (ISCAS), 2014.

<a id="6">[6]</a> 
M. Chase, H. Chen, J. Ding, S. Goldwasser, S. Gorbunov, J. Hoffstein, K. Lauter,
S. Lokam, D. Moody, T. Morrison et al., “Security of homomorphic encryption,”
HomomorphicEncryption. org, Redmond WA, Tech. Rep, p. 27, 2017.

<a id="7">[7]</a> 
Z. Brakerski, “Fully homomorphic encryption without modulus switching from
classical GapSVP,” in Annual cryptology conference, 2012.

<a id="8">[8]</a> 
Z. Brakerski, C. Gentry, and V. Vaikuntanathan, “(Leveled) Fully Homomorphic
Encryption without Bootstrapping,” ACM Trans. Comput. Theory, vol. 6, no. 3,
p. 36, 2014.

<a id="9">[9]</a> 
J. Fan and F. Vercauteren, “Somewhat Practical Fully Homomorphic Encryption,” IACR Cryptol. ePrint Arch., vol. 2012, p. 144, 2012.

<a id="10">[10]</a> 
J. Cheon, A. K. M. Kim, and Y. Song, “Homomorphic Encryption for Arithmetic
of Approximate Numbers,” in Advances in Cryptology – ASIACRYPT 2017, 2017.

<a id="11">[11]</a> 
The Royal Society, “From privacy to partnership,” The Royal Society, Tech. Rep.
January, 2023.
