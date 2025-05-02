# 🗂️ Dataset selection for PET tutorials

To ensure consistency across our tutorials, we have selected a real-world healthcare dataset that supports a wide range of PET techniques. The aim is to ground each tutorial in a common, realistic context.

---

## 🏥 Why Healthcare?

Healthcare offers:

- **📊 High data sensitivity** - requiring strong privacy protections.
- **⚖️ Complex regulations** - making PETs a practical necessity.
- **🔁 Repetitive workflows** - ideal for reproducible privacy patterns.

After reviewing several datasets, we selected the following:

👉 [**Stroke Prediction Dataset**](https://www.kaggle.com/datasets/fedesoriano/stroke-prediction-dataset/data)

It includes demographic, lifestyle and clinical variables - allowing for multiple PET exercises.

---

##  📑 Dataset features

- **Demographics** - age, sex, housing type, marital status
- **Health metrics** - BMI, hypertension, heart disease, glucose levels
- **Lifestyle** - smoking status, work type
- **Outcome** - stroke incidence (target variable)

---

##  🧪 PET Exercise Mapping


  | *PET*    | *Exercise*                                                                                                                                                                            |
  |----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
  | **SD**   | Demonstrate synthetic data generation methods by building on the dataset to create synthetic health records while preserving statistical properties.                                  |
  | **DP**   | Demonstrate privacy-preserving statistical analyses by applying differential privacy techniques to numeric and categorical columns, such as age, BMI, and average glucose level.      |
  | **DL**   | Simulate federated (distributed) learning by training privacy-preserving models on distinct (simulated) healthcare institutions.                                                      | 
  | **HE**   | Demonstrate operations over encrypted attributes such as age or average glucose level for secure computations such as summation or risk classification.                               |
  | **ZKP**  | Illustrate how sensitive attributes, such as smoking status or average glucose level, can be used to construct proofs to validate calculations without revealing the underlying data. |
  | **TEE**  | Simulate secure computations to predict attributes such as stroke status or heart disease demonstrating how TEEs can protect the computation logic.                                   |
  | **SMPC** | Partition the dataset by occupation or address to demonstrate how to perform collaborative computation across institutions while maintaining privacy.                                 | 

---

> This shared dataset serves as a **common thread** through all tutorials - making the exercises relatable, practical and domain-specific.
