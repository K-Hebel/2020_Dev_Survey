### This repository contains an analysis of the 2020 StackOverflow Developer Survey which was circulated in February 2020.   

##### _This analysis includes a Jupyter Notebook which contains detailed information regarding datasets, links to original datasets and commentary on code used in this analysis._

## **Motivation:**
The goal of this project is to remind all of us that measures of 'success' are relative, particularly when the primary measures are absolute numerical values that differ significantly between regions of the world.

This analysis is part of an iterative process and will continue to see improvements.  We appreciate your commentary, feedback and suggestions.  Thank you for your contributions.

# Understanding the Business and the Data

### Taking a peep at the data, there are a number of questions we have that revolve around the topic of compensation.  Note- because of currently fluctuations all compensation is US Dollar denominated and based on the StackOverflow dataset 'ConvertedComp' column

1) What are average developer earnings based on country and how does this compare with the country's 2019 per capita GDP?

2) At what age did most developers begin coding?

3) What was the gender breakdown for all surveyors and do disparities in income still exist for people in the US?

4) What do developers do when they get 'stuck' on a problem and does it change with compensation?

5) What were the top 10 professions based on average compensation of each profession?

6) What features in the dataset are strong predictors of high compensation levels?

### Given compensation is key to all questions, let's prepare the data set by dropping rows  where 'ConvertedComp' is  NaN

## **Files Used :**
 The files used in this analysis were:
 1) The 2020 StackOverflow dataset [HERE](https://insights.stackoverflow.com/survey/?_ga=2.206748819.1859624778.1609725307-1677851539.1609725307 "StackOverFlow 2020 Survey") - survey_results_public.csv
 2) The StackOverflow schema - survey_results_schema.csv
 3) IMF 2019 per capita gdp for select countries -
 imf_data.csv
 * From the IMF Datamapper [HERE](https://www.imf.org/external/datamapper/NGDPDPC@WEO/AZE "IMF GDP Per Capita current prices US Dollars")  and based on the information provided by the  World Economic Outlook for October 2020 for GDP
 4) The jupyter notebook for this analysis - 2020 StackOverflow Survey - Project 1.ipynb

# **Understanding the Data**
**To specifically respond to each question presented above, we used the following data:**
1) StackOverflow dataset - column: 'Country' and
 imf_data.csv  country per capita GDP, for the year 2019.  
 * We looked at mean, median values per country as well as the ratio of the a country's mean to its per capita gdp.

2) StackOverflow dataset - column: 'Age1stCode'
 * We measured the frequency of reported ages

3) StackOverflow dataset - columns: 'Gender' and 'DevType' and 'Country' grouped by 'ConvertedComp'

4) StackOverflow dataset - columns: 'NEWStuck' and 'YearsCodePro' grouped by 'ConvertedComp'

5) StackOverflow dataset -  column: 'DevType' grouped by 'ConvertedComp'

6) StackOverflow dataset - 'Comp_gdp' as target and features.
 * features = ['Hobbyist', 'Age1stCode','Age', 'Country','DevType','Gender', 'JobSat',
            'YearsCodePro','OrgSize', 'ConvertedComp']

# **Preparing the Data**
1) All data was gathered based on the files listed in the heading 'Files Used'

2) From the StackOverFlow dataset - All rows without a value for 'ConvertedComp' in the StackOverFlow dataset were dropped as 'ConvertedComp' is the basis for this analysis.

3) From the StackOverFlow dataset - 'Countries' with less than 100 respondents were dropped. When grouped by country, a relatively small number of respondents is hardly representative, thus we set a minimum benchmark to include only those responses (rows) from 'Countries' with 100 or more survey respondents (sorry Burkina Faso).

4) From the StackOverFlow dataset - 'Age1stCode' non-numerical values and outliers were dropped.

5) From the StackOverFlow dataset - 'NEWStuck' responses included multiple responses within a single cell/row.  We therefore split responses into single answers to obtain an accurate count of answer values.

6) From the StackOverFlow dataset - 'YearsCodePro' non-numerical values were dropped.

7) From the StackOverFlow dataset - 'DevType' with less than 50 respondents were dropped.

8) For modeling purposed, features in the model with NaN values were imputed based on 'most_frequent' value for categorical data and 'mean' for numerical data.

# **Data Analysis / Validation**
1) The first 5 questions in  this project are answered based on statistical analysis our in this analysis.

2) Question 6 required the use of Modeling:
* Considering a test_train_split, X was set to   features = ['Hobbyist', 'Age1stCode','Age', 'Country','DevType','Gender', 'JobSat',
           'YearsCodePro','OrgSize', 'ConvertedComp']

* The target data y was set to the ratio of 'ConvertedComp' to country per capita gdp

* Modeling was based on Random Forest Regression with n_estimators=1000 and random_state = 9 . One Hot Encoding was used to manage categorical data.

* X_test (20% of the X dataset) was used to validate the model

* The r_squared score on the model was 0.9424618175355847

# **Results & Visualizations :**
Summary results and visualizations of the analysis may be found at https://khebel.medium.com/.  The main premise of the analysis is to view desirable compensation as one weighted to the national per capita gdp of one's country location rather than the absolute value of that compensation.  Detailed notes on the analysis and visualizations are contained in the jupyter notebook.


# **Acknowledgements :**
This analysis relies on the StackOverflow dataset and IMF datasets.    The author also relied heavily on panda documentation for the coding process.  In addition, there was additional instructional benefit taken from courses on Udacity, Kaggle and StackOverFlow.   Markdown and dataframe formatting guidance were taken from https://www.markdownguide.org/basic-syntax/ and https://mkaz.blog/code/python-string-format-cookbook/, respectively.  
