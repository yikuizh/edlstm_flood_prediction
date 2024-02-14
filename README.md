# Sample codes for JoH paper 'Generalization of an Encoder-decoder LSTM model for flood prediction in ungauged catchments':
The repository includes sample codes of the workflow for using Encoder-decoder LSTM model to set up, train, and evaluate a regional and PUB flood prediction model.
1) Regional model: The Encoder-decoder LSTM-regional model will be trained on flood events at all 35 catchments, 50% as training set, 25% as validation set, 25% as test set. Namely one model for prediction on all catchments.
2) PUB model: K-fold split strategy is introduced to achieve pseudo PUB prediction. The ED-LSTM-PUB models are trained on flood events at k-1 folds of catchments as gauged catchments, and test on catchments the rest fold as ungauged catchments. The process is repeated k times until all catchments are tested as ungauged catchments once.
3) How to use the code:

# How to run:
1) Prepare your dataset: Slice your continuous observation data into individual flood events. Better include runoff, precipitation, and temperature data. --  where the data stored
## dependency
2) Run scripts: The first is to connect the Google Colab service for using GPU for training. Then assign the correct directories for your training data on Google Drive. If local GPU is available, you need to adjust the codes for your local use. 
3) Collect results: After successfully running the script, it will output csv files that collect the median NSE score at each catchment.
4) N.B. The hyperparameters selection process has been skipped here.
5) N.B. If you have any questions about the dataset, please contact the author for further information.

### Citation for the paper: https://doi.org/10.1016/j.jhydrol.2022.128577
