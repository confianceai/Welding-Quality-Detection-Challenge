# ML-Trustworthy Evaluation Protocol

## Multi-Criteria Aggregation Methodology

The ML-Trustworthy evaluation of the submitted AI component follows a **multi-criteria aggregation methodology** designed to ensure a fair and reliable assessment of various **trust attributes**.  
The table below illustrates the principle of metrics aggregation:

![image](./images/Metric_tabular.png)

## Example of a comparative results table for four fictional submissions.

The following table illustrates a performance overview of four different virtual solutions which were actually evaluated (using manually constructed inference files) using the trustworthy AI pipeline. The indicator color codes are for illustrative purposes only.

Among these four submissions:
 - **Solu-Perfect**: The ideal solution, achieving perfect scores in both performance and all trust-related attributes.
- **Solu-No-Trust**: A realistic solution without any dedicated mechanisms to address trustworthy AI concerns.
- **Solu-With-Trust**: The same base solution as Solu-No-Trust, but enhanced with mechanisms for handling uncertainty, robustness, OOD monitoring, and drift management.
- **Solu-Random**: A baseline solution that returns random predictions.

We observe that the **Solu-Perfect** solution achieves a perfect score across all metrics. Both **Solu-No-Trust** and **Solu-With-Trust** show identical scores in terms of Performance and Generalization. However, Solu-With-Trust significantly improves its trustworthiness scores across other attributes such as Uncertainty, Robustness, Monitoring, and Drift Management.

![image](./images/Tabular_metrique.png)

## ML-Trustworthy Evaluation design

The evaluation protocol was designed to assess both **performance** and **trustworthiness requirements**, based on the **Operational Design Domain (ODD)** derived from operational needs linked to the AI component's automated function (i.e., assistance in weld validation).

After identifying the relevant **trust attributes** (e.g., *robustness*) associated with specific **trust properties** (e.g., *output invariance under blur perturbation*), the evaluation methodology was structured into the following stages:

- **Evaluation Specification**  
  What specific model behaviors do we want to assess and validate?

- **Evaluation Set Specification**  
  What kind of data must be used or constructed to test whether the model exhibits the expected behavior under specific conditions?

- **Evaluation Set Design**  
  What data should be selected or generated to build these evaluation sets?

- **Evaluation Set Validation**  
  How can we ensure that the evaluation datasets are reliable and representative of the scenarios being analyzed?

- **Criteria Specification**  
  What criteria should be defined to measure the presence or absence of the expected behavior?

- **Metrics Design**  
  What metrics can be used to quantify these criteria?

- **Trust-KPI Design**  
  How can these criteria be aggregated into a **Trust-KPI** for each trust attribute?

## Steps of the Metrics and Trust-KPI Computation

The aggregation process consists in several key steps:

### 1. Computation of Metrics Related to Trust Attributes

- Several metrics are computed for each attribute using specific evaluation datasets, in order to capture different aspects of the attribute’s performance.
- These evaluation datasets are either selected or synthetically generated to test distinct behavioral criteria.

### 2. Normalization of Attribute Metrics

- All attribute-specific metrics are normalized to a score within the range \[0, 1\], where **1** represents the best possible performance.
- Normalization is performed using appropriate transformations (e.g., sigmoid functions, exponential decay), depending on the nature of each metric.

Example normalization functions:
$$OP_{score} = e^{-k \cdot M_{OP-P}}$$

### 3. Trust-KPI Aggregation

- For each attribute, a specific aggregation function combines the normalized metrics into a single **trust-KPI**.
- This allows for a comprehensive representation of the model’s performance with respect to each trust attribute.

$$KPI_{X} = agg({metric}_{X^1},..,{Xmetric}_{X^k})$$

### 4.Piecewise Linear Rescaling of Trust-KPIs

  - To ensure consistency and comparability across attributes, each KPI undergoes a **piecewise linear rescaling**.
  - This rescaling takes into account both predefined performance and confidence requirements.
  - This rescaling accounts for predefined performance and confidence thresholds, aligning the raw scores with evaluation constraints.

