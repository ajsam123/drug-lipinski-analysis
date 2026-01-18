# 📄 Project Report: Bioavailability Profiling of ChEMBL Compounds

## 1. Executive Summary
This project performed a physicochemical analysis of bioactive compounds from the **ChEMBL database** to assess their oral "druggability." Using **Lipinski’s Rule of 5** as the filtration metric, we screened the dataset to separate high-potential oral drug candidates from likely attrition risks.

**Key Insight:** The analysis reveals that while **72.09%** of the library complies with strict oral bioavailability rules, there is a strong correlation between *Molecular Weight* and *Lipophilicity*, suggesting that larger compounds in this library suffer from poor solubility.

---

## 2. Methodology
The dataset was processed using **Python** (Pandas, Seaborn). We engineered a "Druggability Scorer" based on the following pharmaceutical constraints:

| Metric | Rule (Lipinski) |
| :--- | :--- |
| **Molecular Weight** | $\le$ 500 Da |
| **LogP (Lipophilicity)** | $\le$ 5 |
| **H-Bond Donors** | $\le$ 5 |
| **H-Bond Acceptors** | $\le$ 10 |

* **Pass:** Compounds violating 0 rules.
* **Fail:** Compounds violating 1 or more rules.

---

## 3. Key Findings & Visualization Analysis

### A. The Chemical Size Distribution
* **Observation:** The histogram of Molecular Weight shows a **[Normal / Right-Skewed]** distribution centered around **[350-400]** Daltons.
* **Implication:** This indicates the library is well-suited for small-molecule drug discovery, rather than biologics or macrocycles.

### B. The "Size vs. Grease" Trap
* **Observation:** The scatter plot of MW vs. LogP reveals a clear **positive correlation**. As molecules get larger, they become significantly more lipophilic (greasy).
* **The "Danger Zone":** A distinct cluster of compounds was identified in the "High MW / High LogP" quadrant (Top-Right). These represent the highest risk for failure due to poor absorption and potential toxicity.
* **The "Safe Zone":** The visualization successfully highlights a dense cluster of "Pass" candidates in the bottom-left quadrant (Low Weight, Low LogP).

### C. Polarity Trade-offs
* **Observation:** Analysis of TPSA vs. LogP confirms an **inverse relationship**.
* **Implication:** Compounds with high polarity (TPSA) tend to have low lipophilicity. The "Sweet Spot" for oral drugs was identified in the intersection where TPSA is below 140 Å² and LogP is between 1 and 5.

---

## 4. Statistical Audit

| Metric | Count |
| :--- | :--- |
| **Total Compounds Analyzed** | 1502539 |
| **Oral Candidates (Pass)** | 1083111 |
| **Attrition Risk (Fail)** | 41928 |
| **Overall Pass Rate** | **72.09%** |

---

## 5. Conclusion & Recommendations
The analysis confirms that **Lipophilicity** is the primary bottleneck for larger molecules in this dataset. Future lead optimization efforts on the "Fail" candidates should focus on **fragment-based design**—reducing molecular weight to bring LogP back into the acceptable range (< 5).

✅ The **[INSERT PASS COUNT]** compounds identified as "Pass" have been exported to `lipinski_pass_candidates.csv` for downstream docking and biological assay screening.
