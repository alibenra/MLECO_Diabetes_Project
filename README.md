# MLECO_Diabetes_Project

## Heterogenous Causal Effects of In-Hospital Insulin on 30-Day Readmission
**A Double Machine Learning Approach**

---

## Research Question

What is the causal effect of in-hospital insulin prescription on 30-day readmission for diabetic patients?
Does this effect vary across patient subgroups defined by age, gender, and prior hospitalisation history?

Standard regression masks a key problem: clinicians assign insulin to *sicker* patients. This creates the issue of
confounding-by-indication. Essentially, patients who receive insulin are systematically sicker, and sicker patients are 
also more likely to be readmitted. This creates a spurious positive association between insulin and readmission that has 
nothing to do with insulin's actual effect.

We use **Double Machine Learning (DML)** to
disentangle treatment effects from this selection process.

---

## Dataset

**Diabetes 130-US Hospitals** (Strack et al., 2014) — 101,766 hospital encounters across
130 US hospitals, 1999–2008. After cleaning: **67,315 unique patients**, 73 variables.

- **Outcome (Y):** 30-day readmission (`readmitted_30`) — base rate ~9%
- **Treatment (D):** Assigned an insulin treatment (`insulin_any`) — ~51% of patients
- **Covariates (X):** Demographics, lab results, diagnosis, medication history,
  hospitalization patterns, payer type, admission type

---

## Notebooks

| Notebook | Description |
|----------|-------------|
| `Notebook_0_Introduction.ipynb` | Project framing, PICO formalization, causal question |
| `Notebook_1_Data_Preparation.ipynb` | Data cleaning to create the data set used for analysis |
| `Notebook_2_Exploratory_Data_Analysis.ipynb` | EDA and summary statistics |
| `Notebook_3_DAG_and_Causal_Design.ipynb` | Covariate choice, Causal DAG, and identification assumptions |
| `Notebook_4_Modeling_Heterogeneity_Sensitivity.ipynb` | Double Machine Learning Estimation, Heterogenous Treatment Effects analysis, Sensitivity Checks & Conclusion |

---

## Key Findings

- In the **main Double Machine Learning (IRM) specification**, receiving any insulin is associated with an increase of about 1.45 percentage points in the probability of readmission within 30 days. 
- In the **heterogeneity section**, we show how the estimated effect appears somewhat larger for **older patients**, for **women**, and for **patients with prior inpatient hospital visits**, suggesting that the relationship may be stronger among clinically more complex individuals. Therefore, this section, along with some sensitivity checks, allows us to essentially study **policy relevant** situations.
- **Placebo analysis produces an estimate close to zero**, which supports the idea that the main result is capturing a real signal rather than pure modeling noise
- **Results should still be interpreted cautiously and not as definitive proof of a causal harmful effect of insulin itself**
  - Treatment assignment is likely influenced by factors only imperfectly observed in the data, such as clinical judgment (upward confounding bias)
  - The most defensible interpretation is that insulin prescription in this dataset acts as a possible indicator for higher subsequent readmission risk, even after rich adjustment, rather than conclusive harmful evidence

---

## Repo Structure
```
├── code/
│   ├── Notebook_0_Introduction.ipynb
│   ├── Notebook_1_Data_Preparation.ipynb
│   ├── Notebook_2_Exploratory_Data_Analysis.ipynb
│   ├── Notebook_3_DAG_and_Causal_Design.ipynb
│   └── Notebook_4_Modeling_Heterogeneity_Sensitivity.ipynb
├── data/
│   ├── diabetic_data.csv          # raw source data
│   ├── analysis_data.csv          # cleaned analytic dataset
│   └── IDS_mapping.csv
├── ML_presentation.pdf
└── README.md
```

---

## References

Strack et al. (2014). *Impact of HbA1c Measurement on Hospital Readmission Rates.*
BioMed Research International.
