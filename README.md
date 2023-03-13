![banner.png](https://github.com/leo-schell/Phase-3-Project/blob/main/images/banner.png)

**Authors**: Leo Schell Villanueva, Christopher Swecker, and Paul Schulken

## Overview

This project is an analysis of customer churn based on anonymized data provided by Flatiron School's curated list of Phase 3 project datasets via [Kaggle.com](https://www.kaggle.com/datasets/becksddf/churn-in-telecoms-dataset).

The premise is to build a classifier to predict whether a customer will discontinue their prepaid mobile phone plan with telecom provider SyriaTel.

From here on out, we will be treating this repository as if it were a presentation from a data scientist team at SyriaTel.


## Background

Churn in the Telecommunications industry is at an all time low however SyriaTel is currently looking at a 14.5% attrition rate.

For reference, our competitors reported an average of 2.31% 2022 4th quarter prepaid churn rate.

![churn.png](https://github.com/leo-schell/Phase-3-Project/blob/main/images/churn.png)[width=50px]

Before analyzing the data, we performed surface level market research to understand what prepaid plans are being offered by our competitors. Below is a word cloud analysis based on the landing pages for top prepaid plans in the United States. 

![wordcloud.png|50%](https://github.com/leo-schell/Phase-3-Project/blob/main/images/wordcloud.png | width=75px)

Note a heavy emphasis on unlimited talk, text, and data plans. This will be important to consider as we evolve our offering to something more attractive to the average United States consumer.

Additionally, the geopolitical conflict in Syria and the attitudes of American clients could have a significant impact on churn for the foreseeable future. SyriaTel’s branding is heavily associated with the country. For this analysis, we have elected to take the most objective look at the data possible and have not factored in possible effects of the geopolitical conflict in Syria.


***

## Bottom Line

Bottom line, here are 2 suggestions that will have immediate impact on whether a customer will churn.

1. ***The number of times a customer engages with customer service has a direct impact on their likelihood of churn.*** For every one phone call, the likelihood increases by 2.6%.

2. To minimize churn, look into any potential issues that international plan members may have. ***For every instance of an international plan, a customer is 2x more likely to churn.***

***

## The Data
     
The data provided by SyriaTel can be found on [Kaggle.com](https://www.kaggle.com/datasets/becksddf/churn-in-telecoms-dataset).

It contains anonymized data for around 3300 customers. With customer churn as our focus, our analysis began with looking at the factors most correlated with churn:
- `international plan`
- `customer service calls`
- `daytime usage`

The limitations we faced included a lack of data around the nature of the customer service calls, an understanding of how the plans work, and no information about service or coverage. In addition, no date ranges or timeframe were included in the data.

Because of these limitations, we decided to drop columns `area code` and `phone number` from the data since we determined that they did not actually correlate to the states they were assigned.

### EDA

Here are a few highlights from our initial analysis:

***States***
We began by plotting the customer churn by state in an attempt to identify geographic trends. Texas, New Jersey, and Maryland churned the most but otherwise there were no significant trends.

![states.png](https://github.com/leo-schell/Phase-3-Project/blob/main/images/states.png | width=100px)

***Daytime Minutes***

Of the customers who did churn, two daytime usage groups stand out: those who speak on the phone between 2-3 hours and 4-5 hours. 

![churn_daytimemins.png](https://github.com/leo-schell/Phase-3-Project/blob/main/images/churn_daytimemins.png | width=100px)

***Evening Charges***

Of the customers who did churn, a significant amount of them spent around $15-$21 over the course of their account on evening calls.

![churn_eveningcharges.png](https://github.com/leo-schell/Phase-3-Project/blob/main/images/churn_eveningcharges.png | width=100px)


***


## The Model

Our full findings and  can be found in [FinalNotebook.ipynb](./FinalNotebook.ipynb).

Following our exploratory data analysis and identification of the most important features, we ran through several iterations of a model and were able to develop a final model using a balanced and scaled version of our dataset.

Throughout the process, we focused on minimizing the amount of false negatives produced - we didn’t want to predict a customer would stay when in fact, they churned.

From that final model, we gathered the top 5 factors and plotted them alongside the likelihood of churn for each unit increase - in other words, for each time a customer has to call customer service, they’re about 2.6 times more likely to churn assuming everything else remains equal. Below is a chart that shows the relationship between `churn` and the top 5 variables: `customer service calls`, `total day minutes`, `international plan`, `number vmail messages`, `total eve minutes`.

![finalmodel.png](https://github.com/leo-schell/Phase-3-Project/blob/main/images/finalmodel.png | width=100px)

We found the model to be 76% accurate overall and 72% accurate when just predicting customer churn.

Finally, based on the results of our final model we were able to retroactively assign probabilities of churn to each observation. We then ranked customer `propensity to churn` in a list of priorities from 1-10.


***


## Conclusions and Recommendations


On average, Priority 1 customers have the following attributes:
- `international plan`: Opted for an international plan
- `customer service calls`: Called customer service 4 times
- `number vmail messages`:  Do not use voicemail
- `total eve charge`: Spent $17 on evening calls over the course of their account
- `total day minutes`: Spent 3.5 hours on the phone during daytime hours

![priority1.png](https://github.com/leo-schell/Phase-3-Project/blob/main/images/priority1.png | width=100px)

Taking our analysis a step further, we can confidently say that by delivering out of this world customer service, we will immediately reduce the likelihood of churn.

## Next Steps

Our first step should be customer service analysis. We would like to parse chat logs of customer service calls to understand the specific nature of the customer service calls. 

Next, we'd like to take a look at the infrastructure of the top ten states where we see churn and examine if there are any gaps in coverage.

Finally, we can reasonably expect that politics will play a factor in a customer's propensity to churn. Some areas for further exploration: 
- Where are our international customers calling?
- How many of our American customers are Syrian and how can this brand best serve them?
- What is the public's perception of the SyriaTel Brand? Could it be time for a rebrand?


## Repository Structure


```
├── README.md                           <- The top-level README for reviewers of this project
├── FinalNotebook.ipynb                 <- Narrative documentation of analysis in Jupyter notebook
├── DataVisualization.ipynb             <- Easy Access to Data Visualization in Jupyter notebook
├── Presentation.pdf                    <- PDF version of project presentation
├── Notebooks                           <- Exploratory Notebooks
├── images                              <- Image Files
└── Data                                <- Data Source
```
