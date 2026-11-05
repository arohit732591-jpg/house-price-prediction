# 🏡 House Price Prediction Using Machine Learning

## 1. Project Overview

Buying a house is one of the biggest financial decisions a person makes. However, determining whether a property's asking price is reasonable can be difficult because house prices depend on several factors, including location, size, quality, age, garage capacity, and other features.

This project uses data analysis and machine learning to predict house sale prices, identify the features that influence property values, and provide data-driven suggestions to help customers make better purchasing decisions.

## 2. Project Objectives

The main objectives are:

- Perform exploratory data analysis to understand the housing market.
- Develop machine learning models to predict house sale prices.
- Identify the most important features influencing property prices.
- Compare multiple regression models and optimize their performance.
- Analyze neighborhoods based on price and value for money.
- Build a house recommendation function based on customer budgets and requirements.

## 3. Dataset Description

**Dataset file:** `data.csv`

The dataset contains 1,460 house sales with 80 input features and one target variable, `SalePrice`.

The target variable represents the house sale price in US dollars.

### Main Feature Categories

| Category | Example Features |
|---|---|
| Location and Lot | `Neighborhood`, `LotArea`, `LotFrontage`, `MSZoning` |
| House Type and Style | `BldgType`, `HouseStyle`, `YearBuilt` |
| Quality and Condition | `OverallQual`, `OverallCond`, `KitchenQual` |
| Size and Rooms | `GrLivArea`, `TotalBsmtSF`, `BedroomAbvGr` |
| Garage | `GarageCars`, `GarageArea`, `GarageType` |
| Sale Information | `YrSold`, `SaleCondition` |

**Target variable:** `SalePrice`

## 4. Data Cleaning and Preprocessing

The following data preparation steps were performed:

- Checked missing values and duplicate records.
- Filled missing categorical values with `None` where the absence of a feature was meaningful, such as no garage or basement.
- Filled `LotFrontage` using the neighborhood median.
- Filled missing `MasVnrArea` values with zero.
- Filled the missing `Electrical` value using the mode.
- Removed `Id` and `GarageYrBlt` columns.
- Identified and removed unusual house-price outliers with living area above 4,000 sq. ft. and sale price below $300,000.

## 5. Exploratory Data Analysis (EDA)

Exploratory data analysis was performed to understand the relationships between house characteristics and sale prices.

The analysis included:

- Distribution of house sale prices.
- Price comparisons across neighborhoods.
- Relationship between overall quality and sale price.
- Living area versus sale price.
- Effect of construction year and garage capacity.
- Kitchen quality and building type comparisons.
- Correlation analysis of numerical features.
- Neighborhood-level price comparisons.

### Key Findings

- House prices are right-skewed, with a median sale price of approximately **$163,000**.
- Overall quality has a strong positive correlation with sale price (approximately 0.80).
- Above-ground living area also has a strong correlation with sale price (approximately 0.73).
- Basement area, garage capacity, and first-floor area are also important price-related features.
- Neighborhood has a considerable influence on property prices.
- The median price varies significantly across neighborhoods.

## 6. Feature Engineering

New features were created to better represent house characteristics:

- `TotalSF`: Combined basement, first-floor, and second-floor area.
- `HouseAge`: Age of the house at the time of sale.
- `RemodAge`: Years since the last remodeling.
- `TotalBathrooms`: Combined full and half bathrooms, including basement bathrooms.
- `TotalPorchSF`: Combined porch area.

Additional preprocessing included:

- Converting quality ratings into numerical values.
- Treating `MSSubClass` as a categorical variable.
- Applying one-hot encoding to categorical features.

## 7. Model Development

The dataset was divided into training and testing sets using an 80:20 split, with `random_state=42`.

Five regression model configurations were evaluated:

1. Linear Regression
2. Random Forest Regressor
3. Gradient Boosting Regressor
4. Tuned Random Forest using GridSearchCV
5. Tuned Gradient Boosting using GridSearchCV

Hyperparameter tuning was performed using GridSearchCV with 3-fold cross-validation.

The final Gradient Boosting model was also evaluated using 5-fold cross-validation.

## 8. Model Evaluation

