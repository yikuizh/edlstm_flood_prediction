# Sample codes for paper 'Generalization of an Encoder-decoder LSTM model for flood prediction in ungauged catchments':
The repository includes two sample codes of the pipelline for using LSTM model to set up, train, and evaluate a regional and PUB flood prediction model.
1) Regional model: The Encoder-decoder LSTM-regional model will be trained on flood events at all 35 catchments, 50% as training, 25% as validation, 25% as test. Namely one model for prediction on all catchments.
2) PUB model: K-fold split strategy is introduced to achieve pseduo PUB prediction. The ED-LSTM-PUB models are trained on flood events at k-1 folds of catchments as gauged catchments, and test on catchments the rest fold as ungauged catchments. The process is repeated for k times until all catchments are test as ungauged catchments once.

# Steps to Recreate Results from Paper:
1) Prepare your dataset: Slice your continuous observation data into individual flood event. Better include runoff, precipitation, and temperature data.
2) Run scripts: First is to connects the Google Colab service for using GPU for training. Then assign the correct directories for your training data on Google drive. If local GPU is available, you need to adjust the codes. 
3) Collect results: After successfully run the script, it will output csv file that collect the median NSE score at each catchment.
4) N.B. The hyperparameters selection process has been skipped here.
