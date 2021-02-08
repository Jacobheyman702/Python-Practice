# Kings County Housing Bake-off

 ## Overview
In this project we where tasked to create the best predictive model for Kings County housing prices, and valadate our model with holdout data. Using the Kings County house price database, I preformed an exploritory data analysis, identifying the nature and oddities of the data set. In my analysis I noticed issues with the date, outliers in the number of bedrooms, and several continuous predictors with catagorical aspects. To acheive the best model I engeniered several new predictors in order to best predict prices on a holdout set of data. Before running any model I checked for multicolinierity leading me to drop several paired coefficiant predictors. In the models I ran, I found the best results in a model that had the date converted to months, the years renovated converted into a catagory of not renovated and renovated after 2000 and catagorical data such as, view, waterfront, condition, year built, bedrooms, floors and zipcode where all converted into dummy catagories. My findal model had an R-squared value of .804 accounting for 80% of the varience of the model, and an RMSE value of 161975.38. The model was exported using Pickle and used to predict on the holdout data. While I do not think this is the perfect model, I believe it is on the right track to creating a good predictibe model

## Bussiness Problem
Creating a predictive model, while being data science, is not an exact science.  Many different factors need to be accounted for, such as coliniarity, outliers and the curse of dimensionality.  In order to procude the best predictive model for machine learning a data scientist must preform an indepth exploritory data analysis in order to produce the best predictive features.  While analyzing the Kings County data I considered these following questions about the data in order to stratagize for feature engineering:
**research Questions**
1. Does the specific month a house is sold effect the price?
2. Do houses renovated after the year 2000 have a higher price then other houses
3. Does roomsize combined with the lot size result in a higher house price.    


## Data
To answer our business question above, I analyzed the Kings County Housing Price data set.  The Dataframe included the following columns:
* **id** - unique ID for a house
* **date** - Date day house was sold
* **price** - Price is prediction target
* **bedrooms** - Number of bedrooms
* **bathrooms** - Number of bathrooms
* **sqft_living** - square footage of the home
* **sqft_lot** - square footage of the lot
* **floors** - Total floors (levels) in house
* **waterfront** - Whether house has a view to a waterfront
* **view** - Number of times house has been viewed
* **condition** - How good the condition is (overall)
* **grade** - overall grade given to the housing unit, based on King County grading system
* **sqft_above** - square footage of house (apart from basement)
* **sqft_basement** - square footage of the basement
* **yr_built** - Year when house was built
* **yr_renovated** - Year when house was renovated
* **zipcode** - zip code in which house is located
* **lat** - Latitude coordinate
* **long** - Longitude coordinate
* **sqft_living15** - The square footage of interior housing living space for the nearest 15 neighbors
* **sqft_lot15** - The square footage of the land lots of the nearest 15 neighbors

## Methods
In this project, I preformed an Exploritory data analysis, creating new features for the predictive models.  To answer the business questions I posed, I preformed statistical analysis of several existing and newley engineered features, in order to observe if they had a significant effect on the target variable.  I also preformed several visualizations to help identify multicolinearity.  The new features I created where date by month, renovated after 2000 and lot square footage multiplied by the number of house bedrooms.  They goal of the new features was to account for as much residual variance as possible in the liniear regression model.  

## Results
My Exploritory Data Analysis revealed several potential outliers and multicolinier variables.

![waterfrontKDE](./Images/waterfront.png)
![heatmapCorr](./Images/heatmap.png)

The outliers and multicolinier variables where removed in order to proceed with the feature generation and modeling

The first model featured a new date by month catagory, dummy variables for the remaining catagorical data and scalled continous variables.  The model had an OLS R-squared value of .806.  An RMSE evaluation resulted in a error value of 2.959139033524656e+16 for the test set.  

The second model incorperated the predictors from model one with a change to the yr_renovated column.  The variable was changed into a catagory of renovated_after_2000 with a value of one and all other values being 0.  A dummy column was added for the new predictor.  Model 2 had an OLS R-squared value of .804 and an RMSE on the test set of 161975.39.

![risidual](./Images/risidual_plot.png)

The third model built off the first 2 and featured a new predictor of sqrt_lot X bedrooms.  Model 3 had an OLS R-squared value of .800 and an RMSE of 162182.48

## Conclusion
The first model had an extremely high RMSE value on the test set.  I think this is most likely do to not accounting for the extreme split nature of the yr_renovated column, with the majority of the values being either 0 or 1970 and up.  When I created a new feature to compensate for this column my error normalized a bit.  In model 3 I attembed to imporve on Model 2 by using generating a polynomial feature.  This new feature, however did now imporve the model.  Based on the three models from my modeling process I chose to use model 2 as my predictor model.  I serialized model 2 with pickle and imported it into a new file, where I used the model to predict on the holdout set.  

## For More Information
please review my full [bake off modeling proccess](./Bakeoff_modelling_process/ipynb) and my [hold out prediction](./Predict_holdout/ipynb)
For addition questions, contact Jacob Heyman (jacobheyman702@gmail.com)

## Repository Structure

```
├── README.md                           <- The top-level README for reviewers of this project
├── images.                             <- images of visualizations for ReadME
├── bakeoff_modeling_process.py         <- EOD and Modeling process for predictive model
├── predict_holdout.py                  <- Final model prediction on the holdout dataset
├── scaler.pickle.                      <- pickle file of model scaler
├── model.pickle.                       <- pickle file of final model
├── housing_preds_Jacob_Heyman.csv      <- Csv of predictions on holdout set
├── kc_house_data_train.csv             <- train data set for modeling process
└── kc_house_data_test_features.csv.    <- holdout data set 