The models were evaluated using:

- **MAE (Mean Absolute Error):** Average absolute difference between actual and predicted house prices.
- **RMSE (Root Mean Squared Error):** Measures prediction error while giving greater weight to larger errors.
- **R² Score:** Measures how much variation in house prices is explained by the model.

### Final Model Performance

The tuned Gradient Boosting model achieved the following recorded test-set results:

| Evaluation Metric | Result |
|---|---:|
| MAE | $14,244 |
| RMSE | $20,204 |
| R² Score | 0.926 |

The model achieved an R² score of approximately 0.92 in cross-validation as well.

Additional error analysis showed:

- Average prediction error of approximately 8.9% of the actual price.
- Median prediction error of approximately 5.9%.
- Approximately 76% of test houses were predicted within 10% of their actual sale price.

**Selected Model:** Tuned Gradient Boosting Regressor.

## 9. Feature Importance and Key Insights

Feature importance analysis identified the following major price drivers:

- `TotalSF` — approximately 43% importance.
- `OverallQual` — approximately 30% importance.
- Other relevant features include total bathrooms, house age, garage capacity, basement quality, kitchen quality, and lot area.

Together, total area and overall quality account for approximately 72% of the model's feature importance.

### What-If Analysis

The notebook also examined how changing individual house features affects predicted prices.

| Feature Change | Approximate Predicted Price Change |
|---|---:|
| Additional 500 sq. ft. of area | +$18,600 |
| One-point increase in overall quality | +$9,800 |
| One additional bathroom | +$7,100 |
| One-level improvement in kitchen quality | +$4,800 |
| One additional garage space | +$3,600 |

These are model-based estimates of association, not guaranteed increases in actual property value.

## 10. Neighborhood Analysis and Customer Recommendations

Neighborhoods were grouped into three price categories:

- Budget
- Mid-range
- Premium

The analysis compared neighborhood median prices, average quality, price per square foot, and estimated value for money.

A custom `recommend_houses()` function was developed to filter and rank properties according to:

- Customer budget
- Minimum number of bedrooms
- Minimum number of bathrooms
- Garage capacity
- Minimum overall quality
- Preferred neighborhoods

The function ranks suitable properties based on the difference between actual and model-predicted prices.

This provides a practical way to identify properties that may offer better value for a customer's requirements.

## 11. Technologies and Libraries

- Python
- Jupyter Notebook
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn

## 12. Repository Structure

```text
house-price-prediction/
│
├── House_Price.ipynb.ipynb
├── data.csv
├── README.md
└── requirements.txt

```

## 13. How to Run This Project

1. Clone or download this repository.
2. Open the project folder in VS Code or Jupyter Notebook.
3. Install the required Python libraries:
   ```bash
   pip install -r requirements.txt
4. Make sure `data.csv` is in the same folder as the notebook.
5. Open `House_Price.ipynb` and execute the notebook cells in order.


## 14. Limitations and Future Improvements

### Limitations

- The dataset contains historical house sales from 2006 to 2010 in one city.
- Historical prices may not represent current real estate market values.
- Information about school quality, commute times, crime rates, and actual property condition is not included.
- Model predictions are estimates and should not replace professional property inspections or market research.

### Future Improvements

- Train and evaluate the model using more recent housing data.
- Explore log transformation of the target variable.
- Experiment with additional regression algorithms such as XGBoost.
- Incorporate more detailed location and neighborhood information.
- Develop an interactive house-price prediction application.

## 15. Conclusion

This project demonstrates an end-to-end machine learning workflow for house price prediction, covering data cleaning, exploratory data analysis, feature engineering, regression modeling, hyperparameter tuning, and model evaluation.

The tuned Gradient Boosting model achieved an R² score of 0.926 on the test set and demonstrated consistent performance through cross-validation.

The project also explored feature importance, neighborhood price differences, and customer-oriented property recommendations.

Overall, it provided practical experience in applying machine learning and data analysis to a real-world real estate pricing problem.

---

**Project Domain:** Data Science | Machine Learning | Real Estate  
**Project Type:** Regression | Predictive Analytics | Exploratory Data Analysis
