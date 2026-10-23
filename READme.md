# Recipe Website Traffic Prediction

## Project Overview

This project uses data analysis and machine learning to predict whether a recipe is likely to receive **high or low website traffic**.

The business currently selects recipes to feature on its homepage. Since featuring popular recipes can increase traffic to other parts of the website by as much as 40%, identifying recipes with high traffic potential could help increase website visits and create opportunities for more subscriptions.

The objective is to develop a classification model that helps the product team make more informed, data-driven decisions about which recipes to promote.

## Business Objectives

- Predict whether a recipe is likely to receive high or low traffic.
- Identify recipe characteristics associated with higher website traffic.
- Compare machine learning models to determine which performs best.
- Evaluate model performance against the business target of at least 80% accuracy.
- Provide actionable recommendations for recipe selection and website promotion.

## Dataset

The project uses the `recipe_site_traffic_2212.csv` dataset.

The dataset contains **947 recipes** and includes information about:

| Feature        | Description                                     |
| -------------- | ----------------------------------------------- |
| `recipe`       | Recipe identifier                               |
| `calories`     | Calories per recipe                             |
| `carbohydrate` | Carbohydrate content                            |
| `sugar`        | Sugar content                                   |
| `protein`      | Protein content                                 |
| `category`     | Recipe category                                 |
| `servings`     | Number of servings                              |
| `high_traffic` | Target variable indicating high or low traffic  |
| `is_snack`     | Additional feature used in the prepared dataset |

The `high_traffic` variable is the target used to train the classification models.

## Data Cleaning and Preparation

The following data preparation steps were performed:

1. Inspected the dataset structure and data types.
2. Checked for missing values.
3. Identified 52 missing values in each of the four nutritional columns: calories, carbohydrates, sugar, and protein.
4. Handled missing nutritional values using median imputation.
5. Checked and standardised recipe category labels.
6. Prepared categorical features using one-hot encoding.
7. Separated the features from the target variable.
8. Split the dataset into training and testing sets.

### Dataset Split

| Dataset      | Number of Records |
| ------------ | ----------------: |
| Training set |               757 |
| Testing set  |               190 |
| Total        |               947 |

After preprocessing, the feature matrix contained 16 encoded features.

## Exploratory Data Analysis

Exploratory data analysis (EDA) was performed to understand the distribution of recipe traffic, differences between recipe categories, and relationships between nutritional characteristics.

### Key Findings

**1. Website traffic distribution**

- High-traffic recipes: 574 (60.61%).
- Low-traffic recipes: 373 (39.39%).

High-traffic recipes represent the majority of observations in the dataset.

**2. Recipe categories**

- Chicken had the highest number of recipes, with 172.
- Vegetable recipes showed the strongest traffic performance among the categories analysed.
- Beverages showed the lowest traffic performance.

**3. Nutritional characteristics**

- High-traffic recipes had a slightly higher median calorie value than low-traffic recipes.
- Protein and calories had the strongest positive correlation among the nutritional variables examined, at approximately 0.17.

These findings suggest that recipe category and nutritional characteristics may provide useful predictive information. However, associations in the dataset do not establish that these characteristics cause higher traffic.

## Machine Learning Models

This project treats recipe traffic prediction as a **supervised binary classification problem**.

Three classification algorithms were trained and evaluated:

1. **Decision Tree Classifier** — provides an interpretable approach to classification.
2. **Random Forest Classifier** — combines multiple decision trees to capture patterns and reduce reliance on a single tree.
3. **Logistic Regression** — provides a baseline classification approach for comparing predictive performance.

The dataset was divided into training and testing sets. Cross-validation was also used to compare model performance across multiple data splits.

## Model Evaluation

The models were evaluated using cross-validation accuracy and test-set accuracy.

### Performance Comparison

| Model               | Cross-Validation Accuracy | Test Accuracy |
| ------------------- | ------------------------: | ------------: |
| Decision Tree       |                    72.97% |        73.68% |
| Random Forest       |                    75.51% |    **76.84%** |
| Logistic Regression |                **76.03%** |        75.79% |

### Key Results

- Random Forest achieved the highest test accuracy of **76.84%**.
- Logistic Regression achieved the highest cross-validation accuracy of **76.03%**.
- Decision Tree achieved a test accuracy of 73.68%.

Random Forest is the current leading candidate based on test accuracy, while Logistic Regression provides a useful comparison because of its slightly higher cross-validation score.

### Business Target

The original business objective was to achieve at least **80% prediction accuracy**.

The best observed test accuracy was 76.84%, meaning the target has not yet been achieved.

Further model improvement and validation are recommended before operational deployment.

