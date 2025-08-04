# Using-GIS-and-machine-learning-to-monitor-sandbars-along-the-Niger-River-in-the-Niger-Delta-Nigeria.

This repository contains the workflow and analysis for detecting changes in sandbar areas over time using a combination of Geographic Information Systems (GIS) and statistical methods, augmented by machine learning for deeper insights. 

---

## **Table of Contents**

1. [Introduction](#introduction)  
2. [Objectives](#objectives)  
3. [Data Description](#data-description)  
4. [Methodology](#methodology)  
5. [Results](#results)  
6. [Future Work](#future-work)  
7. [How to Use](#how-to-use)  
8. [References](#references)  

---

## **Introduction**

Sandbars are dynamic landforms that change due to natural processes like sedimentation and erosion. Monitoring their changes is essential for understanding ecological dynamics and planning coastal management strategies. This project applies change detection analysis using GIS datasets and machine learning techniques.

---

## **Objectives**

- Analyze changes in sandbar areas over different years.  
- Identify correlations and trends between time periods.  
- Apply statistical tests and machine learning to quantify and predict changes.  
- Visualize findings for enhanced interpretability.

---

## **Data Description**

The dataset consists of sandbar area measurements (in arbitrary units) for the years:
- 1974
- 1984
- 1994
- 2004
- 2014
- 2024  

**Sample Data Representation:**

| Year   | Values (Sample)                  |
|--------|----------------------------------|
| 1974   | 2.22, 24.15, 4.39, ...           |
| 1984   | 544.63, 2.07, 240.42, ...        |
| ...    | ...                              |
| 2024   | 19.31, 10.51, 4.75, ...          |

The data has been preprocessed for statistical analysis and visualization.

---

## **Methodology**

The analysis workflow comprises several steps:

### 1. **Descriptive Statistics**
- **Purpose**: Summarize key statistics such as mean, median, and variability.
- **Code**:
    ```python
    desc_stats = df.describe()
    print(desc_stats)
    ```

---

### 2. **Change Detection Analysis**
- **Purpose**: Compute differences in sandbar areas between consecutive years to identify change magnitude and direction.
- **Code**:
    ```python
    df_diff = df.diff(axis=1)
    print(df_diff)
    ```

---

### 3. **Correlation Analysis**
- **Purpose**: Understand relationships between time periods using:
  - Pearson Correlation: Measures linear relationships.
  - Spearman Rank Correlation: Captures monotonic relationships.
- **Code**:
    ```python
    for year1 in df.columns:
        for year2 in df.columns:
            if year1 != year2:
                corr, _ = pearsonr(df[year1].dropna(), df[year2].dropna())
                print(f"Pearson correlation between {year1} and {year2}: {corr:.2f}")
    ```

---

### 4. **Time Series Analysis**
- **Purpose**: Test for stationarity using the Augmented Dickey-Fuller (ADF) test.
- **Code**:
    ```python
    from statsmodels.tsa.stattools import adfuller
    for year in df.columns:
        result = adfuller(df[year].dropna())
        print(f"ADF Statistic for {year}: {result[0]:.2f}, p-value: {result[1]:.2f}")
    ```

---

### 5. **Hypothesis Testing**
- **Purpose**: Perform a two-sample t-test between the years 1974 and 2024 to evaluate differences in means.
- **Code**:
    ```python
    t_stat, p_val = ttest_ind(df["1974"].dropna(), df["2024"].dropna())
    print(f"T-statistic: {t_stat:.2f}, p-value: {p_val:.2f}")
    ```

---

### 6. **Visualizations**
- **Purpose**: Present findings graphically using boxplots and heatmaps.
- **Code**:
    ```python
    plt.figure(figsize=(10, 6))
    sns.boxplot(data=df)
    plt.title('Boxplot of Sandbar Areas Across Years')
    plt.show()

    plt.figure(figsize=(10, 6))
    sns.heatmap(df.corr(), annot=True, cmap='coolwarm')
    plt.title('Correlation Heatmap')
    plt.show()
    ```

---

## **Results**

### Descriptive Statistics
- Observed increasing variability in sandbar areas across decades.

### Change Detection
- Significant changes identified in specific periods, indicating potential influences like climatic events or anthropogenic factors.

### Correlation Analysis
- Strong correlations observed between consecutive decades, with reduced correlations across non-adjacent years.

### Hypothesis Testing
- T-test revealed a significant difference (p < 0.05) between the sandbar areas in 1974 and 2024.

### Visual Insights
- Boxplots highlighted the variability across decades.
- Heatmaps showed temporal relationships.

---

## **Future Work**

1. **Integration of Machine Learning**:
   - Regression models for sandbar area predictions.
   - Classification algorithms for identifying erosion-prone regions.

2. **Satellite Data Analysis**:
   - Use remote sensing to analyze spatial and temporal sandbar dynamics.

3. **Automation**:
   - Develop a pipeline to process GIS data and generate predictions in real-time.

---

## **How to Use**

### Requirements
- Python 3.8+
- Libraries:
    ```bash
    pip install pandas numpy scipy statsmodels matplotlib seaborn
    ```

### Execution
1. Clone this repository:
    ```bash
    git clone https://github.com/Akajiaku11/sandbar-monitoring
    cd sandbar-monitoring
    ```
2. Run the analysis script:
    ```bash
    python sandbar_analysis.py
    ```

### Outputs
- Descriptive statistics, correlation results, hypothesis testing results.
- Graphical visualizations saved in the `outputs/` folder.

--

## **References**
- Statistical methods: Pearson, Spearman, ADF test.
- Visualization: Matplotlib, Seaborn.
- Machine learning frameworks for future extensions: Scikit-learn, TensorFlow.  

--- 

Feel free to contribute or raise issues!
