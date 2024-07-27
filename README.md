# Pitch Prediction Project

## Overview

### Purpose of the project
This project will use machine learning methods to correctly predict the pitch type and location for hitters based on past and in-game information. By doing so, hitters will be well-prepared for the incoming pitches during at-bat and improve their hitting performance, which ultimately helps the team to win the ball game.

### Problem area
Baseball is hard. With pithces flying across the home plate in 0.45 seconds, hitters have only [50 milliseconds](https://entertainment.howstuffworks.com/physics-of-baseball3.htm) to think. As per Ted Williams, ["Baseball is the only field of endeavor where a man can succeed three times out of 10 and be considered a good performer."](https://www.washingtonpost.com/archive/lifestyle/2000/04/03/baseballs-lessons-for-life/782ab98d-e68b-4f3c-bda8-9c7bdd811c24/)If there's a way to help hitters find pattern between pitches, they can prepare in advance and comfortably swing at the pitches they like.

### Impact of the project
In 2019, Houston Astros were found cheating by stealing signals with prohibited devices in 2017 & 2018 season. They decoded the messsage and delivered the information to players at-bat [by banging on a trash can](https://en.wikipedia.org/wiki/Houston_Astros_sign_stealing_scandal#:~:text=The%20investigation%20found%20no%20evidence,picks%20in%202020%20and%202021.)to tell the batter what type of pitch was coming next. As punishment, The Astros were fined 5 millions and lost two first-round draft picks. What if, we can tell what the next pitch is without stealing signals?

### How to tackle the problem area(legally)
First, each pitches only have 2-3 types of the pitches that they are good at. We can examine the data at at-bat level, game level and player level to find:
* For pitchers equipped with certain types of pitches, what's the general pattern of pitching?
* In certain senerios, will they use a similar pitching strategy in terms of pitch type and location?
* Would it be possible to narrow down the habit/strategy to specific pitcher?


## Dataset

The dataset comes from [MLB Pitch Data 2015-2018](https://www.kaggle.com/datasets/pschale/mlb-pitch-data-20152018/data?select=atbats.csv). It records the every pitch information for MLB games from 2015 to 2019. Each row represents a pitch thrown in the game, and each column represents one kind of information. Some key attribute includes:
* px: x-location as pitch crosses the plate. X=0 means right down the middle.
* pz: z-location as pitch crosses the plate. Z=0 means the ground.
* zone: The specific strike zone that the pitch crosses the home plate. Zone 1-9 are in the strike zone. Zone 11-14 are outside the stike zone.
* pitch_type: Type of pitch. See data dictionary for list of pitch types.

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

## Feature Engineering Opportunity
Below list will be used as a guideline to develop columns that help with the project:
- [x] Add the current pitcher's pitch count through the game
- [x] Determine if a pitcher is starting pitcher or relief pitcher
- [x] Show the previous pitch type
- [ ] Show the previous pitch location
- [x] Include the previous pitch's result (type/code column from last row)
- [x] Include the previous at-bat result (type/code column before pitch_number goes back to 1)
- [ ] Narrow the dataframe to player-level. Would we have enough data for most of the player?
- [x] Visualize the strike zone map
- [x] There are rows with "placeholder" in zone column. We can use px and pz to find which strike zone it is.
- [x] Weather

## Data Cleaning

- To preserve the sequence of pitches, if one row is missing necessary value, the entire game data from this pitcher in the game will be excluded from the analysis. Around 30,000 rows are removed.
- For missing weather, cloudy is to assume weather has no influence on these games.
- Many columns are removed as they are either too high-level or not related to the project.

## Hypothesis to look into:
- [ ] Do pithcers pitch differently against lefty and righty?
- [ ] Do pitchers pitch differently with/without runner on bases?
- [ ] Do pitchers pitch differently when leading/trailing?
- [ ] If a hitter's hitting heatmap can be generated, will the pitcher attack the hitter's weak zone?
          Update: hitting's hitting performance would be considered as future information, thus not applicable.
- [ ] Without previous pitch information, how to find a pattern for the first pitch of each at-bat?


## Baseline Model

Currently recurrent neural network is used as the baseline model. The purpose is to capture the play-by-play characteristics of the data source with other features representing the in-game situation. The clean data will be split by each at-bat id, further split into sequenced data and loaded into the model for training. Both pitch type and pitch location will share the same features in the dataframe, use different layers and generate prediction.

### Baseline Model Performance

Horrible is not enough to describle the performance. Once tensor is fed into the model, it generates identical vectors in the tensor for each prediction. As a result, the model predict the same probability for each classes in prediction, thus always making predicting the same value. This would have no real-life application.

## Next Step

As the result of the baseline model is not good, there are some options left for Sprint 3:

### Fine-tuning the model

There's a chance that this model can be fixed. Some areas to consider include:
- Remove/bring back existing features
- Change some parameters
- Deal with class imbalance with approaches other than class weight

### Apply Softmax Regression

Softmax regression is a kind of the logistics regression that is able to handle multiple-class target variable.


