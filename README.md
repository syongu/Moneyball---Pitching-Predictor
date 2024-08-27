# Pitch Prediction Project- MoneyBall

## Overview

### Purpose of the project
This project will use machine learning methods to predict the pitch type and strike/ball based on past and in-game information. By doing so, hitters will be well-prepared for the incoming pitches during at-bat and improve their hitting performance, which ultimately helps the team to win the ball game. 

### Problem area
Baseball is hard. With pithces flying across the home plate in 0.45 seconds, hitters have only [50 milliseconds](https://entertainment.howstuffworks.com/physics-of-baseball3.htm) to think. As per Ted Williams, ["Baseball is the only field of endeavor where a man can succeed three times out of 10 and be considered a good performer."](https://www.washingtonpost.com/archive/lifestyle/2000/04/03/baseballs-lessons-for-life/782ab98d-e68b-4f3c-bda8-9c7bdd811c24/)If there's a way to help hitters find pattern between pitches, they can prepare in advance and comfortably swing at the pitches they like.

### Impact of the project
In 2019, Houston Astros were found cheating by stealing signals with prohibited devices in 2017 & 2018 season. They decoded the messsage and delivered the information to players at-bat [by banging on a trash can](https://en.wikipedia.org/wiki/Houston_Astros_sign_stealing_scandal#:~:text=The%20investigation%20found%20no%20evidence,picks%20in%202020%20and%202021.)to tell the batter what type of pitch was coming next. As punishment, The Astros were fined **5 millions** and lost two first-round draft picks. What if, we can tell what the next pitch is without stealing signals?

## Dataset

The dataset comes from [MLB Pitch Data 2015-2018](https://www.kaggle.com/datasets/pschale/mlb-pitch-data-20152018/data?select=atbats.csv). It records the every pitch information for MLB games from 2015 to 2019. Each row represents a pitch thrown in the game, and each column represents one kind of information. Some key attribute includes:
* zone: The specific strike zone that the pitch crosses the home plate. Zone 1-9 are in the strike zone as a strike. Zone 11-14 are outside the stike zone as a ball.
* pitch_type: Type of pitch. See data dictionary for list of pitch types. We're simplifing it to four classes:
  * Four Seam Fastball
  * Other Fastball
  * Breaking Ball
  * Off-Speed

Some important attributes to use as independent variables are:
* code: Records the result of the pitch. See data dictionary for list of codes and their meaning
* type: Simplified code of the result of the pitch, S (strike) B (ball) or X (in play)
* outs: Number of outs before pitch is thrown
* pitch_number: number of the pitchs in the current at-bat
* on_1b/2b/3b: if there's runner on 1st,2nd or 3rd bases.
* stand: which side batter hits on
* p_throws: which hand pitcher thrown with
* b_score and p_score: score for the batter's/pitcher's team
* b_count: ball in the current count
* s_count: strike in the current count

A data dictionary has been created in dataset folder for the definition of the columns.


## Project WorkFlow:

### Data Cleaning

- To preserve the sequence of pitches, The entire game data from this pitcher in a game will be removed if we are missing data. Around 30,000 rows are removed.
- Many columns are removed as they are either not related or the result.
- There are rows with "placeholder" in zone column. We used px and pz to find which strike zone it is.

### Feature Engineering Opportunity
Below list will be used as a guideline to develop columns that help with the project:
- [x] Add the current pitcher's pitch count through the game
- [x] Determine if a pitcher is starting pitcher or relief pitcher
- [x] Show the previous pitch type
- [x] Show the previous pitch location
- [x] Include the previous pitch's result (type column in simplified version from last row)
- [x] Include the previous at-bat result (type/code column before pitch_number goes back to 1)
- [x] Visualize the strike zone map
- [x] Weather

### Exploratory Data Analysis (EDA)

- Some exploration and analysis on classic game scenarios has been conducted to understand the distribution and relationship.
- After logistic regression on ball/strike is conducted, coefficients are looked at to determine effective factors.

### Modeling

Below models have been tested with different train data processed by class imbalanced handling method and clustering.
- RNN Model
- Logistic Regression Model
- Xgboost
- Random Forest
- Ensemble learning (Logistic Regression Model + random forest)

Below is a quick summary in terms of accuracy:
| Accuracy      | Ball/Strike Prediction| Pitch Type Prediction |
| ------------- |:-------------:|:-------------:|
|   RNN Model   | 0.54 | 0.43 |
| Logistic Regression| 0.54 | 0.42 |
| XGboost       | 0.60 | - |
| Random Forest | 0.54 | 0.45 |
| Ensemble Learning | 0.54 | - |

Considering the accuracy, class imbalance and ease to use, our first choice for general prediction would be ensemble learning for strike/zone and logistic regression for pitch type.

### Cluster

To better capture the pitchers' "habit", K-mean clustering is conducted for all 1511 pitchers. They are divided into 3 groups and will have models with different parameters for prediction.
| Accuracy      |Number of Pitcher| Ball/Strike Model| Accuracy | Pitch Type Model| Accuracy |
| ------------- |:-------------:|:-------------:|:-------------:|:-------------:|:-------------:|
|   Cluster 1   |1007| Ensemble Learning | 0.55 |Logistic Regression| 0.43|
|   Cluster 2   |383| Ensemble learning | 0.53 |Random Forest| 0.40|
|   Cluster 3   |121|Ensemble learning | 0.54 |Logistic Regression|0.43|

## Findings 

It appears that 55% is the accuracy ceiling for predicting ball/strike and 45% for pitch type. Given that batter has at least three chance to make a hit, the chance of both models making correct prediction at least once in three attempts is 57.5%.

- RNN model appears to be the model with most potential. However, it can only make predictions after two pitches with the constrain of sequence length.
- Different models give  a different focus on precision and recall. Some sacrifices the minority class prediction while some acrifices the majority class prediction.

## Limits
- More features are needed. This project only looked at pitcher's side of story. Each batter has their "sweet zone", "sweet pitch" that they can hit great. As baseball is a game, we need to study both sides. 
- Data quality can be improved. As mentioned, the strike/ball total looks different from real-life. Users also can't figure out how correctly the pitch type is recorded.
- Advanced Models: Potentially ensemble learning combining different models will yield a better result
- Evaluation: The best models were chosen with a balanced focus on all classes. If players want to "attack" a specific type of pitch or area, models should be fine-tuned.
- More data/features on pitcher is needed. It includes advanced pitching stats for better clustering result.


