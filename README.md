# Prediction of property prices for the real estate listing resource.

**The goal of the project is to figure out what data works best to predict property price and how close are the predictions to the real values**

The workflow:
1. Data filtering
1. EDA
1. Feature Engineering
1. Developing several Linear Regression models and comparing their performance
1. Feature engineering and data filtering based on the models' performance
1. Analysing models
1. Drawing conclusions

## Data filtering
Data filtering was performed on column-by-column basis. Original data dictionary [here](http://jse.amstat.org/v19n3/decock/DataDocumentation.txt). The majority of columns were removed and others stayed unchanged or were transformed in some way - merged with another column, turned into binary from multiple categories, and other methods.
Initial data has been turned into shortlist of 18 columns after thorough cleaning and filtering process:

| feature | type | description |
| --- | --- | --- |
| **id** | *int64* | Id from original dataset |  
| **lot_area** | *int64* | Area of the parcel in square feet |
| **land_slope** | *int64* | If moderate or severe slope present |
| **central_air** | *int64* | If Central Air Conditioner present |
| **gr_liv_area** | *int64* | Overall square footage of all living areas |
| **totrms_abvgrd** | *int64* |  Total number of rooms suitable for living |
| **new_property** | *int64* | If the property is brand-new |
| **saleprice** | *int64* | Price of the property in US dollars |
| **paved** | *uint8* | If the road to property paved |
| **irregular** | *int64* |  If lot has an irregular configuration |
| **cul_de_sac** | *int64* | If property located at Cul de Sac |
| **positive_feature** | *int64* | If property is adjacent to positive feature, like park |
| **noisy** | *int64* | If there are any noisy objects close to the property, for example, railroad or arterial street |
| **years_old** | *int64* | Years since last renovation or construction |
| **non-living** | *float64* | Overall square footage of non-living area: basement, garage, porch, etc. |
| **baseline** | *float64* | Median neighborhood price + value of miscellaneous features if there are any |
| **condition** | *int64* | Summary of several scores including electrical, heating, overall condition and others |
| **floating_village** | *int64* | If property is in the floating village |

## EDA and Feature Engineering
To decide if the column was worthy to stay, I calculated number of unique categories, number of features per class, median price per class, boxplots with prices distribution per class if the attribute is categorical. I also made sure that all categorical data was transformed into binary or score-based values.
Also I've got rid of two outliers with large square footage and properties with Agronomical Zoning. Null values were dropped, because there was only one row with value missing. Columns with bigger amount of null values were removed from the dataset.
For numerical features I checked how the overall distribution looked like. Also EDA and Feature enginnering were approached several times base on the models perfomance. Mainly, multicollinearity was addressed after developing first model

## Modeling and analysis
To address the data science problem, I created 4 Multivariative Linear Regression models.
All data was scaled to appripriately to unify metrics like square footage and number of rooms.
First model utilizes all features from the short list. Second model has multicollinear features removed. Third model was created using Polynomial features and lasso regularization. Forth model uses the same dataset as model 2 but has ridge regularisation applied.
To evaluate models, I used R Squared score, LINEM assumptions validation and plots showing how predicted and real values overlap. 