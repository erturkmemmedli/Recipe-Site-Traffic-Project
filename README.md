# Recipe-Site-Traffic-Project

The objectives in our project are predicting which recipes will lead to high traffic and predicting high traffic recipes 80% of the time.

For that purpose, we need to study the given data first. We found that there are 947 observations with 8 columns. Among these columns, one is just unique id of recipes, 4 of them are numerical valriables, which inlude calories and 3 nutritional components, other 2 of them are categorical variables, which are category and servings columns, and finally the last one is our target variable, high traffic. We examined the data and handled preprocessing and cleaning steps such as duplicate removal, missing value replacement or deletion, type conversions, etc. In the end, we had 895 observations, which were clean and ready to analysis.

![Picture1](https://github.com/erturkmemmedli/Recipe-Site-Traffic-Project/assets/49902768/90563eb5-6cc9-45bb-bbff-9620890111dd)

We started our exploratory data anaylis by pairplot to show relationship between numerical variables. As shown by scatterplots between variables, we see that there is no significant relationship between them, which is what we desire. Because if there is correlation, it would result in bias in model development.

![Picture2](https://github.com/erturkmemmedli/Recipe-Site-Traffic-Project/assets/49902768/87537e01-73a2-4951-81bb-20322ef5811a)

Then, we used histogram to find how calories and nutritional components are distributed in the recipes. As a result, as you can see in the screen, all of them are right-skewed, which means that low values are mostly preferred in recipes regarding both calories and the amount of nutritional components.

![Picture3](https://github.com/erturkmemmedli/Recipe-Site-Traffic-Project/assets/49902768/81e81e46-015b-4e9d-9f24-31cd12dd1299)

Here, you see the same analysis by different perspective, I mean, with boxplot. It clearly shows outliers and how observations are concentrated in left side, I mean in low values, which once again proves the right-skewness.
These findings suggest that we must prefer median over mean as statistical measurement metrics.

![Picture4](https://github.com/erturkmemmedli/Recipe-Site-Traffic-Project/assets/49902768/1a6b8acb-ef5b-4760-bf11-2506b2142f2e)

So, in this part, we examine medians of numerical variables by categories. We see that medians for calories and nutritional components are not symmetrical as expected, based on the type of food and beverages.

![Picture5](https://github.com/erturkmemmedli/Recipe-Site-Traffic-Project/assets/49902768/188aa0c2-03ce-40ea-9752-04cc70b6734f)

Then, we examined relationship between categorical variables and high traffic. As you see in the left figure, although ratio of high traffic recipes to low traffic recipes are generally close to each other, we see that when serving count is high, I mean at its maximum value 6, high traffic is achieved more. Also, as you see in the right figure, specific categories results in higher traffic. Top 3 are "Vegetable", Potato", and "Pork". And the worst category in this regard is "Beverages".

After finishing analysis, we developed the appropriate model for achieving objectives. Since we are dealing with binary target variable, our problem is on the scope of binary classification algorithms of supervised machine learning. To achieve the goal, we can develop different models such as Linear Regression, Decision Tree, Random Forest, Support Vector Machines and so on. I have chosen Linear Regression as baseline model and the others as comparison models.

![Picture6](https://github.com/erturkmemmedli/Recipe-Site-Traffic-Project/assets/49902768/d6b066e1-f82e-49d5-995f-5220706cc222)

But before fitting models, we need to make transformation on our numerical variables since they are right-skewed. I have tried different techniques such as removing outliers, capping outliers, winsorization, logarithmic transformation, square root transformation, box-cox and yeo-johnson transformations. Among them, the best choice was yeo-johnson so that you see the distribution for numeircal variables in the screen.

![Picture7](https://github.com/erturkmemmedli/Recipe-Site-Traffic-Project/assets/49902768/cac1deed-cc0c-45f9-b703-4cab0e5f7045)

Afterward, I have performed one-hot encoding for handling categorical variables. It was done only on category column because although servings column is categorial in nature, it is numerical, and numeric values there are reasonable since they refer to serving count.

![Picture8](https://github.com/erturkmemmedli/Recipe-Site-Traffic-Project/assets/49902768/2e463ce6-016b-49e0-af46-5c5b69e86e4e)

Afterward, we split data into train and test sets, fit the model and made predictions. As can be seen from Logistic Regression model evaluation, test and train results are close to each other. The fact that test results are a little bit higher than train results means that we have not enough data to develop a model on. Furthermore, there is no overfitting. Since the goal is to correctly predict high traffic recipes 80% of the time, we need to check the precision metrics, which is 80.87% as desired. Since Decision Tree and Random Forest models are too strong models, they memorized the training data so that the model is overfitting; thus, they are not suitable for our dataset. In the Support Vector Machines model, we see underfitting because the model could not learn from trained data since the number of observations is low. We could also use Gradient Boosting, LGBM, xGboost models but since they are also powerful models, they would also result in overfitting due to low amount of data.

From the business perspective, predicting high as low is worse error than predicting low as high. So, our priority is the model precision because the former can result in a great loss for the business. We defined our own KPI by True Positive / False Positive division in the confusion matrix and named it as "High Traffic Conversion Rate” and determined that it should always be greater than 4.0 depending on train and test results of our baseline model. We compared KPI results for models we developed. This KPI should be applied to our business model.

From exploratory analysis, we found that some categories result in generally high or low traffic. If a recipe belongs to "Vegetable", Potato", or "Pork" categories, we can summarize that it will result in high traffic So, we can recommend that it should always be offered in the website regardless of the model result. If a recipe belongs to "Beverages" category, we can conclude that it will result in low traffic. So, we can recommend that it should never be offered.

In conclusion, after preprocessing, cleaning, and analysis, we have developed several models to achieve our goal. Among the models developed, the Logistic Regression model has performed the best. This indicates that the Logistic Regression model is the most suitable model for predicting whether a recipe will lead to high traffic and correctly predict high traffic recipes 80% of the time. We also determined a KPI for our business model so that the KPI property must hold all the time for creditability of our data analysis and model development. We also noticed there are some categories that bring high traffic to the website, and some vice versa, so, we recommended to offer some recipes and not to offer some recipes regarding this knowledge.
