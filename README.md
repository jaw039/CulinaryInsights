# CulinaryInsights
**Authors**: Jackie Wang, Brandon Ng
## Project Overview
This is a data science project for DSC80 at UC San Diego. We decided to analyze this data as it allows us to discover new recipes to try in our own kitchen and better understand the nutritional value and benefits of different foods. This knowledge helps us make informed choices to support our fitness goals while still enjoying delicious and healthy meals.

---
## Topic and Introduction
The dataset comprises detailed information from food.com, focusing on recipes submitted since 2008. This timeframe provides us with the most relevant and contemporary eating trends that reflect current nutritional awareness and preferences. **Our main goal of this project is to detrmine which recipes are healthy based on the nutritional facts** This goal is significant because understanding the nutritional value of meals can help individuals make informed choices about their diets, supporting their fitness and health goals. By analyzing the nutritional content, we can identify recipes that align with dietary guidelines and promote overall health.

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

| average_rating | calories | total_fat | sugar | sodium | protein | saturated_fat  | carbohydrates | PtoCarb_ratio | PtoCal_ratio | is_healthy |
|----------------|----------|-----------|-------|--------|---------|----------------|---------------|---------------|--------------|------------|
| 4.0            | 138.4    | 10.0      | 50.0  | 3.0    | 3.0     | 19.0           | 6.0           | 0.500000      | 0.021676     | False      |
| 5.0            | 595.1    | 46.0      | 211.0 | 22.0   | 13.0    | 51.0           | 26.0          | 0.500000      | 0.021845     | False      |
| 5.0            | 194.8    | 20.0      | 6.0   | 32.0   | 22.0    | 36.0           | 3.0           | 7.333333      | 0.112936     | False      |
| 5.0            | 878.3    | 63.0      | 326.0 | 13.0   | 20.0    | 123.0          | 39.0          | 0.512821      | 0.022771     | False      |
| 5.0            | 267.0    | 30.0      | 12.0  | 12.0   | 29.0    | 48.0           | 2.0           | 14.500000     | 0.108614     | False      |


These steps were critical in preparing our data for analysis, ensuring the accuracy and completeness of the dataset, and allowing us to draw meaningful insights about the healthiness of recipes based on their nutritional content.


### Univariate Analysis



#### Distribution of Protein 
<iframe
  src="assets/protein_by_avg.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


#### Distribution of Calories


### Bivariate Analysis




### Interesting Aggregates




---
## Assessment of Missingness
### NMAR Analysis




### Missingness Dependency




---
## Hypothesis Testing
### Permutation Test