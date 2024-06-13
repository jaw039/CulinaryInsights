# CulinaryInsights
**Authors**: Jackie Wang, Brandon Ng
## Project Overview
This is a data science project for DSC80 at UC San Diego. We decided to analyze this data as it allows us to discover new recipes to try in our own kitchen and better understand the nutritional value and benefits of different foods. This knowledge helps us make informed choices to support our fitness goals while still enjoying delicious and healthy meals.

---
## Topic and Introduction
The dataset comprises detailed information from food.com, focusing on recipes submitted since 2008. This timeframe provides us with the most relevant and contemporary eating trends that reflect current nutritional awareness and preferences. **Our main goal of this project is to determine is there a relationship between the nutritional content of a recipe and its average rating?** This goal is significant because understanding the nutritional value of meals can help individuals make informed choices about their diets, supporting their fitness and health goals. By analyzing the nutritional content, we can identify recipes that align with dietary guidelines and promote overall health.

### Introduction to the Datasets in this Study
Recipes Dataset: The first data set we are using contains the information of 83,782 recipes from 2008 to 2018 on food.com, with the following relevant columns:

|Column	                 |Description|
|---                     |---        |
|`'name'	`            |Recipe name|
|`'id'`	                 |Recipe ID|
|`'minutes'`	         |Minutes to prepare recipe|
|`'contributor_id'`	     |User ID who submitted this recipe|
|`'submitted'`	            | Date recipe was submitted|
|`'tags'`	              |Food.com tags for recipe|
|`'nutrition'`	          |Nutrition information in the form [calories (#), total fat (PDV), sugar (PDV), sodium (PDV), protein    (PDV), saturated fat (PDV), carbohydrates (PDV)]; PDV stands for “percentage of daily value”|
|`'n_steps'`	          |Number of steps in recipe|
|`'steps'`	              |Text for recipe steps, in order|
|`'description'`	     | User-provided description|

Interactions Dataset: Contains 731,927 total reviews with the following relevant columns:

|Column|Description|
|---|---|
|`'user_id'`	|User ID|
|`'recipe_id'`	|Recipe ID|
|`'date'`	|Date of interaction|
|`'rating'`	|Rating given|
|`'review'`	|Review text|

In our project, we mainly used two columns from the recipes dataset:`nutrition`and `recipes`. The `nutrition` columns contains information about calories, total fat, sugar, sodium, protein, saturated fat, carbohydrates. We extracted these values into separate columns for detailed analysis. And we also used the `recipes` column to identify recipes tagged as `healthy`.

---
## Cleaning Data and Exploratory Data Analysis
### Data Cleaning
In order to increase the readability and accuracy of our data, we followed the following steps to clean our DataFrame:

1. **Left merge the recipes and interactions datasets together.**: This step was necessary to match user comments and ratings with the corresponding recipes, enabling easier comparisons and comprehensive analysis.
2. **In the merged dataset, we replaced all ratings of 0 with np.nan to handle missing values appropriately.**: Ratings of 0 generally indicate missing values as the lowest valid rating on most websites is 1. Replacing these with np.nan prevents skewed analysis due to invalid ratings.
3. **We calculated the average rating for each recipe.**: Calculating the average rating for each recipe helps summarize user feedback and allows us to compare recipes based on user satisfaction.
4. **We converted the nutrition column to separate columns for calories, total fat, sugar, sodium, protein, saturated fat, and carbohydrates.**: This step makes it easier to analyze individual nutritional components and their impact on healthiness and user ratings.
5. **We calculated the protein-to-carbohydrates and protein-to-calories ratios.**: These ratios provide additional metrics for evaluating the nutritional balance of recipes, helping identify healthier options.
6. **We identified recipes tagged as `healthy` based on the tags column.**: Identifying recipes tagged as "healthy" allows us to analyze their nutritional content and user ratings, providing insights into user perceptions of healthy recipes.
7. **We filled missing descriptions with `No description available` and checked for missing values in other columns.**: Filling missing descriptions ensures all recipes have a description, improving data completeness. Checking for missing values in other columns highlights any remaining data quality issues.

Here is the head of our cleaned dataframe:

| average_rating | calories | total_fat | sugar | sodium | protein | saturated_fat  | carbohydrates | PtoCarb_ratio | PtoCal_ratio | is_healthy |
|----------------|----------|-----------|-------|--------|---------|----------------|---------------|---------------|--------------|------------|
| 4.0            | 138.4    | 10.0      | 50.0  | 3.0    | 3.0     | 19.0           | 6.0           | 0.500000      | 0.021676     | False      |
| 5.0            | 595.1    | 46.0      | 211.0 | 22.0   | 13.0    | 51.0           | 26.0          | 0.500000      | 0.021845     | False      |
| 5.0            | 194.8    | 20.0      | 6.0   | 32.0   | 22.0    | 36.0           | 3.0           | 7.333333      | 0.112936     | False      |
| 5.0            | 878.3    | 63.0      | 326.0 | 13.0   | 20.0    | 123.0          | 39.0          | 0.512821      | 0.022771     | False      |
| 5.0            | 267.0    | 30.0      | 12.0  | 12.0   | 29.0    | 48.0           | 2.0           | 14.500000     | 0.108614     | False      |


These steps were critical in preparing our data for analysis, ensuring the accuracy and completeness of the dataset, and allowing us to draw meaningful insights about the healthiness of recipes based on their nutritional content.


### Univariate Analysis

<iframe
  src="assets/carbs_vs_avgrat.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

This plot allows us to explore how the carbohydrate content in recipes might affect user satisfaction, as reflected by their ratings. 

### Bivariate Analysis

<iframe
  src="assets/CaloriesByAvg.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

This plot suggests that higher-rated recipes tend to have higher calorie content, especially among non-healthy recipes. However, healthy recipes maintain a lower calorie count consistently, regardless of their rating. This insight can be useful for understanding how calorie content influences user ratings and the perception of healthiness in recipes.

### Interesting Aggregates

| is_healthy | PtoCal_ratio | PtoCarb_ratio | calories   | carbohydrates | protein    | saturated_fat | sodium    | sugar     | total_fat |
|------------|--------------|---------------|------------|---------------|------------|---------------|-----------|-----------|-----------|
| False      | 0.079061     | 6.067121      | 450.084108 | 12.913191     | 34.876118  | 46.819121     | 29.026477 | 65.364843 | 37.296644 |
| True       | 0.074865     | 2.762035      | 344.691962 | 17.480654     | 25.764166  | 12.442336     | 28.583125 | 82.616575 | 12.872941 |


This pivot table provides a clear comparison of nutritional components between healthy and non-healthy recipes, offering insights into what differentiates these categories.

---
## Assessment of Missingness
### NMAR Analysis

In our dataset, the `average_rating` column is suspected to be NMAR, where the missingness potentially depends on the ratings themselves. A plausible reason for this pattern could be that users are less likely to leave a rating for recipes that they found disappointing or difficult to execute successfully. This tendency could lead to a disproportionately high number of missing ratings for recipes that did not meet users' expectations or were too complex to prepare satisfactorily. 

To further investigate, an analysis could be conducted to compare the complexity of recipes (number of ingredients, prep time) and the user engagement metrics (completion rate). 


### Missingness Dependency

1. n_steps TVD Analysis:

    Observed TVD: The red dashed line at TVD = 0.43 indicates the observed difference in the distribution of the 'n_steps' between recipes with and without ratings.
    Permutation TVDs: Represented in blue, these show the distribution of TVDs calculated from randomly shuffling the missingness of the 'average_rating' and recalculating the TVD many times.
    Interpretation: The observed TVD is significantly higher than most of the permutation TVDs, as it lies far to the right of the bulk of the blue histogram. This suggests that the difference in 'n_steps' for recipes with and without ratings is greater than what would be expected by chance, indicating that the missingness in 'average_rating' might be dependent on 'n_steps'.

<iframe
  src="assets/N-stepTVD.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>  

2. Minutes TVD Analysis:

    Observed TVD: Here, the red dashed line at TVD = 0.0 shows almost no observed difference in the distribution of `minutes` between recipes with and without ratings.
    Permutation TVDs: The bulk of these values are close to zero, similar to the observed TVD.
    Interpretation: Since the observed TVD is well within the range of the permutation TVDs, this suggests that there is no significant association between the missingness of `average_rating` and the `minutes` it takes to prepare a recipe. The missingness in `average_rating` does not appear to be dependent on `minutes`.

<iframe
  src="assets/minutesTVD.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>  

We conclude that the missingness of `average_rating` is likely independent of the preparation time (`minutes`) listed for the recipes. This suggests that other factors not captured by the `minutes` variable might influence whether a user decides to rate a recipe

---
## Hypothesis Testing

Null Hypothesis: There is no difference in the average protein content between recipes with higher ratings (greater than or equal to 4) and those with lower ratings (less than 4). The observed difference in means is due to random chance.

Alternative Hypothesis (H₁): There is a statistically significant difference in the average protein content between recipes with higher ratings and those with lower ratings.

We will use a significance level of 0.05 since it is the standard convention. 

Test Statistic: We will use the difference in means of protein content between high-rated and low-rated recipes as our test statistic.


### Permutation Test

The permutation test involves randomly shuffling the 'average_rating' values among the recipes multiple times (100 times in this instance), recalculating the mean difference for each permutation. This approach helps us understand if the observed difference could have occurred by chance.

<iframe
  src="assets/diffinMeans.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>  

The observed p-value is significantly higher than the conventional alpha level of 0.05. This result leads us to fail to reject the null hypothesis, suggesting that the difference in protein content between high-rated and low-rated recipes is not statistically significant and could indeed be due to random variation.

Given the p-value and the context of our data, these findings indicate that users' ratings may not be influenced by the protein content of the recipes, or possibly, users do not consistently prefer recipes with higher or lower protein content.

### Framing a Prediction Problem

Problem Type: classification problem

We plan to predict whether a recipe is healthy or not (binary: healthy or not healthy). This is identified by the column `is_healthy` in our dataset, which is marked as True if the recipe is healthy, and False.

We use nutritional content details such as:
`Calories`, `Total Fat`, `Sugar`, `Sodium`, `Protein`, `Saturated Fat` and `Carbohydrates`

We chose the F1-Score because it balances the precision and recall, which is crucial for our dataset, given the potential imbalance between healthy and not healthy recipes. The F1-score helps us to evaluate the model's accuracy in predicting both classes fairly.

### Baseline Model 

Model: Random Forest Classifier

Features in the Model:

    Protein (Quantitative)
    Carbohydrates (Quantitative)

The model utilizes two quantitative features: protein and carbohydrates. These nutrients were selected due to their potential to influence the healthiness of a recipe. Both features were normalized using the StandardScaler to ensure that the model does not bias towards features with inherently larger values.

![Alt text](baselinemodel)


The F1-Score across Categories shows that the model categorizes 'is_healthy = false' more effectively than 'is_healthy = true', likely due to the number of data points in each group as most recipes are labeled as 'not healthy'.

The F1-Score: Indicates low precision (many false positives) and/or low recall (many false negatives), suggesting that the model's performance is not optimal for reliable classification.

Cross-Validation:
    Cross-validation scores indicate that the model is stable and performs consistently well across different subsets of the data, underscoring its robustness

### Final Model

The features used in the final model were average rating, protein to carbohydrate ratio, calories, carbohydrates, protein, saturated fat, sugar, and total fat. These nutritional features are likely to be good predictors of whether a recipe is healthy or not, since the healthiness of a recipe is largely determined by its nutritional composition. Calories, fat, sugar and carbohydrate content are commonly used to assess the healthiness of foods. The protein to carbohydrate ratio captures the balance of macronutrients, which is important for a healthy diet. And the average rating may indirectly reflect recipe healthiness, as users might rate healthier recipes more highly on average.

The modeling algorithm chosen was a Random Forest Classifier. The hyperparameters were tuned using grid search, with the best performing values being a max depth of 12 and 125 estimators.

The final model shows substantial improvement compared to the baseline model:

Test accuracy increased from 79.6% to 82.6%
The F1 score drastically improved from 0.0929 to 0.3873
The F1 score for identifying healthy recipes jumped from 0.0929 to 0.3873
5-fold cross validation scores increased by ~3% on average, showing the model is more consistent

<iframe
  src="assets/FinalModel.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>  