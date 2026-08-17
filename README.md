# Data Preprocessing and Feature Extraction Assignment

## 1. Dataset Source
- **Platform:** Kaggle / Open-Data Repository
- **Dataset Name:** Lung Cancer Survey Dataset
- **URL / Source Link:** "https://www.kaggle.com/datasets/akashnath29/lung-cancer-dataset/data"
- **Overview:** Survey dataset containing patient demographic details, symptoms (such as coughing, shortness of breath, fatigue), lifestyle factors (smoking, alcohol consumption), and lung cancer diagnosis outcomes.

## 2. Number of Rows/Columns Before Preprocessing
- **Initial Rows:** 3,000
- **Initial Columns:** 16

## 3. Problems Identified
During the initial inspection of the raw dataset, the following data quality issues were identified:
- **Duplicate Records:** Identified 2 identical duplicate rows in the dataset.
- **Inconsistent Formatting:** Column headers were in uppercase and needed conversion to standardized `snake_case`.
- **Missing Values:** Potential missing/null entries across survey responses and demographic features.
- **Outliers:** Extreme values present in numerical features such as `age`.
- **Unencoded Categorical Features:** Text-based categorical columns (`gender` and target `lung_cancer`) could not be directly fed into machine learning algorithms.
- **Unscaled Numerical Features:** Features had varying numerical scales, which can bias distance-based algorithms.

## 4. Preprocessing Techniques Applied

1. **Duplicate Removal:** 
   - Identified and dropped 2 duplicate rows, bringing row count down from **3,000 to 2,998**.
2. **Column Formatting & Type Correction:** 
   - Converted all column names to lowercase and replaced spaces/special characters with underscores.
   - Verified that data types aligned with expected types (`int64` for survey metrics, `object` for strings).
3. **Missing Value Imputation:** 
   - Imputed missing numerical features using the **Median**.
   - Imputed missing categorical features using the **Mode**.
   - Verified 0 remaining missing values.
4. **Outlier Detection & Capping:** 
   - Used the **Interquartile Range (IQR)** method ($Q1 - 1.5 \times IQR$ to $Q3 + 1.5 \times IQR$).
   - Capped extreme values to boundaries without removing valid entries.
5. **Feature Extraction:** 
   - Created interaction and ratio features by combining related symptom indicators (e.g., combining respiratory symptoms like `coughing` and `shortness_of_breath`).
   - Expanded column count from **17 to 18**.
6. **Categorical Encoding:** 
   - Converted binary categorical variables (`gender` and `lung_cancer`) into numerical 0/1 formats using `pd.get_dummies`.
7. **Numerical Normalization/Standardization:** 
   - Standardized continuous features using **`StandardScaler`** to achieve a mean of 0 and standard deviation of 1.

## 5. Number of Rows/Columns After Preprocessing
- **Final Rows:** 2,998
- **Final Columns:** 18

## 6. Final Cleaned Dataset
- The output file is saved in the repository as: **[`LungCancer_cleaned_dataset.csv`](./LungCancer_cleaned_dataset.csv)**
