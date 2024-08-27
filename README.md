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

### Modeling

Below models have been tested with different train data processed by class imbalanced handling method and clustering.
- RNN Model
- Logistic Regression Model
- Xgboost
- Random Forest
- Ensemble learning (Logistic Regression Model + random forest)

Below is a quick summary in terms of accuracy:
| Accuracy      | Ball/Strike Prediction| Pitch Type Prediction |
| ------------- |:-------------:|  ----------------------------:|
|   RNN Model   | 0.54 | 0.43 |
| Logistic Regression| 0.54 | 0.42 |
| XGboost       | 0.60 | - |
| Random Forest | 0.54 | 0.45 |
| Ensemble Learning | 0.54 | - |

### Findings and Conclusions

There's a chance that this model can be fixed. Some areas to consider include:
- Remove/bring back existing features
- Change some parameters
- Deal with class imbalance with approaches other than class weight




