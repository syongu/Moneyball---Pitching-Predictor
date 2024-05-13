# Pitch Prediction Project

## Overview

### Purpose of the project
This project will use machine learning methods to correctly predict the pitch type and location for hitters based on past and in-game information. By doing so, hitters will be well-prepared for the incoming pitches during at-bat and improve their hitting performance, which ultimately helps the team to win the ball game.

### Problem area
Baseball is hard. With pithces flying across the home plate in 0.45 seconds, hitters have only [50 milliseconds](https://entertainment.howstuffworks.com/physics-of-baseball3.htm) to think. As per Ted Williams, ["Baseball is the only field of endeavor where a man can succeed three times out of 10 and be considered a good performer."](https://www.washingtonpost.com/archive/lifestyle/2000/04/03/baseballs-lessons-for-life/782ab98d-e68b-4f3c-bda8-9c7bdd811c24/)If there's a way to help hitters find pattern between pitches, they can prepare in advance and comfortably swing at the pitches they like.

### Impact of the project
In 2019, Houston Astros were found cheating by stealing signals with prohibited devices in 2017 & 2018 season. They decoded the messsage and delivered the information to players at-bat [by banging on a trash can](https://en.wikipedia.org/wiki/Houston_Astros_sign_stealing_scandal#:~:text=The%20investigation%20found%20no%20evidence,picks%20in%202020%20and%202021.)to tell the batter what type of pitch was coming next. As punishment, The Astros were find 5 millions and lost two first-round draft picks. What if, we can tell what the next pitch is without stealing signals?

### How to tackle the problem area(legally)
First, each pitches only have 2-3 types of the pitches that they are good at. We can examine the data at at-bat level, game level and player level to find:
* For pitchers equipped with certain types of pitches, what's the general pattern of throw?
* In certain senerios, will they use a similar pitching strategy?
* Would it be possible to narrow down the habit/strategy to specific pitcher?


## Dataset

The dataset comes from [MLB Pitch Data 2015-2018](https://www.kaggle.com/datasets/pschale/mlb-pitch-data-20152018/data?select=atbats.csv). It records the every pitch information for MLB games from 2015 to 2019. Each row represents a pitch thrown in the game, and each column represents one kind of information. Some key attribute includes:
* px: x-location as pitch crosses the plate. X=0 means right down the middle.
* pz: z-location as pitch crosses the plate. Z=0 means the ground.
* zone: The specific strike zone that the pitch crosses the home plate. Zone 1-9 are in the strike zone. Zone 11-14 are outside the stike zone.
* pitch_type: Type of pitch. See data dictionary for list of pitch types.
* code: Records the result of the pitch. See data dictionary for list of codes and their meaning
* type: Simplified code of the result of the pitch, S (strike) B (ball) or X (in play)

A data dictionary has been created in /dataset for the definition of the columns.





