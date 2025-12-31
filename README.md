# Evaluating the Impact of Adversarial Debiasing on Fairness, Performance, and Interpretability in the Adult Dataset

**Author:** David Rocha de Santana  

---

## Abstract

Algorithmic decision-making systems trained on real-world data are prone to inheriting and amplifying societal biases, particularly when applied to sensitive domains such as income prediction. In this study, we evaluate the impact of **Adversarial Debiasing** as a fairness-aware in-processing technique using the Adult dataset. Our analysis focuses on the trade-offs between predictive performance, group fairness metrics, and model interpretability. We compare a baseline classifier against an adversarially debiased model and complement the evaluation with **SHAP-based feature attribution**. The results demonstrate that adversarial debiasing substantially improves demographic parity and disparate impact but introduces a noticeable degradation in predictive performance and equal opportunity. Furthermore, SHAP analysis reveals how fairness constraints alter feature importance, reducing direct reliance on sensitive attributes while preserving indirect bias through correlated variables. These findings highlight the importance of combining fairness metrics with explainability techniques for a comprehensive assessment of fairness-aware machine learning models.

---

## 1. Introduction

Machine learning models are increasingly used in decision-making systems across high-impact domains such as finance, healthcare, and public policy. Despite their effectiveness, these models often learn and reproduce historical biases present in the data, leading to unfair outcomes for protected social groups.

To address this issue, the field of **fair machine learning** has proposed multiple bias mitigation strategies, which can be applied before, during, or after model training. Among these approaches, **Adversarial Debiasing** stands out as an in-processing method that integrates fairness objectives directly into the learning process.

At the same time, the rise of **explainable artificial intelligence (XAI)** has emphasized the need to understand how fairness-aware constraints influence model behavior. However, the interaction between adversarial debiasing and interpretability remains underexplored. This work aims to bridge this gap by jointly analyzing fairness metrics, predictive performance, and SHAP-based explanations.

---

## 2. Related Work

Fairness in machine learning has been extensively studied through three main categories of approaches: pre-processing, in-processing, and post-processing methods. Adversarial Debiasing, introduced by Zhang et al., employs an adversarial objective to minimize the ability of a secondary network to infer protected attributes from the model’s predictions.

Previous studies report that adversarial approaches are effective in improving global fairness metrics such as demographic parity and disparate impact. However, they often introduce trade-offs in predictive performance and may worsen other fairness criteria, such as equal opportunity.

Interpretability techniques such as **SHAP (SHapley Additive exPlanations)** have become standard tools for understanding feature contributions in machine learning models. Recent work suggests that explainability can support fairness audits by identifying direct and proxy sources of bias, yet comprehensive analyses combining SHAP and adversarial debiasing remain limited.

---

## 3. Dataset and Experimental Setup

### 3.1 Adult Dataset

The Adult dataset contains demographic and employment-related attributes used to predict whether an individual’s annual income exceeds \$50,000. Following common practice in fairness research, **sex** was selected as the protected attribute, with males treated as the privileged group.

All categorical attributes were encoded numerically to satisfy the requirements of the AIF360 framework. Instances with missing values were removed during preprocessing.

### 3.2 Models

Two models were evaluated:

- **Baseline Model:** A standard classifier trained without any fairness constraints.
- **Adversarially Debiased Model:** A model trained using Adversarial Debiasing to mitigate bias with respect to the protected attribute.

### 3.3 Evaluation Metrics

Model performance was assessed using:

- Accuracy  
- F1-score  

Fairness was evaluated using the following group-level metrics:

- **Demographic Parity Difference (DP Diff)**
- **Equal Opportunity Difference (EO Diff)**
- **Disparate Impact (DI)**

Model interpretability was analyzed using SHAP, comparing feature importance before and after debiasing.

---

## 4. Results

### 4.1 Performance and Fairness Trade-offs

The baseline model achieved strong predictive performance but exhibited substantial bias. Fairness metrics indicated that unprivileged groups were significantly less likely to receive positive outcomes, as reflected by a large demographic parity difference and a disparate impact far from the ideal value of one.

After applying adversarial debiasing, **demographic parity improved substantially**, with DP Diff moving close to zero and DI approaching one. However, these improvements came at a cost: both Accuracy and F1-score decreased noticeably. Moreover, **equal opportunity worsened**, indicating an increased disparity in true positive rates between groups.

These results illustrate the inherent trade-offs of fairness-aware learning, where optimizing certain fairness objectives may negatively affect others and reduce predictive performance.

---

## 5. SHAP-Based Interpretability Analysis

SHAP analysis revealed meaningful changes in feature importance after adversarial debiasing. The direct contribution of the sensitive attribute **sex** was significantly reduced, indicating that the model was constrained from explicitly using protected information.

Nevertheless, features strongly correlated with the sensitive attribute—such as marital status, relationship, and occupation—remained influential. This suggests that while direct discrimination was mitigated, **indirect bias persisted through proxy variables**.

The interpretability analysis complements fairness metrics by providing insight into *how* debiasing reshapes model behavior rather than only *whether* fairness metrics improve.

---

## 6. Discussion

The results demonstrate that adversarial debiasing is effective in improving global measures of fairness, particularly demographic parity and disparate impact. However, the observed degradation in predictive performance and equal opportunity highlights the limitations of optimizing fairness in isolation.

Furthermore, SHAP analysis shows that fairness constraints do not eliminate bias entirely but redistribute importance across correlated features. This reinforces the importance of integrating explainability tools into fairness evaluations to detect both direct and indirect sources of bias.

---

## 7. Conclusion

This study presented a comprehensive evaluation of adversarial debiasing applied to the Adult dataset, combining predictive performance metrics, group fairness measures, and SHAP-based interpretability. While adversarial debiasing substantially improved demographic parity and disparate impact, it introduced significant trade-offs in predictive performance and equal opportunity.

SHAP analysis provided valuable insights into the mechanisms behind these changes, revealing reduced reliance on sensitive attributes and the persistence of indirect bias through proxy features. Future work includes exploring multi-objective optimization strategies, comparing alternative debiasing techniques, and extending the analysis to additional datasets and protected attributes.

---

## References

- Zhang, B. H., Lemoine, B., & Mitchell, M. (2018). *Mitigating unwanted biases with adversarial learning*.
- Hardt, M., Price, E., & Srebro, N. (2016). *Equality of opportunity in supervised learning*.
- Lundberg, S. M., & Lee, S. I. (2017). *A unified approach to interpreting model predictions*.
- Bellamy, R. K. E., et al. (2018). *AI Fairness 360: An extensible toolkit for detecting and mitigating algorithmic bias*.
