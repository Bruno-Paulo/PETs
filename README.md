# A Practical Guide to Privacy Enhancing Technologies

This repository is a curated and practical resource to help engineers, researchers, and privacy practitioners 
understand and apply **Privacy Enhancing Technologies (PETs)**. This project combines theory, real-world applications, 
and hands-on experimentation to support privacy-conscious system design.

---

## Why PETs?

Privacy Enhancing Technologies enable sensitive data to be used, shared, and analysed without compromising individual 
or organisational privacy. From training machine learning models to data sharing, PETs make it possible to unlock 
value from data while meeting privacy requirements.

Here are some of the core PETs this repository explores:

| PET                                   | Description                                                                                                                     |
|---------------------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| Synthetic Data (SD)                   | Generates artificial datasets that preserve the patterns and statistical properties of the original data.                       |
| Differential Privacy (DP)             | Adds noise to data to ensure privacy while preserving overall data utility.                                                     |
| Distributed Learning (DL)             | Enables machine learning models to be trained on multiple sensitive data sources without disclosure to parties.                 |
| Homomorphic Encryption (HE)           | Allows computations to be performed on encrypted data without decrypting it.                                                    |
| Zero-Knowledge Proofs (ZKP)           | A cryptographic method that allows one party to prove the validity of a statement without revealing any underlying information. |
| Trusted Execution Environments (TEE)  | Ensures the integrity and confidentiality of computations and data in untrusted environments.                                   |
| Secure Multi-Party Computation (SMPC) | Allows multiple parties to collaborate on computations while keeping their input data private.                                  |
---

## What’s in this Repository?

This project is divided into three interconnected guides, each addressing a different aspect of PET adoption:

### 🧠 1. [The Technical Reference Guide](Technical Reference Guide/README.md)

A detailed reference manual for each PET — covering their definitions, algorithms, practical use cases, efficiency trade-offs, and known limitations. It aims to bridge academic concepts with engineering realities and is designed to be modular and extensible.

### 🧭 2. [The Privacy Pattern Guide](Privacy Pattern Guide/README.md)

An interactive decision-support tool that helps you choose appropriate PETs based on real-world technical and business use cases.

🔗 **[Explore the Guide](https://docs.google.com/spreadsheets/u/2/d/e/2PACX-1vSlzlIJoQdCJNCo7mWNitzwNGA4yhsv7WhDPQCxc8ZDokVXJ_Dl1i2r2T9zEWhPrMEjwLKUNyOeeHrJ/pubhtml?gid=1038081398&single=true)**

### 🧪 3. [The PET Laboratory Guide](PET Laboratory Guide/README.MD)

A collection of hands-on tutorials designed for Google Colab. Each tutorial walks through a PET implementation in a consistent real-world scenario, with working code, exercises, and test validations.

#### ✅ Available Tutorials:

| PET                    | Tutorial                                                                                     |
|------------------------|----------------------------------------------------------------------------------------------|
| Synthetic Data         | [Launch SD Notebook](https://colab.research.google.com/drive/1h5NqIZDZKtV9WfIaFHFp4Qd6O_21bCOm?usp=sharing) |
| Differential Privacy   | [Launch DP Notebook](https://colab.research.google.com/drive/16g49145eZUnPEEgIC_phnHClrb6pRCcG?usp=sharing) |
| Distributed Learning   | [Launch DL Notebook](https://colab.research.google.com/drive/1xtVGzNHkPM5cMImY-oDqReMv5FtUCmG9?usp=sharing) |
| Homomorphic Encryption | [Launch HE Notebook](https://colab.research.google.com/drive/1SuQxaVb15CaNQjIUKLtYIrqRarylmtOK?usp=sharing) |

> Tutorials for TEE, ZKP, and SMPC are not included due to technical limitations of the Colab environment.

---

## 📜 License

This project is released under the **Apache License 2.0**. See the [LICENSE](LICENSE) file for full details.

---

## 🤝 Contributing

Contributions are welcome! If you’d like to extend the guides, propose improvements, or add support for more PETs, feel free to open an issue or submit a pull request.