$$f'(x) =
\begin{cases}
\frac{\beta_1}{\alpha_1} f(x), & 0 \leq f(x) < \alpha_1 \\
\frac{\beta_2 - \beta_1}{\alpha_2 - \alpha_1} (f(x) - \alpha_1) + \beta_1, & \alpha_1 \leq f(x) \leq \alpha_2 \\[8pt]
\frac{1 - \beta_2}{1 - \alpha_2} (f(x) - \alpha_2) + \beta_2, & \alpha_2 < f(x) \leq 1
\end{cases}$$

### 5. Weighted Aggregation of Trust-KPIs
  - The rescaled attribute KPIs are then aggregated into a **final evaluation score** using a **weighted mean**.
  - Each weight reflects the relative importance of its corresponding attribute within the overall trustworthy AI assessment.
$$\alpha_1*I^{perf} + \alpha_2*I^{U} + \alpha_3*I^{Rob} + \alpha_4*I^{ood} + \alpha_5*I^{gen}+\alpha_6*I^{drift}$$

### 6. Purpose of the Aggregation Protocol

The goal of this aggregation process is to produce a single, comprehensive trust score that captures the system’s performance across six key trust attributes. Each of these attributes is assessed through multiple criteria, measured with relevant metrics and normalized to reflect their practical impact.

## Trust-KPI and metrics by attribute.

### Performance attribute

**Purpose**: Measures the model's predictive accuracy and efficiency, ensuring it meets baseline expectations in a controlled environment.

**Evaluation sets**: Standard ML evaluation set based on a representative 20% split of the dataset.

**Metrics**:
  - **OP-Perf** (Operational Performance): Evaluates model performance through an operational view using confusion-matrix-based metrics that account for the cost of different error types and weld criticality.

       $$ex : c^{op} = \sum_{k}^{|N|} \sum_{i}^{true_{class}} \sum_{j}^{pred_{class}} \mathbb{1}_{Top_{class}(\hat{y}_k)=j} * cost(i,j,k,k_{seam}) $$
  - **ML-Perf** (Machine Learning Performance): Assesses performance using standard ML metrics such as precision.
    $$ex : s^{ml} = \frac{\sum_{i=1}^{N} \mathbb{1} (y_i = 1 \land \hat{y}_i = 1)}{\sum_{i=1}^{N} \mathbb{1} (\hat{y}_i = 1)}$$
  - **Inference Time (Times)**: Measures computational efficiency and runtime.

**Performance-KPI**: Combines OP-Perf and ML-Perf using a weighted average, penalized by inference time to reflect operational constraints.
$$ I^{Perf}=\frac{(\alpha_{op} e^{-k_c c^{op}} + \alpha_{ml} s^{ml})}{1 + k_t ln(1+t)} $$

### Uncertainty assessement
**Purpose** : Evaluates the AI component’s ability to express meaningful and calibrated uncertainty, helping assess the risk of decision errors.

**Evaluation sets**: Standard ML evaluation set based on a representative 20% split of the dataset.

**Metrics**:
  - **U-OP** (Uncertainty Operational Gain): Relative measures of the virtual gain (in operational term) to consider probabilistic outputs compared to hard outputs predictions in relation to the gap between the perfect solution and the current hard outputs predictions.
  $$ex : c^{U} = \sum_{k}^{|N|} \sum_{i}^{true_{class}} \sum_{j}^{pred_{class}} \hat{y}_k(j) * cost(i,j,k,k_{seam}) $$

  $$ U^{op} = \frac{(c^{U} - c^{op})}{(c^{op} - c^{op}_{perfect})}$$

  - **U-Calib** (Calibration Quality): Evaluates how well predicted probabilities align with actual error rates (e.g., Expected Calibration Error).
    $$ex : \beta^U = \sum_{m=1}^{M} \frac{|B_m|}{N} acc(B_m) - conf(B_m)\ \text{ECE}$$

