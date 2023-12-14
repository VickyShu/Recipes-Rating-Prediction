# Recipes Rating Prediction

**Authors**: Xin Shu, Chang Shu

## Project Overview
This project aims to predict the ratings giving by people from several features. This is a project for DSC80 at UCSD. The dataset used to investigate this topic can be find [here](https://drive.google.com/file/d/1kIbMz6jlhleiZ9_3QthmUnifoSds_2EI/view).

## Framing the Problem
In the culinary world, the balance between taste and health is a subject of much interest and debate. Meals are a critical factor in this balance, directly affecting an individual's health and well-being. In this project, we aim to predict the rating of a recipe based on various features, like reviews from people, average rating of a recipe, number of ratings for each recipe, users' average rating for recipes, and minutes to prepare a recipe. Therefore, we will build a regression model to fit our data to predict the rating for unseen recipes.

### **Response Variable**
We chose rating as the response variable, which has five different classes from star one to star five. Understanding the rating of a recipe helps people to regulate their meals for better health.

### **Evaluation Metrics**
To evaluate the model’s performance, we will use metrics such as RMSE. That’s because there are lots of outliers in our features, like lots of time to prepare recipes. So we choose RMSE because it is sensitive to outliers. It will give a higher error value, signaling that these points are not being predicted accurately.


## Baseline Model

### Model Description
In our baseline model, we intend to predict whether the rating is based on the average rating of the recipe and total minutes needed to prepare for a recipe. We will use `recipe_average_rating` and `log_minute` as features of our baseline Decision Tree Regressor model.

### Feature Transformations
For this baseline model, we did not have any categorical features, so we did not need to use OneHotEncoder() or any other categorical transformations. 

`recipe_average_rating`: This is a nominal feature. We just keep it as the raw integer value for simplicity. 

`minutes`: This is another nominal feature. We decided to perform a transformation for it because we found that some recipes need a huge amount of time to prepare. Thus, we have to transform minutes by log to make it more suitable for prediction.

<iframe src="assets/fig_minutes_rating.html" width=800 height=600 frameBorder=0></iframe>
<iframe src="assets/fig_log_min.html" width=800 height=600 frameBorder=0></iframe>

### Performance
Our model achieved a training RMSE of 0.7143 and a testing RMSE of 0.6130, which is reasonably a good performance. We believe it is good because the average rating of a recipe is indeed related to the rating itself. That’s because people are easily influenced by others' thoughts. If a recipe has already got a higher rating, people tend to give higher ratings based on that.


| Metric | Train RMSE | Test RMSE |
|--------|-------------|-------------|
| 'RMSE' | 0.7143449388166899 | 0.6130274904203801 |

---

## Final Model
After several trials, we decided to use DecisionTreeRegressor as our model. The reason is that Decision Trees can capture nonlinear relationships between features and the response variable `rating`. This is beneficial because the preparation time, average rating, and the final rating of a recipe is not linear based on the plots we draw. Here are the features we chose:

### **Description**
<!-- <iframe src="assets/fig_average_rating.html" width=800 height=600 frameBorder=0></iframe>
<iframe src="assets/fig_num_rating.html" width=800 height=600 frameBorder=0></iframe>
<iframe src="assets/fig_average_user_rating.html" width=800 height=600 frameBorder=0></iframe> -->

`recipe_average_rating`: For the average rating of a recipe, we want to examine if a recipe with higher rating would receive a higher rating from people. 

`recipe_num_ratings`: For the number of ratings for each recipe, we want to study whether a recipe with a higher number of ratings possibly tends to receive higher ratings from people. 

`user_average_rating`: For the user's average rating, we want to check if a person tends to give a higher rating just because he habitually gives high scores. 

`minutes`: For the minutes, we want to see if a higher rating recipe needs more time to prepare generally.

## Fairness Analysis

---