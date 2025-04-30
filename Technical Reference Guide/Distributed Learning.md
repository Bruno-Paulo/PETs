# Distributed Learning

Distributed learning (DL) involves executing a computer program
against decentralised data without directly revealing the data to the
party initiating the analysis [[1]](#1). DL ensures data privacy as only
model weights are communicated. However, there is a risk of user
information inference from these weights, often mitigated by combining
with other techniques like differential privacy, secure multi-party
computation, and homomorphic encryption for enhanced
privacy [[2]](#2)[[3]](#3)[[4]](#4)[[5]](#5).

Federated learning, a specific approach within DL, uses a distributed
data architecture where models and training updates are sent to edge
nodes or devices rather than querying centralised endpoints. Each device
contributes to the training of a shared model using its local data,
ensuring that sensitive data remains decentralised and private.

## Current and potential applications

Distributed learning provides a privacy-preserving approach to model
training that is particularly suitable for data distributed across
different edge devices such as mobile phones. DL is used for mobile
keyboard prediction in Google devices and speech recognition
applications such as Siri [[3]](#3). It enables broader population reach
and model de-biasing by leveraging diverse, non-IID data from edge
devices, which is essential for building more comprehensive models.

It is effective in environments where sensitive data cannot be moved or
centralised for security, privacy or regulatory reasons, using federated
analytics to process data where it resides [[2]](#2). In
scenarios involving IoT devices or on-premises systems with
confidentiality rules, distributed learning ensures that data remains
local while still supporting analytical objectives. For example,
predictive maintenance and alert systems can benefit from local
statistical analysis and training at the edge, enabling faster detection
of cause-and-effect relationships while minimising data transfer.

Distributed learning also enables offline functionality, allowing models
on devices to operate independently during connectivity issues. In
addition, its application extends to techniques such as multitask
learning, split learning, and model personalisation on heterogeneous
data, although these are primarily areas of ongoing research. It also
facilitates cross-silo learning, enabling collaboration between
different parts of an organisation or between organisations without the
need to share raw data. This is relevant in areas such as logistics and
telecommunications. Personalised models can depart locally from a
central model, improving the user experience while preserving privacy by
keeping both data and models on the user's device.

In Trusted Smart Surveys, smartphone sensor data can complement
traditional surveys conducted by the National Statistical Office,
supporting the regular production of statistics and facilitating
collaboration with public and private data sources [[3]](#3).

## Efficiency and parameters

   The efficiency parameters of distributed learning include
communication and computation costs on both client and server sides.
Federated learning requires frequent transfers of model updates between
clients and the central authority, resulting in communication and
computation costs for clients. In contrast, split learning offers lower
client-side computational costs, but introduces latency due to its
sequential nature and queuing delays [[3]](#3). Other efficiency
parameters include the size and type of data, complexity of the neural
network architecture used, and decentralised network characteristics
such as the number of clients and their relationships [[6]](#6).
Research in this area explores methods focused on network resource
management and device selection to reduce the communication
overhead [[7]](#7).

Efficient deployment of federated systems requires consideration of
connectivity reliability, device hardware limitations such as memory and
power, and load variations due to concurrent processes. Reliable
connectivity ensures fewer training interruptions and enables
aggregation of updates from a larger subset of devices, improving model
accuracy and robustness. Devices with greater power and memory
availability can handle larger model updates and participate in more
computationally intensive training rounds, reducing latency and
improving convergence speed. Device load variations affect their ability
to contribute effectively, while workload management ensures that
resource-intensive tasks do not impact device usability or battery
life [[2]](#2).

The choice of device also affects the performance of the optimisation
system. For example, devices with higher battery levels are better
suited for extended participation, while those with the latest software
versions can take advantage of advanced features for improved
performance. The availability of high quality, representative data on
edge devices enhances the training process, ensuring more accurate and
diverse model learning outcomes [[2]](#2).

These mechanisms allow fault detection and performance monitoring
without compromising user privacy, ensuring both system efficiency and
compliance with privacy guarantees. Such practices improve the
scalability and reliability of distributed learning systems, especially
when operating across diverse edge devices.

## Primitives and algorithms

   DL can be divided into *federated learning* [[3]](#3), *split
learning* [[8]](#8), and *meta learning* [[5]](#5). In *federated
learning*, each data holder computes and updates weights on their data
and sends it to a central authority, which computes and distributes it
back to each party. Each party can obtain a trained neural network
without sharing their data directly. In *split learning*, the network is
divided between parties and the server. Forward propagation is done by
parties and sent to the server, which then updates and distributes the
weights back to the parties for further training.  In *meta learning*,
multiple cohorts of clients jointly train models using secure
aggregation protocols, ensuring the privacy of individual model updates
while improving robustness against backdoor attacks. This framework
aggregates cohort updates instead of individual ones, enabling
cohort-level anomaly detection, reducing update variability and
mitigating malicious interference.

Federated learning poses two types of privacy-related risks: *local or
gradient-level risk*, where sharing model updates can indirectly reveal
sensitive information about the underlying data, and *global or
model-level risk*, where the learned model itself is vulnerable to
attacks such as membership inference and model reconstruction.
Disclosure control techniques like differential privacy can mitigate
these risks, but challenges remain in implementing them effectively,
especially in deep learning models with high-dimensional data.
Additionally, federated learning approaches are susceptible to
non-privacy-related risks such as *model poisoning* and *model inversion
attacks* at both local and global levels [[3]](#3).

## Limitations

The following limitations underline the need for careful
consideration and evaluation when using distributed learning in
different
applications [[1]](#1)[[2]](#2)[[3]](#3)[[6]](#6)[[9]](#9)[[10]](#10):

- **Privacy risks:** Even without directly accessing the data,
  information about individuals can be inferred by analysing the
  results. For instance, distributed learning apps can leak information
  in the parameters sent back to the controller.

- **Development:** Limited access to data makes development, testing,
  and troubleshooting code more difficult. Sharing schema details, data
  standards, and dummy data can help mitigate this.

- **Heterogeneity:** Devices participating in the distributed learning
  process may have different specifications. Additionally, the data
  stored on these devices may be of different formats or qualities. This
  heterogeneity can make it difficult to train a model efficiently and
  limits the types of models you can build.

- **Connectivity reliance:** Distributed learning relies on stable
  connectivity, posing challenges for applications needing uninterrupted
  access to analytic outcomes.

- **Communication:** The constant communication between devices to share
  and update model parameters can consume significant network bandwidth,
  especially for resource-constrained devices.

### References

<a id="1">[1]</a> 
Centre for Data Ethics and Innovation, “Privacy Enhancing Technologies Adoption Guide,” https://cdeiuk.github.io/pets-adoption-guide/privacy-enhancing-
technologies-adoption-guide (Last accessed on May, 2024), 2021.

<a id="2">[2]</a> 
K. Jarmul, Practical Data Privacy. O’Reilly Media, Inc., 2023.

<a id="3">[3]</a> 
United Nations, United Nations Guide on Privacy-Enhancing Technologies for
Official Statistics, 2023.

<a id="4">[4]</a> 
C. Dwork and A. Roth, “The Algorithmic Foundations of Differential Privacy,”
Foundations and Trends in Theoretical Computer Science, vol. 9, no. 3-4, pp.
211–407, 2014.

<a id="5">[5]</a> 
O. Aramoon, P. Chen, G. Qu, and Y. Tian, “Meta federated learning,” CoRR,
vol. abs/2102.05561, 2021.

<a id="6">[6]</a> 
T. Li and A. Sahu and A. Talwalkar and V. Smith, “Federated Learning: Challenges, Methods, and Future Directions,” IEEE Signal Processing Magazine,
vol. 37, no. 3, pp. 50–60, 2020.

<a id="7">[7]</a> 
M. Chen and N. Shlezinger and H. Poor and Y. Eldar and S. Cui,
“Communication-efficient federated learning,” Proceedings of the National
Academy of Sciences, vol. 118, no. 17, p. e2024789118, 2021.

<a id="8">[8]</a> 
P. Vepakomma, O. Gupta, T. Swedish, and R. Raskar, “Split learning for
health: Distributed deep learning without sharing raw patient data,” ArXiv, vol.
abs/1812.00564, 2018.

<a id="9">[9]</a> 
OECD, “Emerging privacy-enhancing technologies: Current regulatory and policy
approaches,” no. 351, p. 51, 2023.

<a id="10">[10]</a> 
Information Comissioner’s Office, “Privacy-enhancing technologies (PETs),”
https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/data-
sharing/privacy-enhancing-technologies/ (Last accessed on May, 2024), 2023.
