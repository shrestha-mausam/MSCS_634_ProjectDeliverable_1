# Amazon Consumer Behavior Dataset Analysis

## Project Overview

This project analyzes the [Amazon Consumer Behavior Dataset](https://www.kaggle.com/datasets/swathiunnikrishnan/amazon-consumer-behaviour-dataset) to understand consumer behavior patterns and identify factors influencing shopping satisfaction, purchase frequency, and review behavior on Amazon. The dataset contains **602 records** with **23 attributes**, making it suitable for exploratory data analysis and predictive modeling.

## Dataset Summary

### Dataset Characteristics
- **Size**: 602 rows × 23 columns
- **Memory Usage**: ~0.68 MB
- **Data Types**: 
  - 5 numerical variables (age, satisfaction scores, importance ratings)
  - 18 categorical variables (purchase patterns, preferences, demographics)

### Key Variables
- **Demographics**: Age, Gender
- **Purchase Behavior**: Purchase Frequency, Purchase Categories, Browsing Frequency
- **Shopping Experience**: Shopping Satisfaction, Service Appreciation, Improvement Areas
- **Review Behavior**: Review Left, Review Reliability, Review Helpfulness
- **Recommendations**: Personalized Recommendation Frequency, Recommendation Helpfulness
- **Search & Cart**: Product Search Method, Cart Completion Frequency, Cart Abandonment Factors

## Key Insights from Analysis

### 1. Demographic Distribution
- **Age**: Most consumers are between 23-36 years old (median age: 26)
- **Gender**: Female consumers dominate the dataset (~58.5%)
- **Age Outliers**: Found 2 potentially unrealistic ages (ages 3 and 12), which may represent parent responses rather than direct consumer data

### 2. Purchase Patterns
- **Most Common Frequency**: "Few times a month" is the most common purchase pattern (~34%)
- **Browsing Behavior**: "Few times a week" is the most common browsing frequency (~41%)
- **Product Categories**: "Beauty and Personal Care" is the most frequently purchased category

### 3. Shopping Satisfaction
- Satisfaction levels cluster around **moderate ratings (2-3 on a 5-point scale)**
- Mean satisfaction: 2.46 out of 5
- **Strong Correlation** with Rating Accuracy (0.514) and Personalized Recommendation Frequency (0.438)

### 4. Behavioral Relationships
- **Purchase Frequency ↔ Review Behavior**: Consumers who purchase more frequently are more likely to leave reviews
- **Personalized Recommendations**: Show varying impact on satisfaction across different frequency levels
- **Age Groups**: Younger consumers (18-25) exhibit different purchase patterns compared to older groups
- **Service Appreciation**: Most consumers appreciate "Competitive prices" and "Product recommendations"

### 5. Improvement Areas
- **Top Concerns**: 
  - Product quality and accuracy
  - Customer service responsiveness
  - Reducing packaging waste

### 6. Search & Navigation
- **Product Search Method**: "Categories" is most popular (~37%), followed by "Keyword" searches (~36%)
- **Search Exploration**: Most consumers explore multiple pages of results (73%)

## Major Steps in Data Cleaning

### 1. Handling Missing Values
- **Challenge**: Identified 2 missing values (0.33%) in the `Product_Search_Method` column
- **Solution**: Used mode imputation to fill missing values with the most frequent value ("categories")
- **Result**: All missing values successfully handled without data loss

### 2. Removing Duplicates and Correcting Inconsistencies
- **Duplicate Check**: No duplicate rows found in the dataset
- **Column Name Issues**: 
  - Identified columns with trailing spaces: `'Personalized_Recommendation_Frequency '` and `'Rating_Accuracy '`
  - **Solution**: Renamed columns to remove trailing spaces and ensure consistency
- **Categorical Value Cleaning**:
  - Checked for trailing/leading spaces in categorical values across all object-type columns
  - Applied `.strip()` method to clean any inconsistent whitespace
- **Result**: Dataset cleaned of naming inconsistencies and whitespace issues

### 3. Identifying and Addressing Noisy Data
- **Outlier Detection**: Used Interquartile Range (IQR) method to identify outliers:
  - **Age**: 20 outliers (3.32%), range 3-67 (normal range: 3.5-55.5)
  - **Personalized Recommendation Frequency**: 35 outliers (5.81%)
  - **Rating Accuracy**: 21 outliers (3.49%)
  - **Shopping Satisfaction**: 17 outliers (2.82%)
  
- **Age Validation**: 
  - Flagged 2 rows with potentially unrealistic ages (3 and 12)
  - **Decision**: Preserved these values as they may represent valid parent responses
  
- **Categorical Inconsistencies**: 
  - Checked for case variations and typos in categorical columns
  - **Result**: No major inconsistencies found after initial cleaning

## Major Steps in Exploratory Data Analysis

### 1. Distribution Analysis
- Created histograms for all numerical variables showing their distributions
- Analyzed categorical variable distributions using bar charts and pie charts
- Key findings: Right-skewed age distribution, clustering around moderate satisfaction levels

### 2. Outlier Detection
- Generated box plots for all numerical columns using IQR method
- Visualized outliers and identified their potential impact
- **Decision**: Outliers preserved as they may represent valid extreme survey responses

### 3. Feature Relationship Analysis
- **Correlation Matrix**: Computed and visualized correlations between numerical variables
- **Key Correlations Identified**:
  - Shopping Satisfaction ↔ Rating Accuracy: **0.514** (moderate positive)
  - Shopping Satisfaction ↔ Recommendation Frequency: **0.438** (moderate positive)
  - Reviews Importance ↔ Satisfaction: **0.402** (moderate positive)
  
### 4. Behavioral Pattern Analysis
- Created crosstabulations to examine relationships between:
  - Purchase Frequency and Gender
  - Review Left status and Purchase Frequency
  - Shopping Satisfaction and Personalized Recommendation Frequency
  - Age Groups and various behavioral metrics

### 5. Age Group Segmentation
- Created age groups: 18-25, 26-35, 36-45, 45+
- Analyzed how purchase patterns and satisfaction vary across age groups
- Found distinct behavioral differences between younger and older consumers

## Challenges Encountered and Solutions

### Challenge 1: Column Name Inconsistencies
- **Problem**: Two columns had trailing spaces (`'Personalized_Recommendation_Frequency '` and `'Rating_Accuracy '`), causing potential issues in column referencing
- **Impact**: Could lead to KeyError when accessing columns by exact name
- **Solution**: 
  - Renamed columns to remove trailing spaces
  - Standardized column naming convention throughout the analysis
- **Prevention**: Applied systematic column name cleaning at the start of data cleaning process

### Challenge 2: Mixed Data Types
- **Problem**: Dataset contains both numerical (5) and categorical (18) variables requiring different preprocessing strategies
- **Impact**: Requires careful feature engineering and encoding for modeling
- **Solution**: 
  - Separated numerical and categorical columns for distinct analysis
  - Applied appropriate visualization techniques for each data type
  - Documented encoding strategies needed for future modeling

### Challenge 3: Outlier Interpretation
- **Problem**: Some numerical variables showed outliers (e.g., age 3, age 67) that could be either data errors or valid responses
- **Impact**: Need to decide whether to remove, cap, or preserve these values
- **Solution**: 
  - Used domain knowledge: age 3 likely represents parent responding on behalf of child
  - Preserved outliers as valid survey responses
  - Documented rationale for future reference
  - Noted in analysis that these may need special handling in modeling if required

### Challenge 4: Categorical Variables with Many Unique Values
- **Problem**: Some columns like `Purchase_Categories` have 29 unique values, and `Improvement_Areas` has 18 unique values
- **Impact**: Difficult to visualize effectively; may need feature engineering for modeling
- **Solution**: 
  - Used top-N visualizations (e.g., top 6 service appreciation factors)
  - Recommended extracting features from multi-value categories (e.g., count of categories)
  - Documented feature engineering recommendations for future work

### Challenge 5: Sample Size Limitations
- **Problem**: Dataset has 602 rows, which limits complex model complexity
- **Impact**: Need to avoid overfitting; may not support very complex models
- **Solution**: 
  - Recommended stratified k-fold cross-validation
  - Suggested simpler models or ensemble methods that work well with smaller datasets
  - Documented sample size considerations for modeling phase

### Challenge 6: Ordinal Scale Interpretation
- **Problem**: Satisfaction and rating scales (1-5) are ordinal but treated as numerical in correlation analysis
- **Impact**: Correlation values may not fully capture ordinal relationships
- **Solution**: 
  - Used correlations as initial exploration tool
  - Recommended ordinal regression methods for proper modeling
  - Documented ordinal nature for future modeling considerations

## Future Modeling Recommendations

### Target Variables
- **Primary**: `Shopping_Satisfaction` (ordinal, 1-5 scale)
- **Secondary**: `Review_Left` (binary), `Purchase_Frequency` (categorical)

### Feature Engineering
- Create age groups (already demonstrated)
- Extract features from `Purchase_Categories` (count, presence indicators)
- Combine related review metrics into composite scores
- Consider interaction terms (Age × Gender, Purchase_Frequency × Satisfaction)

### Modeling Approaches
- **Classification**: For `Review_Left` and `Purchase_Frequency`
- **Ordinal Regression**: For `Shopping_Satisfaction` (respects 1-5 ordering)
- **Ensemble Methods**: Given mixed data types (numerical + categorical)

### Validation Strategy
- Stratified k-fold cross-validation
- Monitor for overfitting given dataset size
- Maintain distribution of key categorical variables in train-test splits

## Technologies Used

- **Python 3.13**
- **Pandas**: Data manipulation and analysis
- **NumPy**: Numerical computations
- **Matplotlib & Seaborn**: Data visualization
- **KaggleHub**: Dataset download

## File Structure

```
MSCS_634_ProjectDeliverable_1/
├── notebook.ipynb          # Main analysis notebook
├── requirements.txt        # Python dependencies
├── README.md               # This file
└── venv/                   # Virtual environment
```

## Running the Analysis

1. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

2. Ensure Kaggle API credentials are set up in `~/.kaggle/kaggle.json`

3. Open and run `notebook.ipynb` in Jupyter Lab or Jupyter Notebook

## Author
Mausam Shrestha

MSCS 634 Project Deliverable 1 - Data Cleaning and Exploratory Data Analysis

---

*This analysis forms the foundation for future predictive modeling tasks focused on consumer behavior prediction and satisfaction analysis.*

