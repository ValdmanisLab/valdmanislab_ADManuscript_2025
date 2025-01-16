# Analysis of Dementia, Bacteria Infections, and Retroviruses

## 1. Purpose of the Analysis
- Investigate temporal patterns and correlations between bacterial infections, retrovirus presence, and their association with dementia and Alzheimer's disease.
- Use SQL to extract relevant data from the electronic health records (EHR) and perform enrichment analysis inside the ALL OF US database.

## 2. Environment Setup
- **Goal**: Prepare the necessary tools and libraries for data extraction, transformation, and analysis.
- **Key Steps**:
    - Validate the environment by listing Python and Conda packages.
    - Import essential libraries:
        - **Data manipulation**: `pandas`, `numpy`
        - **Statistical analysis**: `scipy`, `statsmodels`
        - **Visualization**: `matplotlib`, `seaborn`
        - **Domain-specific tools**: `hail`, `lifelines`

## 3. Data Extraction
- **Source**: SQL database containing patient EHRs from the ALL OF US database.
- **Focus**:
    - Extract patient IDs, diagnosis dates for bacterial infections, retroviruses, dementia, and Alzheimer's disease.
    - Ensure data completeness and consistency.

## 4. Data Processing
- **Transformations**:
    - Convert timestamps into comparable formats.
    - Sort events chronologically to establish order (e.g., bacterial infections preceding retrovirus or vice versa).
- **Data Cleaning**:
    - Handle missing or outlier data.
    - Remove duplicates or irrelevant entries.
    - Keep patients that meet the following criteria:
        - At least **60 years old** (CDR version 7).
        - At least **10 EHR entries**.
        - Valid information about **age** and **sex at birth**.
    - Determine population structure using **16 PCA components** for race analysis.
    - Retrieve genotype information for **APOE e2 and e4** SNPs (`rs7412`, `rs429358`).

## 5. Statistical Analysis
### Tests Applied
- **Enrichment Analysis**:
    - Identify over-representation of bacteria/retrovirus combinations in dementia cases.
- **Temporal Analysis**:
    - Determine the sequence of events and their correlation with disease progression.
- **Group Comparisons**:
    - **One-Way ANOVA**:
        - Compare means across multiple groups (e.g., dementia vs. Alzheimer's vs. no neurological disorder).
        - Assumptions: Normality and homogeneity of variance.
        - Follow-up: Conduct post hoc tests (e.g., Tukey’s HSD) for significant results.
    - **Mann-Whitney U Test**:
        - Compare two independent groups when data does not meet normality assumptions (e.g., retrovirus load in dementia vs. controls).
- **Time-to-Event Analysis**:
    - **Kaplan-Meier Survival Analysis**:
        - Evaluate the time to disease onset (e.g., from bacterial infection to dementia/Alzheimer’s diagnosis).
        - Outputs: Survival curves with log-rank tests for group comparison.
        - Key Metric: Hazard ratios (using Cox proportional hazards models, if applicable).
- **Categorical Data Analysis**:
    - **Enrichment Analysis**:
        - Identify overrepresentation of specific infections in dementia/Alzheimer’s patients.
        - Statistical Tests: Fisher’s Exact Test, Chi-Square Test.
- **Key Metrics**:
    - Odds ratios, p-values, confidence intervals.

## 6. Visualization
- **Tools**: Use bar charts, scatter plots, Kaplan-Meier survival curves, histograms,KDE , and violin plots to summarize findings visually.

## 7. Findings
- Identify significant temporal and statistical patterns linking bacterial infections and neurological conditions.
- Discuss potential causal or correlative relationships.

