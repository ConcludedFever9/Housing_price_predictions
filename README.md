Tanner Zuleeg
12/12/23
___ 
### Dataset and problem statement
___
In this project, we will be using the Ames Housing Data set, collected from 2006-2010 from Ames, Iowa. There is plentry of information here about housing features along with saleprice. The question we will be trying to answer is, from the perspective of a homeowner in Ames, Iowa, which features of my home hold the most value potential as measured by sale price? We will use linear regression to predict sale price in terms of a collection of relevant features which a homeowner **has control over**.

### Familiarizing ourself with data by making a predictive model
To familiarize ourselves with the data and relationships between features, we make a predcitive model for sale price. This model uses many features which cannot be cnahnged by a homeowner. We will answer our problems statement more explicitly in the inferential model after. In some columns with categorical/ordinal data, 'NA' was entered to represent the absence of the item whose quality was being measured. These should not be seen as null but as another category in itself. This constituted all the cleaning that was necessary.

Next, we ran the baseline linear regression model and reported on its error. This allowed us to assess if our model performed better than simply guessing the average for every house. We observed that the testing RMSE for the base model is 79356.03.

Our subsequent goal was to create a general predictive model, sacrificing inference and intelligibility. The first step was holistically choosing a feature set and preparing them for the model by dummifying the columns that needed it. All columns in our feature set were dummied except 'Year Remod/Add' and 'Overall Cond'. These two were not dummied because the newer a house (int), the more it would probably sell for. The same logic applied to 'Overall Cond', which is ordinal. Next, we fitted and tested this model, obtaining a training score of 0.79 and a testing score of 0.71. This model performance is a decent start, and the bias-variance tradeoff seemed balanced, as indicated by the similar scores. We obtained a testing RMSE of 42063.40.

### LASSO and Ridge analysis for predictive model
We regularized to run some tests. After running Ridge and fitting the optimal alpha of 8.1, we got a slightly increased model score of 0.72. Next, we ran a LASSO test which helped us discover certain predictors that should be dropped. After doing this and remaking a model with this pruned feature set, we obtained a training score of 0.76 and a testing score of 0.73, indicating slightly higher model performance and a good bias-variance tradeoff.

### Adding polynomial features
After this, we ambitiously added a poly fit for interaction terms, but after checking model performance, we only achieved a training score of about 0.82 with a test score of 0. Running LASSO here would not be worth it, so we ended with our predictive model defined in the last iteration.

### Inferential model and addressing problem statement
Now, familiar with our data and models, we started from scratch to make a model from the viewpoint of someone interested in improving specific features of their own home to maximize its sale price. This became our primary research question. We selected many features from the dataframe that the person would have control over: kitchen quality, garage quality, basement quality, etc., while staying away from features someone cannot control: terrain their house is on, neighborhood, PID, etc.

Cleaning the data here took a while. We dummified the columns that needed to be (Exterior materials, Roof materials, etc.) and used a mapping function to assign a numerical value (from 0-5) to the ordinal data. Once we did this, we fitted a model, and its performance was pretty good, obtaining a training score of 0.79 and a testing score of 0.82, with a testing RMSE of 32848.47.

We checked model assumptions first by creating two heatmaps. The first heatmap was of the features, which showed low correlation between all features overall with just two exceptions: Garage_Cond/Garage_Qual and Roof_Matl_Tar&Grv/Roof_Matl_CompShg. Ideally, we would rerun the model after dropping one from each correlation, but given that we have a large feature space, this should be fine. The residual plot was spot on.

In conclusion, looking at the coefficients on the predictors, we see that the most valuable features are the membrane roof material, hooking up to water and sewer and installing cinderblock exterior.

### Directions and Resources
Sign up for an account on [Kaggle](https://www.kaggle.com/)
Click the link [DSI-1113 Ames Regression Challenge](https://www.kaggle.com/t/177bc8cfe89b48d59ee4360ed9b56680) to **join** the competition (otherwise you will not be able to make submissions!)
Review the material on the [DSI-1113 Ames Regression Challenge](https://www.kaggle.com/competitions/1113-ames-competition)
Review the [data description](http://jse.amstat.org/v19n3/decock/DataDocumentation.txt).