**Uncertainty-KPI** : Combines Uncertainty Operational Gain with calibration error.
$$I^{U} = e^{k_u*U^{op}} * (1 - \beta^U)^{k_{\beta}} $$

### Robustness
**Purpose**: Assesses model stability under perturbations such as blur, lighting variation, rotation, and translation.

**Evaluation sets**: Generated by applying synthetic perturbations to a weld-balanced subset of the standard evaluation set.

![image](./images/Blur_illu.png)

**Metrics**:
   - **Blur Robustness** : Aggregation (AUC) of the ML-performance (Precision score) across increasing perturbation levels.
   - **Luminance Robustness** : Aggregation (AUC) of the ML-performance (Precision score) across increasing perturbation levels.
   - **Rotation Robustness** : Aggregation (AUC) of the ML-performance (Precision score) across increasing perturbation levels.
   - **Translation Robustness**: Aggregation (AUC) of the ML-performance (Precision score) across increasing perturbation levels.
$$ex : r^x = Auc(s^ML_{/delta_1}/,..., s^ML_{/delta_k}) $$ 

**Robustness-KPI** : Weighted aggregation of robustness scores across all perturbation types.

$$ I^{Rob} = \sum_{i \in {blur,lum,rot,trans}} \alpha_{r_i} * r^i $$ 

### OOD-Monitoring 

**Purpose**: Evaluates the model's ability to detect and handle out-of-distribution (OOD) inputs.

**Evaluation sets**: Includes both synthetic and real OOD datasets with a balanced mix of normal and OOD samples. Real OOD samples are manually selected, and synthetic OOD samples are generated through transformations.

![image](./images/Ood_illu.png)

**Metrics**
  - **Real-OOD score** : AUROC on the real OOD evaluation set.
  - **Syn-OOD score** :AUROC on the synthetic OOD evaluation set.
  
	$$ex : s^{ood}_x = \frac{1}{N_{\text{ID}} N_{\text{OOD}}} \sum_{i=1}^{N_{\text{OOD}}} \sum_{j=1}^{N_{\text{ID}}} \mathbb{1}(\hat{s}^{ood}_i > \hat{s}^{ood}_j)\ (\text{AUROC})$$ 

**OOD-Monitoring KPI**: Weighted average of real and synthetic OOD detection performance.
$$I^{ood} = \alpha_{syn}*s^{ood}_{syn} + \alpha_{real}*s^{ood}_{real}$$

### Generalization 
**Purpose**: Measures the model’s ability to generalize to unseen weld types that share characteristics with the training set.

**Evaluation sets**: Built using data from weld types excluded during training but with similar visual/structural traits.

![image](./images/Gen_illu.png)

**Metrics**:
  - **OP-Perf-g** Operational performance on the generalization set.
  - **ML-Perf-g** ML performance (e.g., precision) on the generalization set.

**Generalization-KPI**: Aggregated from OP-Perf-g and ML-Perf-g.
$$I^{gen} = \alpha_{op}*e^{-k_c c^{op}_g} + \alpha_{ml}*s^{ml}_{g}$$

### Data-Drift handling
**Purpose**: Evaluates both the robustness and OOD detection of the model in response to gradual data drift.

**Evaluation sets**: Constructed by applying increasing levels of synthetic perturbations to a normal data sequence, simulating drift. Final segments are manually labeled as OOD.

![image](./images/Drift_illu.png)

**Metrics**:
  - Perf-OP-d : Operational performance under drift.
  - OOD-d: "OOD-Detection score" : AUROC on the drift-induced OOD subset.  

**Data-Drift-KPI**: Combines performance and detection ability during simulated drift.
$$I^{Drift} = e^{-k_{op} * c^{op}_{drift}} + s^{ood}_{drift}$$
