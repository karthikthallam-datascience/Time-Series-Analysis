# Time-Series-Analysis
Time Series Forecasting of monthly sales for Retail and Food services using Recurrent Neural Network(RNN)

1) Data:

Release: Advance Monthly Sales for Retail and Food Services  
Units:  Millions of Dollars, Not Seasonally Adjusted

Frequency:  Monthly

The value for the most recent month is an advance estimate that is based on data from a subsample of firms from the larger Monthly Retail Trade Survey. The advance estimate will be superseded in following months by revised estimates derived from the larger Monthly Retail Trade Survey. The associated series from the Monthly Retail Trade Survey is available at https://fred.stlouisfed.org/series/MRTSSM448USN

Information about the Advance Monthly Retail Sales Survey can be found on the Census website at https://www.census.gov/retail/marts/about_the_surveys.html

Suggested Citation:
U.S. Census Bureau, Advance Retail Sales: Clothing and Clothing Accessory Stores [RSCCASN], retrieved from FRED, Federal Reserve Bank of St. Louis; https://fred.stlouisfed.org/series/RSCCASN, November 16, 2019.


2) Train/Test split

3) Scaling

4) Batch Generator using TimeSeriesGenerator class

5) Create a Model

6) Early stopping and Validation generator & fit the model through generator:

    a) model.fit_generator(generator, validation_data=validation_generator, epochs=20, callbacks=[early_stop])
    
7) Evaluate on the Test Data

8) Retrain the model on the whole data and Forecast into unknown future:

      a) full_scaled_data
      
      b) Batch Generator
      
      c) Create the model
      
      d) Since we are forecasting into the unknown future no need for using Early_stop and validation_generator
      
      e) model.fit_generator(generator, epochs=8)
      
      f) Forecasting:
      
          forecast = []
          
          months_to_predict = 12
          
          first_eval_bacth = scaled_full_data[-length:]
          
          current_batch = first_eval_batch.reshape((1, length, n_features))
          
          for i in range(months_to_predict):
          
              current_pred = model.predict(current_batch)[0]
              
              forecast.append(current_pred)
              
              current_bacth = np.append(current_batch(:, 1:, :), [[current_pred]], axis=1)
              
      
      g) Inverse_Transformation on the forecasted values:
      
          forecast = scaler.inverse_transform(forecast)
          
      h) Add these forecasted values with the timestamps to create forecasted_index:
      
          forecast_index = pd.date_range(start='2019-10-11', periods=months_to_predict, freq='MS')
          
          forecast_df = pd.DataFrame(data=forecast, index=forecast_index, columns=['Forecast'])
          
      i) Plot the both graphs on the same axis:
      
          ax = df.plot()
          
          forecast_df.plot(ax=ax)
          
              
              plt.xlim('2018-10-11', '2020-10-11')   .......... to zoom-in 
    
