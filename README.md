## Welcome to engines soul search party

### Summary
Task was to predict remaining useful life for engines. Given input is a series of sensor and configuration data for each engine. My minimum plan was to explore the input data, try to understand the structure of the data and fiqure out if there are any obvious patterns. Then implement a quick-and-dirty model that predicts at least something and is better than some 'dumb' baseline. If time allows, come back to data exploration and try to build a more robust and better model.

To speed up prototyping I focused on dataset1 (dataset_id='FD001'). Hoping that techniques developed for dataset1 are transferrable to other datasets. 

Dataset1 Baseline estimate with constant prediction errors on test set:
'mae'=36 and 'rmse'=41.

Best model prediction errors test set:
'mae'=18 and 'rmse'=23.

Best model was in fact quite simplistic and 'naive' approach using RandomForestClassifier as predictor. I am pretty sure it is far from optimal.

Model logic is as follows:
loop through train set
. . for each unit_id
. . . . fit a predictor with senor data as X and remaing cylces as Y

Resulting in a list of predictors: one for each unit_id. Run all predictors over the test set and choose 5 best. Final prediction is the average of best 5 predictions.

Because of time constraint I treated Test set as 'Validation set'. Ideally we should split training data into train and validation samples. Train our model on train set trying to minimize prediction error on validation set. Later use given Test set as the ultimate truth of how our model behaves. 



### My journey
#### Thoughts on data



### Future thoughts