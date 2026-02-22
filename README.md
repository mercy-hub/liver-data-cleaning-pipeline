
# Liver Patient Dataset – Data Cleaning and Validation Pipeline

Overview

This project demonstrates a structured data cleaning and validation workflow applied to a clinical dataset (Liver Patient Dataset).

The goal was not to maximize predictive performance, but to transform raw patient records into a clean, reliable, and reproducible dataset while clearly documenting the reasoning behind each transformation decision.

Process Flow

The notebook follows a deliberate sequence:
1. Load raw dataset  
2. Perform initial inspection and visualization  
3. Identify structural data issues  
4. Apply targeted cleaning decisions  
5. Validate post-cleaning integrity  
6. Perform light modeling for verification  
7. Export cleaned dataset  
Each step was chosen to reflect a real-world data engineering and QA workflow.

Initial Data Assessment

Raw inspection revealed:
- Missing values across numeric and categorical columns  
- 902 missing entries in the Gender column  
- Over 11,000 exact duplicate rows  
- Moderate imbalance in the target variable  
- Mixed data types  

Before applying any cleaning, visualizations were generated to understand distribution patterns and correlations. This ensured decisions were data-informed rather than arbitrary.

Cleaning Decisions and Rationale

Missing Values
Gender (Categorical):
Mode imputation was selected because it preserves the most frequent real-world category without introducing artificial values. Since the variable is binary, this approach maintains distribution consistency.

Numeric Clinical Features:
Median imputation was chosen instead of mean because clinical biomarkers often exhibit skewed distributions. The median is robust to outliers and better preserves realistic medical ranges.
The objective was to correct missingness without distorting the dataset’s statistical structure.

Duplicate Removal
Over 11,000 exact duplicate rows were identified.
Duplicates were removed because they:

- Artificially inflate statistical relationships  
- Bias model evaluation metrics  
- Distort correlation analysis  
- Suggest potential data replication during collection  
Removing duplicates ensures unbiased representation and prevents inflated performance results.

Categorical Encoding
The Gender column was label-encoded.
Label encoding was chosen instead of one-hot encoding because:

- The feature is binary  
- One-hot encoding would introduce unnecessary dimensionality  
- Simplicity improves interpretability  
- Tree-based models handle encoded integers effectively  
The decision prioritized structural efficiency without sacrificing modeling compatibility.

Class Imbalance Evaluation
The target variable exhibited moderate imbalance.
Rather than immediately applying synthetic resampling methods (such as SMOTE), the imbalance was first quantified and documented. Since the project emphasizes structural cleaning and dataset integrity rather than optimization, the original distribution was preserved to reflect real-world data characteristics.

Scaling Strategy
Feature scaling was applied after train-test splitting.
This decision was made to prevent data leakage. Scaling before splitting would allow test data information to influence the training process.

MinMax scaling was selected because:
- It normalizes values into a bounded range  
- It preserves proportional differences  
- It does not assume normal distribution  
- Clinical values benefit from consistent scaling  

Post-Cleaning Validation
After transformations:
- No missing values remained  
- Duplicate rows were removed  
- Data types were standardized  
- Class distribution was reassessed  
- Outliers were visualized and examined  
These validation checks confirmed the dataset was structurally sound and analysis-ready.

Light Modeling for Structural Verification
A Random Forest classifier was trained after cleaning.
The purpose was not model optimization, but to confirm:
- Features were correctly encoded  
- No leakage occurred  
- The dataset was ready for downstream analytical use  
Random Forest was chosen because it is robust, handles non-linear relationships well, and requires minimal tuning. It serves as a reliable structural validation tool.

Final Output
The cleaned dataset was exported as:
cleaned_liver_data.csv
All transformations are implemented in:
cleaning_pipeline.ipynb

The notebook can be executed sequentially to reproduce the entire process.

Project Emphasis
This project focuses on:
- Data quality assurance  
- Transparent decision-making  
- Structured cleaning pipelines  
- Reproducibility  
- Responsible transformation practices  

The objective was to demonstrate the role of a data professional acting as the bridge between raw data and reliable analytical output.
