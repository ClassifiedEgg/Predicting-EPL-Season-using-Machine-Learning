# Predicting The 19/20 EPL Season Using Machine Learning
Football is if not the most, one of the most widely watched sports in the world, and with such viewership. The English Premier League, often abbreviated as EPL, is the biggest (by viewership) club football league in the world. here we try to predict the outcome of the currently ongoing league based on how teams performed the last season. 

## Data Gathering
The match stats for each season was gathered from http://www.football-data.co.uk/
The fixture list for the current season was taken from https://fixturedownload.com/

## Data Wrangling
The following stats were taken into consideration while making the model
*FTHG - Full-Time Home Goals
*FTAG - Full-Time Away Goals

We group the data by the HomeTeam, and AwayTeam and calculate the data we use in the model, as follows
*HAS - Home Average Scored (Total goals scored by a team at home / 19)
*HAC - Home Average Conceded (Total goals conceded by a team at home / 19)
*AAS - Away Average Scored (Total goals scored by a team away / 19)
*AAC - Away Average Conceded (Total goals conceded by a team away / 19)

We then scale the data to the range [0,1] to help us in calculating other parameters

For each fixture, we calcuate the following other paramerters
*HAtS - Home Attack Strength ( HAS [HomeTeam] * AAC [AwayTeam] )
*AAtS - Away Attack Strength ( AAS [AwayTeam] * HAC [HomeTeam] )

We do this for both the last season and current season as some teams participating in the current season were in the Championship (Division 2) last year, so we do not have their stats in the Premier League. We take the teams' performances till Matchday 15 to calculate the metrics we require

Note: We did consider taking 'Shots' as a parameter, but decided against it after it did not show any significant improvement in the results.

## Model 
We have used 5 different models to make our predictions, the models with the parameters are
*Logistic Regression (iterations = 10000)
*Random Forest Classifier
*Multinomial Naive Bayes
*XGB Classifier
*Super Vector Machine (iterations = 10000)

(XGB Classifier was implemented from the (XGBoost)[https://github.com/dmlc/xgboost] library, while the rest were from (sklearn)[https://scikit-learn.org/stable/])

Here is the accuracy of our models using various methods


| Method                   | Accuracy            |
| -------------------------|:-------------------:|
| Logistic Regression      | 0.6578947368421053  |
| Random Forest Classifier | 0.6052631578947368  |
| Multinomial Naive Bayes  | 0.618421052631579   |
| XGB Classifier           | 0.631578947368421   |
| Super Vector Machine     | 0.6447368421052632  |

## Possible Improvements
We could improve our model in a few ways, a few being: 
*Incorporating more match stats (like passes completed, corners taken, fouls committed) into our model 
*Incorporating betting odds
*Calculating the rating for each player in a team and using that

## Conclusion
Predicting football games is no easy task, and more so predicting a complete season correctly is near impossible as other match stats, they are a lot of variables that factor into a game, some not even measurable. This is just out attempt at doing so.

Project By 
Ashish Reddy, Dhiraj Lokesh
