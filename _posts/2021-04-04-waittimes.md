---
layout: post
title: Disney World Wait Times
description: Predictive multivariate time series model using LSTM neural network with Keras.
image:
---


## Multivariate Time Series Predictive Model

### Summary
Can wait times for a Disney World attraction be predicted?

A recurrent neural network is used to predict wait times for the Walt Disney World attraction, Pirates of the Caribbean. Long short-term memory (LSTM) is used from the Keras library to create a predictive model. This project demonstrates the full data science process from data wrangling, exploratory data analysis, model building and making predictions.

The wait time data used was collected from 2016-2019. Additional variables such as weather, park hours, holidays, parades, and percentage of schools in session were used as input variables. It was trained on two years worth of data, tested on 1 year of data, and finally validated on 1 additional year of data. Predictions are compared to the actual wait times to further gain an understanding of how well the model performed.


### Tools
* Keras
* Pandas
* Scikit-learn
* Matplotlib

### Modeling Methods
* Recurrent neural network
* LSTM

### Results
On the validation set, the final model produced an RMSE of 7.174, which equates to 7.174 minute variance from the actual wait time.

### Project Preview

#### Exploratory Data Analysis
Through EDA, you can see trends in longer wait times vs. shorter wait times from yearly, weekly, and daily trends.

![Average Month](/assets/images/wait_avg_month.jpg)

![Average Day](/assets/images/wait_avg_day.jpg)

![Yearly Graphed](/assets/images/wait_one_year.jpg)

![Weekly Graphed](/assets/images/wait_one_week.jpg)

![Day Graphed](/assets/images/wait_one_day.jpg)

![Wait vs School](/assets/images/wait_vs_school.jpg)

#### Modeling
The time series data was reformatted for a supervised learning algorithm using one timestep in the past to predict one future timestep.

The final model used 1 LSTM layer with constraint of 50 and 1 dense layer. The training set was fitted on 100 epochs with a batch size of 72.

![Model Summary](/assets/images/wait_model_summary.JPG)

```
# create the model
model = Sequential()
model.add(LSTM(50, input_shape=(train_X.shape[1], train_X.shape[2])))
model.add(Dense(1))
model.compile(loss='mae', optimizer='adam')

# fit the model
history = model.fit(train_X, train_y, epochs=100, batch_size=72,
	validation_data=(test_X, test_y), verbose=2, shuffle=False)

# predict on test
yhat = model.predict(test_X)
model_test_X = test_X.reshape((test_X.shape[0], test_X.shape[2]))

# invert scaling for forecast
inv_yhat = np.concatenate((yhat, model_test_X[:, 1:]), axis=1)
inv_yhat = scaler.inverse_transform(inv_yhat)
inv_yhat = inv_yhat[:,0]

# invert scaling for actual
model_test_y = test_y.reshape((len(test_y), 1))
inv_y = np.concatenate((model_test_y, model_test_X[:, 1:]), axis=1)
inv_y = scaler.inverse_transform(inv_y)
inv_y = inv_y[:,0]

# calculate RMSE
rmse = sqrt(mean_squared_error(inv_y, inv_yhat))
print('Test RMSE: %.3f' % rmse)

# calculate MAE
mae = mean_absolute_error(inv_y, inv_yhat)
print('Test MAE: %.3f' % mae)
```

The training set started to smooth out after about 40 epochs. The test set had fluctuations in residuals always just above the training set without overfitting or underfitting the data, but never converging.

![Train Validation Loss](/assets/images/wait_train_val_loss.jpg)

#### Predictions
10% of the predicted values are plotted against the actual values. The lines fall very close to each other, following the same trends through each timestep in the data.

![Predictions](/assets/images/wait_predicted_vs_actual.jpg)

### Presentation Deck
<iframe src="https://bellevueuniversity-my.sharepoint.com/:p:/g/personal/tcapobianco_my365_bellevue_edu/Ee0WA9zGslZMn7kP8UPi5mgBuutTUQ99Z1edLIJ8fhvKFA?e=plZ1oW&amp;action=embedview&amp;wdAr=1.7777777777777777" width="962px" height="565px" frameborder="0">This is an embedded <a target="_blank" href="https://office.com">Microsoft Office</a> presentation, powered by <a target="_blank" href="https://office.com/webapps">Office</a>.</iframe>
<br>

### The Complete Project
<section id="Repository">
	<div class="inner">
    <ul class="actions fit small">
      <li><a href="https://github.com/Torreylee1028/Disney-World-Wait-Times" target="_blank" class="button small">View Repository</a></li>
    </ul>
	</div>
</section>
