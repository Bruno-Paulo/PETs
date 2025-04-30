# The PET Laboratory Guide

The PET Laboratory Guide is a hands-on resource designed to help
engineers practically apply Privacy Enhancing Technologies (PETs) to
real-world scenarios. It introduces an example problem that serves as a
central theme throughout the guide, providing a consistent context for
learning and experimentation.

## Structure of the guide

To support this, the guide includes a *cookbook*-style section with
clear, step-by-step instructions, along with the necessary code and
configurations. These resources are designed to facilitate rapid
prototyping and help developers integrate PETs into their systems with
ease.

The guide also includes a practical exercise that extends the main
problem scenario. This challenge encourages readers to explore
variations of the original use case and deepen their understanding of
each PET. Detailed solutions and working examples are provided for each
exercise, providing clear guidance on how to implement PETs in different
applications.

To ensure the correctness of their implementations, developers use
provided input datasets as test cases. These datasets serve as
controlled environments for validation, helping users to verify the
expected behaviour of their PET prototypes.

## List of guides

The following PETs in this guide have been successfully implemented using 
Google Colab-compatible tools and environments. Each tutorial is designed
to be practical, reproducible, and immediately usable, with working code
and hands-on exercises.

| PETs                   | Guide                              |
|------------------------|------------------------------------|
| Synthetic Data         | [SD](Synthetic_Data.ipynb)         | 
| Differential Privacy   | [DP](Differential_Privacy.ipynb)   | 
| Distributed Learning   | [DL](Distributed_Learning.ipynb)   | 
| Homomorphic Encryption | [HE](Homomorphic_Encryption.ipynb) | 

The guides should run without errors. If there is a dependency problem, please try the
and run the requirements.txt file.


## Limitations of the implementation environment

TEEs provide a hardware-based approach to secure computation by
isolating sensitive code and data within protected enclaves.
Implementing a tutorial on TEEs in Google Colab is infeasible due to the
platform's lack of support for the necessary hardware. TEEs such as
Intel SGX, require specific CPU features that are not available in
Colab's virtualised environment. While it is technically possible to
simulate TEEs using tools such as Gramine in a non-secure mode, such
simulations do not reflect the real security characteristics of a TEE.

A TEE tutorial would require users to run code on compatible local
hardware or use specialised virtual machines, which contradicts our goal
of providing universally accessible tutorials.

The practical implementation of ZKPs in Google Colab poses technical
challenges. Most mature ZKP frameworks, such as ZoKrates and Circom are
written in Rust and C++, and are not natively supported in Colab. We
tried to use Python wrappers or install the full toolchains hit
roadblocks due to Colab's lack of support for Rust environments, Docker
containers, and root access. In addition, ZKP computations are
resource-intensive, requiring extensive pre-processing and circuit
compilation that exceeds Colab's time and memory limits. Given these
limitations ZKPs were deemed impractical to implement as a tutorial.

SMPC allows multiple parties to jointly compute a function over their
private inputs without revealing them to each other. CrypTen, a
PyTorch-based SMPC framework, was initially considered for
implementation. However, CrypTen relies heavily on multi-processing and
*inter-process communication (IPC)*, both of which are limited in the
Google Colab architecture. The notebook model in Colab is designed for
single-process execution and does not reliably support forking or
spawning new processes. Colab also restricts socket-based communication
and shared memory access, both of which are essential for CrypTen's
secure computation protocols. Furthermore, CrypTen's reliance on
background processes clashes with Colab's aggressive resource
management, where inactive or secondary processes can be terminated
prematurely. These limitations make Colab unsuitable for realistic SMPC
tutorials, which require local machines or dedicated cloud servers.