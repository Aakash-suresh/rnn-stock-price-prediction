# Stock Price Prediction

## AIM

To develop a Recurrent Neural Network model for stock price prediction.

## Problem Statement and Dataset

## Neural Network Model

Include the neural network model diagram.

## DESIGN STEPS

### STEP 1:
Import the tensorflow modules
### STEP 2:
Load the stock datatset
### STEP 3:
fit the model and then predict
## PROGRAM
```
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
from sklearn.preprocessing import MinMaxScaler
from keras import layers
from keras.models import Sequential

dataset_train = pd.read_csv('trainset.csv')

dataset_train.columns

dataset_train.head()

train_set = dataset_train.iloc[:,1:2].values
plt.plot(np.arange(0,1259),train_set)

sc=MinMaxScaler(feature_range=(0,1))
training_set_scaled = sc.fit_transform(train_set)
train_set.shape

type(train_set)

sc = MinMaxScaler(feature_range=(0,1))
training_set_scaled = sc.fit_transform(train_set)

training_set_scaled.shape

X_train_array = []
y_train_array = []
for i in range(80, 1259):
  X_train_array.append(training_set_scaled[i-80:i,0])
  y_train_array.append(training_set_scaled[i,0])
X_train, y_train = np.array(X_train_array), np.array(y_train_array) 
X_train1 = X_train.reshape((X_train.shape[0], X_train.shape[1],1))

X_train.shape

X_train1.shape

length = 80
n_features = 1

model = Sequential()

model.add(layers.SimpleRNN(40,input_shape=(length,n_features)))
model.add(layers.Dense(1))

model.compile(optimizer='adam',loss='mse')

model.summary()

model.fit(X_train1,y_train,epochs=100, batch_size=64)

dataset_test = pd.read_csv('testset.csv')
dataset_test.head()

dataset_test.head()

test_set = dataset_test.iloc[:,1:2].values
test_set.shape

dataset_total = pd.concat((dataset_train['Open'],dataset_test['Open']),axis=0)
dataset_total.shape

inputs = dataset_total.values
inputs.shape

inputs = inputs.reshape(-1,1)
inputs_scaled=sc.transform(inputs)
X_test = []
for i in range(80,1384):
  X_test.append(inputs_scaled[i-80:i,0])
X_test = np.array(X_test)
X_test = np.reshape(X_test,(X_test.shape[0], X_test.shape[1],1))

X_test.shape

predicted_stock_price_scaled = model.predict(X_test)
predicted_stock_price = sc.inverse_transform(predicted_stock_price_scaled)

predicted_stock_price.shape

plt.plot(np.arange(0,1384),inputs, color='red', label = 'Test(Real) Google stock price')
plt.plot(np.arange(80,1384,),predicted_stock_price, color='blue', label = 'Predicted Google stock price')
plt.title('Google Stock Price Prediction')
plt.xlabel('Time')
plt.ylabel('Google Stock Price')
plt.legend()
plt.show()
```
## OUTPUT

### True Stock Price, Predicted Stock Price vs time

![output](A.png)

### Mean Square Error

![output](B.png)

## RESULT
Thus, a Recurrent Neural Network model for stock price prediction is developed.

