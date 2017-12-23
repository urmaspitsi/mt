## Welcome to engines soul search party

### Summary
Task was to predict remaining useful life for engines. Given input is series of sensor and configuration data for each engine.

To speed up prototyping I focused on dataset1 (dataset_id='FD001'). Hoping that techniques developed for dataset1 are transferrable to other datasets. 

Dataset1 Baseline estimate with constant prediction errors on test set:
'mae'=36 and 'rmse'=41.
Best model prediction errors test set:
'mae'=18 and 'rmse'=23.
Best model was in fact quite simplistic and 'naive' approach using RandomForestClassifier as predictor. 

Because of time constraint I treated Test set as 'Validation set'. Ideally we should split training data into train and validation samples. Train our model on train set trying to minimize prediction error on validation set. Later use given Test set as the ultimate truth of how our model behaves. 



### My journey
#### Thoughts on data



### Future thoughts