# Analysis of Dementia and Infections in the ALL OF US Database

## 1. Purpose of the Analysis
- Investigate temporal patterns and correlations between infections and their association with dementia and Alzheimer's disease.
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
    - Perform checks and cleaning for the **sex at birth** field.
    - Keep patients that meet the following criteria:
        - At least **60 years old** (CDR version 7).
        - At least **10 EHR entries**.
        - Valid information about **age** and **sex at birth**.

## 5. Statistical Analysis
### Tests Applied
- **Enrichment Analysis**:
    - **Question**: If you have a specific disease (e.g., bacterial infection), are you more likely to also have dementia/Alzheimer's (AD)?
    - **Contingency Table Construction**:
        - `a`: Number of individuals who have both the specific disease (`disease=1`) and dementia/Alzheimer's (`dementia_alzheimer=1`).
        - `b`: Number of individuals who have the specific disease (`disease=1`) but do not have dementia/Alzheimer's (`dementia_alzheimer=0`).
        - `c`: Number of individuals who do not have the specific disease (`disease=0`) but do have dementia/Alzheimer's (`dementia_alzheimer=1`).
        - `d`: Number of individuals who have neither the specific disease (`disease=0`) nor dementia/Alzheimer's (`dementia_alzheimer=0`).
    - **Purpose**: Evaluate whether having a disease is associated with an increased likelihood of also having dementia/Alzheimer's (AD).
- **Violin Plots**:
    - **T-Test**: Test if the median age difference between AD and disease onset is significantly different from zero, indicating a timing difference (e.g., disease first vs. dementia first).
    - **Direction Test**: Determine whether the disease is more likely to occur before AD (First Disease), after AD (First AD), or at the same time.
- **Group Comparisons**:
    - **One-Way ANOVA**:
        - Compare means across multiple groups (e.g., dementia/Alzheimer's vs. infections).
        - Assumptions: Normality and homogeneity of variance.
        - Follow-up: Conduct post hoc tests (e.g., Tukey’s HSD) for significant results.
    - **Mann-Whitney U Test**:
        - Compare two independent groups when data does not meet normality assumptions (e.g., age at dementia/AD onset vs. age at infection).
- **Time-to-Event Analysis**:
    - **Kaplan-Meier Survival Analysis**:
        - Evaluate the time to disease onset (e.g., from bacterial infection to dementia/Alzheimer’s diagnosis).
        - Outputs: Survival curves with log-rank tests for group comparison.
    - Compare survival curves for:
        - Patients with AD/Dementia vs. those without bacterial infections and,
        - Groups with AD/Dementia 1, 2, 3, or more infections.
- **Categorical Data Analysis**:
    - **Enrichment Analysis**:
        - Identify enrichment of Dementia/Alzheimer's in patients with bacterial infections.
        - **Statistical Tests**: Fisher’s Exact Test
- **Key Metrics**:
    - Odds ratios, p-values, confidence intervals.

## 6. Visualization
- **Tools**: Use bar charts, scatter plots, Kaplan-Meier survival curves, histograms, KDE plots, pie charts, and violin plots to summarize findings visually.

### What is KDE (Kernel Density Estimation)?
- **KDE** stands for Kernel Density Estimation.
- It is a statistical method used to estimate the **probability density function (PDF)** of a random variable based on a finite data sample.
- KDE is used to create a **smooth curve** (density function) that represents the underlying distribution of the data.
- **Advantages**:
    - Unlike histograms, which are discrete, KDE provides a **continuous representation** of the data.
- **Kernel**:
    - The "kernel" is a mathematical function used to smooth the data points.
    - **Gaussian kernels** (bell-shaped) are the most commonly used, though others exist.
- **Purpose in This Study**:
    - KDE plots were used to visualize the distribution of ages or other continuous variables to better understand trends in the dataset, without showing summary data from counts less than 20.

## 7. Findings
- Identify significant temporal and statistical patterns linking bacterial infections and neurological conditions.
- Discuss potential causal or correlative relationships.

---

### Additional Details:
- For the **Kaplan-Meier plots**:
    - The **log-rank test** is used to compare survival curves between two groups:
        - Null Hypothesis (H₀): The survival distributions of the two groups are the same.
        - Alternative Hypothesis (H₁): The survival distributions of the two groups are different.
    - Compare the survival experiences of:
        - Patients with AD/Dementia and no infection.
        - Patients with AD/Dementia and 1, 2, 3, or more infections.
- For the **enrichment analysis**:
    - Evaluate whether having a disease increases the likelihood of also having Alzheimer's disease or Dementia.
