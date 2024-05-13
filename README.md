# Pitch Prediction Project

## Overview

### Purpose of the project
This project will use machine learning methods to correctly predict the pitch type and location for hitters based on past and in-game information. By doing so, hitters will be well-prepared for the incoming pitches during at-bat and improve their hitting performance, which ultimately helps the team to win the ball game.
### Problem area
Baseball is hard. With pithces flying across the home plate in 0.45 seconds, hitters have only [50 milliseconds](https://entertainment.howstuffworks.com/physics-of-baseball3.htm) to think. If there's a way to help hitters find pattern between pitches, they can prepare in advance and comfortably swing at the pitches they like.

## Dataset

The dataset comes from [MLB Pitch Data 2015-2018](https://www.kaggle.com/datasets/pschale/mlb-pitch-data-20152018/data?select=atbats.csv). It records the every pitch information for MLB games from 2015 to 2019. Each row represents a pitch thrown in the game, and each column represents one kind of information. Some key attribute includes:
* px: x-location as pitch crosses the plate. X=0 means right down the middle.
* pz: z-location as pitch crosses the plate. Z=0 means the ground.
* zone: The specific strike zone that the pitch crosses the home plate. Zone 1-9 are in the strike zone. Zone 11-14 are outside the stike zone.
* pitch_type: Type of pitch. See data dictionary for list of pitch types.
* code: Records the result of the pitch. See data dictionary for list of codes and their meaning
* type: Simplified code of the result of the pitch, S (strike) B (ball) or X (in play)

A data dictionary has been created in /dataset for the definition of the columns.

## 





