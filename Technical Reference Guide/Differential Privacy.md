# Differential Privacy

Differential privacy (DP) is an information-theoretic concept that aims
at preserving the privacy of individual records within a database when
query results are released. It achieves this by defining strict limits
or bounds on the amount of privacy loss that can occur, ensuring
protection against additional knowledge or post-processing by potential
attackers [[1]](#1)[[2]](#2)[[3]](#3)[[4]](#4). DP introduces calibrated noise into query results,
obscuring individual details while preserving the utility of aggregated
information. This approach provides measurable anonymity for each
individual in the dataset and preserves overall data trends, delivering
statistically useful insights with minimal impact on results [[5]](#5)[[6]](#6).

There are two approaches to DP; namely *global differential privacy
(GDP)* and *local differential privacy (LDP)* [[7]](#7). In GDP,
noise is added during aggregation, requiring a central aggregator to
access real data, while in LDP, noise is added to individual records
before aggregation, ensuring privacy without sharing raw data. In
practice, GDP yields more accurate results with less noise but relies on
trust in the aggregator process, while LDP offers deniability of record
content but requires more users for meaningful results. Moreover, both
models have distinct implications for privacy protection and data
utility, with global DP suitable for accurate results and *deniability
of non-participation*, where it is not possible to verify whether an
individual’s information was included in the dataset, and local DP
mitigating *sensitive attribute inference*, which is the process of
deducting attributes that should not be linked to an individual
[[5]](#5).

## Current and potential applications

By adding noise to datasets, DP reduces the reliability of individual
data, thereby enhancing the privacy of data subjects and protecting
against attacks such as reconstruction, re-identification, or tracing
even when adversaries have access to arbitrary side-knowledge [[2]](#2)[[6]](#6)[[8]](#8). DP enables the analysis of large datasets
that were previously considered too sensitive to share making it harder
to perceive if the individual’s data is true or includes noise
[[6]](#6). Furthermore, DP can reduce the likelihood that erroneously
leaked data will be accurately identified and verified, thereby
enhancing data security and privacy [[6]](#6).

A notable example is the US Census Bureau’s use of DP in the 2020 Census
to address vulnerabilities from reconstruction attacks observed in the
2010 Census [[9]](#9). These attacks successfully re-identified
individuals by combining public census data with external databases,
posing significant privacy risks, particularly for less populated areas.
To counter this, the Bureau took a top-down approach, generating noisy
histograms at different population levels to ensure aggregate
consistency while preserving privacy [[1]](#1). Apple
uses local differential privacy to improve features such as emoji
suggestions on iOS devices. Noise is added on-device and anonymised data
is sent for aggregation, enabling privacy-preserving analytics while
maintaining user deniability [[10]](#10).

## Efficiency and parameters

Technically, DP uses the value of epsilon to determine the level of
noise to be added, which acts as a privacy budget. In practice, epsilon
represents the maximum amount of information that can be inferred about
an individual’s participation in the data [[11]](#11). Smaller
epsilon values indicate stronger privacy guarantees, limiting how much
an attacker can infer about individual records from query results, even
in a worst-case scenario.

Beyond epsilon, the *sensitivity* of a query function quantifies the
maximum change in its output resulting from the addition or removal of a
single individual in the dataset and determines the amount of noise
required to maintain differential privacy [[1]](#1)[[4]](#4)[[11]](#11). There are three types of sensitivity:
*global sensitivity*, which is the maximum difference in the query’s
result on any two neighbouring databases (worst case bound), *local
sensitivity*, which is the maximum difference between the query’s result
on the true database and any of its neighbouring databases, reflecting
actual sensitivity for the given dataset, and *elastic sensitivity*,
which is an efficiently-computed approximation of local sensitivity that
supports joins, offering a balance between global and local sensitivity
for optimal noise addition [[12]](#12).

Bounding sensitivity is essential to ensure that noise addition remains
practical and useful, particularly for queries such as sums or averages,
where unbounded sensitivity can lead to excessive noise or privacy
risks. Clamping and other bounding techniques help to limit the
sensitivity, which directly affects the amount of noise required for a
given epsilon. Larger bounds, while preserving flexibility, introduce
higher noise levels and reduce utility.

The added noise provides plausible deniability, preventing the
identification of specific individuals. Through Bayesian reasoning,
which defines conditional probabilities based on observations and known
or probable ranges of events, an attacker’s ability to update their
prior knowledge of the dataset from query responses is explicitly
constrained, with calibrated noise ensuring that their posterior
knowledge of each individual’s data remains probabilistically bounded.
This balance between noise addition and privacy risk is visualised in
probabilistic terms, with smaller epsilons yielding tighter bounds on
information leakage [[1]](#1).

In addition, composability enables the tracking of cumulative privacy
loss across multiple queries, allowing epsilon to be strategically
allocated based on query importance and sensitivity. Adaptive mechanisms
such as *privacy units* tailored to specific contexts such as
device-level or time-bound intervals, further optimise differential
privacy for longitudinal data or multi-user systems. These mechanisms
take into account dynamic sensitivities and help to preserve privacy
budgets in scenarios with repeated queries or high-dimensional datasets
[[1]](#1).

There are two ways to enforce a privacy budget, either interactively or
non-interactively. Interactive privacy budgets add noise to each query
response and stop querying once the privacy budget is met.
Non-interactive privacy budgets predetermine and apply the level of
identifiable information for the entire dataset, making it suitable for
different types of data handling scenarios [[5]](#5). In other words,
epsilon can be considered as the maximum variance possible between the
output of a query with all the individuals included and the output of a
different query with one of the individuals excluded from the dataset
[[13]](#13).

Setting a privacy budget requires that we first evaluate the sensitivity
of the information, the type of data, the number of queries expected,
and the size of the database. The goal of this analysis is to reduce the
risk of unintended disclosure in queries and to implement contractual
controls to mitigate malicious parties [[14]](#14). Several
factors need to be considered, including the potential for attackers to
gain knowledge from inputs or intermediate results, from multiple
queries, or through collusion among malicious parties to link
information to other datasets resulting in unwanted disclosure. The
privacy budget can be adjusted to reduce privacy risks to an acceptable
level [[5]](#5).

## Primitives and algorithms

DP introduces noise with algorithms such as *Laplace mechanism*,
*Gaussian mechanism*, *exponential mechanism*, *randomised response*,
*composition theorems*, *subsampling and amplification*, and *stochastic
gradient descent* [[15]](#15)[[16]](#16). The *Laplace mechanism*
solves the need for privacy in numerical data queries by adding noise
from a Laplace distribution to the function’s output. This noise is
scaled according to the function’s sensitivity and the privacy parameter
epsilon. However, it is limited to numerical data and high-sensitivity
functions require substantial noise, which can reduce the output’s
utility, especially in high-dimensional data. Furthermore, the Laplace
mechanism is often better suited to low sensitivity queries and may
struggle to maintain utility in cases where individual data points have
high variability. The *Gaussian mechanism* is used when the Laplace
mechanism is limiting, by adding noise from a Gaussian distribution. The
complexity of implementing the Gaussian mechanism and the challenge of
balancing epsilon and the added variable delta are notable limitations.
In addition, the Gaussian mechanism requires careful tuning of the delta
to avoid over-loosening the privacy guarantees, which can introduce
vulnerabilities [[1]](#1).

The *Exponential mechanism* addresses privacy for categorical data by
probabilistically selecting outputs based on a utility function. While
effective, designing an appropriate utility function can be complex, and
the computational cost can be high with large output spaces. The
*Randomised response* protects individual privacy in surveys by having
respondents probabilistically provide truthful or predetermined false
answers, ensuring plausible deniability. This method, while effective
for aggregate statistics, can introduce bias and reduce accuracy. The
*Composition theorems* manage cumulative privacy loss when multiple
differentially private algorithms are applied to the same dataset. Basic
composition adds privacy losses linearly, while advanced composition
offers tighter bounds. Managing the privacy budget across multiple
queries can be complex and computationally intensive. *Subsampling and
amplification* techniques improve privacy guarantees by analyzing random
subsets of data, effectively reducing sensitivity. These methods enhance
privacy-utility trade-offs but can reduce data utility and are complex
to implement.

Finally, the *stochastic gradient descent (SGD)* algorithm optimises the
parameters of a model by iteratively updating them based on the gradient
of the loss function computed from random subsets (batches) of training
data. When combined with differential privacy (*DP-SGD*), noise is added
to the gradients and their sensitivity is limited by clipping, ensuring
that individual contributions remain private while preserving the
learning process.

## Limitations

The following limitations underline the need for careful consideration
and evaluation when using differential privacy in different applications
[[1]](#1)[[2]](#2)[[3]](#3)[[5]](#5)[[6]](#6)[[13]](#13)[[14]](#14):

- **Loss of utility:** The use of differential privacy might not be
  advantageous due to the challenge of balancing noise addition to
  ensure both strong protection and good utility across various
  purposes.

- **Accumulation of epsilon values:** Epsilon values accumulated with
  each subsequent release of a dataset can impact the effectiveness of
  subsequent queries, necessitating deducting these accumulated values
  from the overall privacy budget.

- **Smaller datasets:** Inaccuracies caused by noise are more noticeable
  for smaller datasets.

- **Lack of guidelines:** Selecting an appropriate value for the privacy
  budget can be difficult and depends greatly on the specific context.
  Improper configuration of differential privacy settings can lead to
  the risk of personal information leakage from multiple queries,
  potentially enabling re-identification by attackers.

- **Case-by-case expertise:** The need for case-by-case tuning of
  differential privacy settings and the potential requirement for expert
  knowledge pose challenges for implementation and optimisation.

- **Limited scale deployment:** Despite being well-developed in
  academia, only a few organizations have deployed differential privacy
  at scale.

- **Impact on underrepresented groups:** Noise in differential privacy
  can mask underrepresented groups, risking their underrepresentation in
  datasets and raising ethical concerns in areas such as federal funding
  and redistricting, where accurate representation is critical.


### References

<a id="1">[1]</a> 
K. Jarmul, Practical Data Privacy. O’Reilly Media, Inc., 2023.

<a id="2">[2]</a> 
United Nations, United Nations Guide on Privacy-Enhancing Technologies for
Official Statistics, 2023.

<a id="3">[3]</a> 
The Royal Society, “From privacy to partnership,” The Royal Society, Tech. Rep.
January, 2023.

<a id="4">[4]</a> 
C. Dwork, “Differential privacy,” in Proceedings of the 33rd International Conference on Automata, Languages and Programming - Volume Part II, 2006.

<a id="5">[5]</a> 
Information Comissioner’s Office, “Privacy-enhancing technologies (PETs),”
https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/data-
sharing/privacy-enhancing-technologies/ (Last accessed on May, 2024), 2023.

<a id="6">[6]</a> 
OECD, “Emerging privacy-enhancing technologies: Current regulatory and policy
approaches,” no. 351, p. 51, 2023.

<a id="7">[7]</a> 
European Union Agency for Cybersecurity, M. Adamczyk, P. Drogkaris, “Data
protection engineering: from theory to practice.” ENISA, Tech. Rep. January, 2022.

<a id="8">[8]</a> 
C. Dwork, A. Smith, S. Thomas, and J. Ullman, “Exposed! A Survey of Attacks
on Private Data,” Annual Review of Statistics and Its Application (2017), 2017.

<a id="9">[9]</a> 
S. Garfinkel, J. Abowd, and C. Martindale, “Understanding database reconstruction attacks on public data,” Commun. ACM, vol. 3, no. 3, p. 46–53, 2019.

<a id="10">[10]</a> 
A. Differential Privacy Team, “Learning with privacy at scale,” Apple, Tech. Rep.
December, 2017.

<a id="11">[11]</a> 
J. Lee and C. Clifton, “How Much Is Enough? Choosing ϵ for Differential Pri-
vacy,” in Information Security, 2011.

<a id="12">[12]</a> 
N. Johnson, J. Near, and D. Song, “Towards Practical Differential Privacy for
SQL Queries,” Proc. VLDB Endow., vol. 11, no. 5, pp. 526–539, 2017.

<a id="13">[13]</a> 
Centre for Data Ethics and Innovation, “Privacy Enhancing Technologies Adoption Guide,” https://cdeiuk.github.io/pets-adoption-guide/privacy-enhancing-
technologies-adoption-guide (Last accessed on May, 2024), 2021.

<a id="14">[14]</a> 
C. Dwork, N. Kohli, and D. Mulligan, “Differential Privacy in Practice: Expose
your Epsilons!” Journal of Privacy and Confidentiality, vol. 11, no. 2, 2019.

<a id="15">[15]</a> 
C. Dwork and A. Roth, “The Algorithmic Foundations of Differential Privacy,”
Foundations and Trends in Theoretical Computer Science, vol. 9, no. 3-4, pp.
211–407, 2014.

<a id="16">[16]</a> 
M. Abadi, A. Chu, I. Goodfellow, H. McMahan, I. Mironov, K. Talwar, and L.
Zhang, “Deep Learning with Differential Privacy,” in Proceedings of the 2016
ACM SIGSAC Conference on Computer and Communications Security, 2016.