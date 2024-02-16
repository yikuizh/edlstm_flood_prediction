# Sample codes for JoH paper 'Generalization of an Encoder-decoder LSTM model for flood prediction in ungauged catchments':
The repository includes sample workflow codes for using Encoder-decoder LSTM model to set up, train, and evaluate a regional and PUB flood prediction model.
1) `lstm_regional.py`/`lstm_regional.ipynb` -- Regional model: The Encoder-decoder LSTM-regional model will be trained on flood events at all 35 catchments, 50% as the training set, 25% as validation set, 25% as the test set. Namely one model for prediction on all catchments.
2) `lstm_pub.py`/'lstm_pub.ipynb' -- Prediction in ungauged basin (PUB) model: K-fold split strategy is introduced to achieve pseudo PUB prediction on the entire dataset. The ED-LSTM-PUB models are trained on flood events at k-1 folds of catchments as gauged catchments, and test on catchments the rest fold as ungauged catchments. The process is repeated k times until all catchments are tested as ungauged catchments once.
3) The model structure:
![image](https://github.com/yikuizh/edlstm_flood_prediction/assets/55485922/17d66385-c84c-4e5c-9d0f-092ead568017)


# How to run:
1) Prepare your dataset: If you have a continuous long-term streamflow dataset, first slice the continuous dataset into individual flood events at an hourly scale, as well as the corresponding runoff, precipitation, and temperature data.
2) Run scripts: The first is to connect the Google Colab service for using GPU for training. Then assign the correct directories for your training data on Google Drive. If a local GPU is available, you must adjust the local use codes;
3) The dependency -- load google colab:
```
!apt-get install -y -qq software-properties-common python-software-properties module-init-tools
!add-apt-repository -y ppa:alessandro-strada/ppa 2>&1 > /dev/null
!apt-get update -qq 2>&1 > /dev/null
!apt-get -y install -qq google-drive-ocamlfuse fuse
from google.colab import auth
auth.authenticate_user()
from oauth2client.client import GoogleCredentials
creds = GoogleCredentials.get_application_default()
import getpass
!google-drive-ocamlfuse -headless -id={creds.client_id} -secret={creds.client_secret} < /dev/null 2>&1 | grep URL
vcode = getpass.getpass()
!echo {vcode} | google-drive-ocamlfuse -headless -id={creds.client_id} -secret={creds.client_secret}
```
Load packages for deep learning:
```
import keras
import keras.backend as K
from keras.layers import TimeDistributed, Dense, LSTM, RepeatVector, Dropout, Input, Flatten,Concatenate
from keras.models import load_model
from keras.models import Model
from keras import optimizers
from tensorflow import optimizers
```

3) Collect results: After successfully running the script, it will output csv files that collect the median NSE score at each catchment.
4) N.B. The hyperparameters selection process has been skipped here.
5) N.B. If you have any questions about the dataset, please don't hesitate to contact the author for further information.

### Citation for the paper: https://doi.org/10.1016/j.jhydrol.2022.128577
