# 📄 CIS-2025-19 Research Internship Challenge  
## Bias Detection and Explainability in AI Models

**Name:** Azza Hassan Said  
**Email:** azzahassan1118051@gmail.com  
**Track:** Bias Detection and Explainability in AI Models  
**Platform:** Kaggle Notebooks

---

## 📌 Introduction

This submission presents my solution to the CIS-2025-19 Research Internship technical challenge. The objective was to build an AI-based resume screening model, assess its fairness, explain its decisions, and apply bias mitigation. The task was addressed using a combination of natural language processing, group fairness evaluation, and explainable AI tools.

---
## 🚀 How to Run

### ✅ Run on Kaggle
> No setup required. Just open and run the notebook.

---

## 🧰 1. Dataset & Feature Engineering

- The dataset includes structured attributes like `Gender`, `Age`, `EducationLevel`, `ExperienceYears`, `SkillScore`, `PersonalityScore`, and `RecruitmentStrategy`.
- Synthetic **resume texts** were generated using a predefined template to simulate realistic inputs.
- Mappings applied:
  - `EducationLevel` → degree names (e.g., *Bachelor’s*, *Master’s*)
  - `RecruitmentStrategy` → readable phrases (e.g., *campus recruitment*, *job portal*)
- Gender was encoded as 1 = Male, 0 = Female.
- Data was imbalanced to simulate real-world settings (90% male, 10% female).

---

## 🤖 2. Model Architecture and Performance

Two models were explored:
- **TF-IDF + Logistic Regression**: included text preprocessing and EDA.
- **DistilBERT**: fine-tuned transformer model using Hugging Face with minimal preprocessing.

Final evaluation used the BERT model for its superior performance.

### Initial BERT Results:
- **Accuracy: 82.3%**
- **F1-Score (Hire): 0.79**

## 📊 3. Fairness Evaluation

We measured fairness using standard group fairness metrics:

| **Metric**                   | **Before Mitigation** |
|-----------------------------|------------------------|
| Demographic Parity Diff.    | 0.0951                 |
| Equal Opportunity Diff.     | 0.2113                 |
| Average Odds Difference     | 0.1099                 |

🔍 **Insight**: Model slightly favored male candidates based on recall and opportunity gap.

---

## 🧠 4. Explainability (SHAP Analysis)

We applied **SHAP** to interpret five example predictions (3 "Hire", 2 "No-Hire"):

- Dominant contributing tokens were career-related terms such as `"campus"`, `"Bachelor"`, `"recruitment"`.
- **Gender tokens like `"male"` and `"female"` were always present** but had **negligible SHAP values**.
- No gendered term appeared in top influential tokens.

💡 **Conclusion**: While individual predictions were not biased by gender terms, group-level metrics suggested subtle bias in treatment.

---

## 🧪 5. Bias Mitigation and Trade-offs

We applied **counterfactual data augmentation**:

- Gender terms were swapped in resume text (e.g., `"male"` → `"female"`)
- Gender labels flipped accordingly
- Counterfactual resumes were added to the training set

### Results Before vs. After Augmentation:

| **Metric**                | **Before** | **After** |
|---------------------------|------------|-----------|
| Accuracy                  | 82.3%      | 88.0%     |
| F1-score (Hire)           | 0.72       | 0.80      |
| Demographic Parity Diff.  | 0.0951     | 0.0908    |
| Equal Opportunity Diff.   | 0.2113     | 0.1991    |
| Average Odds Difference   | 0.1099     | 0.1089    |

✅ **Outcome**: The mitigation improved **both performance and fairness**, with minimal trade-offs.

---

## ✅ Conclusion

This project demonstrates a responsible AI pipeline that:
- Applies NLP models to real-world-like resume data
- Evaluates group fairness rigorously
- Uses SHAP for interpretable decision-making
- Successfully mitigates bias through data-level augmentation

The approach balances **accuracy** and **fairness**, showcasing ethical AI design in hiring workflows.

---


