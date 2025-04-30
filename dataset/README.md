### Selecting a Dataset

It became clear from our analysis that healthcare is a domain where
multiple PETs play an important role. The relevance of this domain
results from the high sensitivity of healthcare data and the strict
privacy controls required to manage it effectively, which are in line
with the objectives of PETs. To support the development of guides that
teach the implementation of each PET in a real-world context, we need a
running dataset.

The healthcare domain was chosen because of its relevance and critical
role in privacy-preserving research. Indeed, healthcare data is highly
sensitive and requires strict privacy controls, which are well aligned
with the goals of PETs. 

<!-- This is further supported by the mapping shown in
Table [\[table:domainsAndPETS\]](#table:domainsAndPETS){reference-type="ref"
reference="table:domainsAndPETS"}, where healthcare is one of the
domains where all PETs are fully or partially applicable.] -->

The dataset enables a wide range of use cases, such as:

- **Data sharing and analysis:** Simulate scenarios where patient data
  is shared for research while ensuring privacy.

- **Federated learning applications:** Training models across multiple
  healthcare institutions without centralising sensitive data.

- **Privacy-preserving risk prediction:** Use the dataset to simulate
  secure computations for stroke prediction while preserving patient
  privacy.

This dataset will be used accross the guides providing a unified
practical context for hands-on exercises that teach how to implement
PETs effectively.

After evaluating several publicly available datasets in the healthcare
domain, we selected the [**Stroke Prediction Dataset**](https://www.kaggle.com/datasets/fedesoriano/stroke-prediction-dataset/data). This dataset provides data for predicting the
likelihood of stroke based on patient information, making it an
interesting resource for illustrating how PETs are used in healthcare.
In particular, enabling the demonstration of various PETs in realistic
scenarios. This dataset contains the following attributes:

- **Patient demographics:** Gender, age, marital status and place of
  residence, providing key information about the patient.

- **Health indicators:** Hypertension, heart disease, body mass index
  (BMI) and average blood glucose levels, which are important in
  predicting stroke.

- **Lifestyle information:** Smoking status and job type, which help to
  understand the patient's risk factors.

- **Outcome label:** Stroke status (1 for stroke, 0 for no stroke),
  which serves as the primary prediction target.

The structure and features of the dataset provide a robust basis for
designing exercises to be used in the PET guides that meet the
objectives of the guides which are to teach the implementation of PETs
through practical, domain-specific examples.

A summary of the proposed exercises for each PET is given bellow:


  | *PET*    | *Exercise*                                                                                                                                                                            |
  |----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
  | **SD**   | Demonstrate synthetic data generation methods by building on the dataset to create synthetic health records while preserving statistical properties.                                  |
  | **DP**   | Demonstrate privacy-preserving statistical analyses by applying differential privacy techniques to numeric and categorical columns, such as age, BMI, and average glucose level.      |
  | **DL**   | Simulate federated (distributed) learning by training privacy-preserving models on distinct (simulated) healthcare institutions.                                                      | 
  | **HE**   | Demonstrate operations over encrypted attributes such as age or average glucose level for secure computations such as summation or risk classification.                               |
  | **ZKP**  | Illustrate how sensitive attributes, such as smoking status or average glucose level, can be used to construct proofs to validate calculations without revealing the underlying data. |
  | **TEE**  | Simulate secure computations to predict attributes such as stroke status or heart disease demonstrating how TEEs can protect the computation logic.                                   |
  | **SMPC** | Partition the dataset by occupation or address to demonstrate how to perform collaborative computation across institutions while maintaining privacy.                                 | 
