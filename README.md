## Welcome to engines soul search party

### Summary

Task was to predict remaining useful life of the engines. Given input was a series of sensor and configuration data for each engine. My minimum plan was to explore the input data, try to understand the structure of the data and fiqure out if there are any obvious patterns. Then implement a quick-and-dirty model that predicts at least something and is better than some 'dumb' baseline. If time allows, come back to data exploration and try to build a more robust and better model.
To speed up prototyping I focused on dataset1 (dataset_id='FD001'). Hoping that techniques developed for dataset1 are transferrable to other datasets. 

#### Prediction results on Dataset1:
* Baseline estimate with constant prediction errors on the test set: 'mae'=36 and 'rmse'=41.
* Best model prediction errors on the test set: 'mae'=18 and 'rmse'=23.

Best model was in fact quite simplistic and 'naive' approach using RandomForestClassifier as predictor. Main motivation for choosing this type of solution was that I wanted to implement rather quickly a robust model that works. Timeframe was critical for me, so that priority was to get something working and prepare [presentation](https://github.com/urmaspitsi/mt/blob/master/explorer.ipynb) with some useful visuals.
I am pretty sure the chosen model and its' implementation is far from optimal.

#### Model logic:
* loop through train set
* for each unit_id: 
  * fit a predictor with sensor data as X and remaing cylces as Y
* This results in a list of predictors: one for each unit_id.
* Run all predictors over the test set and choose 5 best.
* Final prediction is the average of best 5 predictions.

Feature set was top 7 highest variance sensors.
Underlying statistic for X was moving average with period length 5.

#### Comments
Because of time constraint I treated Test set as 'Validation set'. Ideally we should split training data into train and validation samples. Train our model on train set trying to minimize prediction error on validation set. Later use given Test set as the ultimate truth of how our model behaves. 



### Thoughts on data
* Sensor data exhibit pretty good convergence and underlying trendline, which suggest the data could be modelled very well.
* At the same time sensor data seems to exhibit quite good randomness on a local scale. Meaning it resembles a normal random walk. Eg terminal values of sensor data by unit_id follow normal distribution quite closely.
* Out of 21 sensors only some seem to be relevant. This provides good dimensionality reduction
* Different datasets have different 'relevant' sensors. It could be related to different configuration settings that I left out of focus at the moment. 

### Next steps
#### Data preprocessing and analytics
* use train-validation split and cross validation to properly train the model
* training generator: produces infinite stream of randomized training samples
* error analysis: understand model behaviour and which conditions produce largest errors etc.

#### Data exploration
* more data exploration and visuals
* correlation between sensors
* autocorrelation in each sensor series
* does configuration settings matter and how

#### Models
* stochastic methods: autoregressive models etc.
* apply deep learning: LSTM; needs proper preprocessing: data scaling and fitting
* rephrase problem into binary classication and model as confidence prediction eg: confidence that engine works atleast n cycles is >=99%; suppose relevant horizon is 10 cycles, we could ask are we at least 99% sure that engine works at least 10 more cycles. If answer is no, then engine goes to repair, otherwise ask the same question again after each succesful cycle.