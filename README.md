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

1. **Left merge the recipes and interactions datasets together.**
2. **In the merged dataset, we replaced all ratings of 0 with np.nan to handle missing values appropriately.**
3. **We calculated the average rating for each recipe.**
4. **We converted the nutrition column to separate columns for calories, total fat, sugar, sodium, protein, saturated fat, and carbohydrates.**
5. **We calculated the protein-to-carbohydrates and protein-to-calories ratios.**
6. **We identified recipes tagged as `healthy` based on the tags column.**
7. **We filled missing descriptions with `No description available` and checked for missing values in other columns.**





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