### Business Metric to Monitor

In addition to overall accuracy, the business should monitor **high-traffic recall**.

High-traffic recall measures the proportion of recipes that actually receive high traffic that the model correctly identifies.

This is important because incorrectly classifying a potentially popular recipe as low traffic could cause the business to miss an opportunity to promote it.

High-traffic precision should also be monitored to determine how often recipes predicted to receive high traffic actually belong to the high-traffic class.

## Feature Importance

The Random Forest model identified the following five features as the most important according to its feature-importance scores:

| Rank | Feature            | Importance |
| ---- | ------------------ | ---------: |
| 1    | Beverages category |     0.2124 |
| 2    | Vegetable category |     0.1478 |
| 3    | Potato category    |     0.1102 |
| 4    | Protein            |     0.1060 |
| 5    | Breakfast category |     0.0823 |

These scores indicate how the model used the features when making predictions. They do not establish that a feature causes high or low traffic.

The prominence of recipe categories suggests that category-level information may be useful when prioritising recipes for further investigation and promotion.

## Business Recommendations

Based on the analysis and model results, the following recommendations are proposed.

### 1. Use Predictions to Support Homepage Selection

Use the model to help identify recipes that may have high traffic potential. Predictions should support, rather than completely replace, the product team's existing judgement.

### 2. Investigate Recipe Categories

Conduct further analysis of Vegetable, Chicken, and other recipe categories to understand which characteristics are associated with stronger traffic.

### 3. Improve Model Performance

The current best test accuracy of 76.84% falls short of the 80% business target.

Further work should include:

- Hyperparameter tuning.
- Comparing additional classification algorithms.
- Reviewing high-traffic precision and recall.
- Investigating additional predictive features.
- Validating model performance on unseen data.

### 4. Conduct a Controlled Pilot

Test model-assisted recipe selection on the website and compare the results against an appropriate comparison group.

Monitor actual website traffic and engagement to establish whether the recommendations improve business outcomes.

### 5. Monitor Performance Over Time

Track model performance and actual recipe traffic regularly. Retrain or review the model when performance deteriorates or website traffic patterns change.

## Tools and Technologies

- **Python** — data analysis and model development.
- **Pandas** — data manipulation and cleaning.
- **NumPy** — numerical operations.
- **Matplotlib and Seaborn** — exploratory data visualisation.
- **Scikit-learn** — preprocessing, model training, cross-validation, and evaluation.
- **Jupyter Notebook** — project analysis and documentation.

## Project Files

The project includes the following main deliverables:

| File or Folder                     | Purpose                                                                |
| ---------------------------------- | ---------------------------------------------------------------------- |
| `README.md`                        | Project overview, methodology, findings, and recommendations           |
| `notebook.ipynb`                   | Data cleaning, exploratory analysis, model development, and evaluation |
| `recipe_site_traffic_2212.csv`     | Original dataset                                                       |
| `recipe_traffic_model_results.csv` | Exported model results                                                 |
| `charts/`                          | Visualisations generated during the analysis                           |

_The file and folder names above reflect the project structure discussed during development. Confirm that they match the final GitHub repository before publishing._

## How to Run the Project

1. Clone or download this repository.

2. Ensure Python is installed.

3. Install the required libraries:

   ```bash
   pip install pandas numpy matplotlib seaborn scikit-learn jupyter
   ```

4. Open the project notebook:

   ```bash
   jupyter notebook notebook.ipynb
   ```

5. Run the notebook cells in order to reproduce the analysis and model evaluation.

Ensure the dataset is available at the file path referenced in the notebook.

## Limitations

- The best observed test accuracy is below the 80% business target.
- Model accuracy alone does not indicate how effectively high-traffic recipes are identified.
- Feature importance indicates predictive contribution, not causation.
- Historical traffic patterns may not remain stable over time.
- Improved prediction accuracy does not automatically guarantee increased subscriptions or revenue.

A controlled website experiment is needed to measure the actual business impact of model-assisted recipe selection.

## Conclusion

This project demonstrates how data analysis and machine learning can support more informed decisions about recipe promotion.

Three classification models were compared, with Random Forest achieving the highest test accuracy of **76.84%**. Exploratory analysis also highlighted differences in traffic across recipe categories and relationships between nutritional variables.

Although the model has not yet reached the 80% target, the results provide a foundation for further model improvement and controlled testing.

The recommended next step is to improve high-traffic identification, pilot the model in the recipe-selection process, and measure whether model-assisted promotion produces meaningful increases in website traffic and subscriptions.

---

**Project focus:** Data Analytics | Machine Learning | Binary Classification | Business Intelligence
