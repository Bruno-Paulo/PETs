### Selecting a Dataset

To create a consistent and realistic foundation for hands-on PET tutorials, we selected a single dataset that supports diverse privacy-preserving scenarios. Healthcare emerged as a strong candidate due to its high data sensitivity, regulatory complexity, and the broad applicability of PETs across clinical, operational, and research use cases.

After reviewing several public datasets, we chose the [**Stroke Prediction Dataset**](https://www.kaggle.com/datasets/fedesoriano/stroke-prediction-dataset/data), which contains demographic, health, lifestyle, and outcome data. It’s well-suited for simulating key PET applications such as:

- **Data sharing & analysis**: Explore anonymisation and data synthesis techniques.
- **Federated learning**: Train models across simulated institutions without sharing raw data.
- **Privacy-preserving predictions**: Securely predict stroke risk using encrypted or distributed data.

The dataset includes:
- **Demographics**: Gender, age, residence, marital status
- **Health indicators**: Hypertension, heart disease, BMI, blood glucose
- **Lifestyle**: Smoking status, occupation
- **Outcome**: Stroke status (target label)

We use this dataset across all PET tutorials, creating a unified, domain-specific context that makes the implementation of privacy techniques more tangible and relevant.

#### 🧪 PET Exercises Overview


  | *PET*    | *Exercise*                                                                                                                                                                            |
  |----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
  | **SD**   | Demonstrate synthetic data generation methods by building on the dataset to create synthetic health records while preserving statistical properties.                                  |
  | **DP**   | Demonstrate privacy-preserving statistical analyses by applying differential privacy techniques to numeric and categorical columns, such as age, BMI, and average glucose level.      |
  | **DL**   | Simulate federated (distributed) learning by training privacy-preserving models on distinct (simulated) healthcare institutions.                                                      | 
  | **HE**   | Demonstrate operations over encrypted attributes such as age or average glucose level for secure computations such as summation or risk classification.                               |
  | **ZKP**  | Illustrate how sensitive attributes, such as smoking status or average glucose level, can be used to construct proofs to validate calculations without revealing the underlying data. |
  | **TEE**  | Simulate secure computations to predict attributes such as stroke status or heart disease demonstrating how TEEs can protect the computation logic.                                   |
  | **SMPC** | Partition the dataset by occupation or address to demonstrate how to perform collaborative computation across institutions while maintaining privacy.                                 | 
