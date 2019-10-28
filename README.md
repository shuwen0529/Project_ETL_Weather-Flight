# ETL project: weather hindcast and forecast influence flights in JFK

## Project goal: 
In this project, we are reporting weather data for the JFK airport
1) To review how weather conditions influence the delays of the departure and arrival flights in 2013;
2) To inspect the following 5-day weather forecast from today so that they can predict the air traffics. 

## ETL process:
1) Extract
   Jupiter Notebook is used to extract data from the following data source:
   * The historical weather datasets are from Kaggle (https://www.kaggle.com/selfishgene/historical-hourly-weather-data/version/2). The dataset contains 5 years of hourly measurements data of six weather attributes (temperature, humidity, air pressure, wind direction, wind speed, weather description) for 30 U.S. and Canadian Cities.
   * The flight data is from Kaggle (https://www.kaggle.com/lampubhutia/nyc-flight-delay), which contains all flights (336,776 in total) that departed from NYC (e.g. EWR, JFK and LGA) in 2013.
   * The weather forecast data is acquired using Weather API on the OpenWeatherMap website, in which the forecast is available every three hour in the future 5 days.

2) Transform 
   * For the historical weather data, the five weather variables (temperature, humidity, pressure, wind_speed, wind_direction) are retrieved only in year 2013 and then averaged daily; the sixth variable “weather description” is string, so we select the most frequent weather_description by day. 
   * For the flight data, we clean up the csv table by only keeping JFK airport information; then filtering columns by only keeping delayed flights (>0) based on the departure delays ("dep_delay") and arrival delays ("arr_delay"); at last the daily total number of delayed flights are transformed into dataframe.
   The above two tabled are joined together and saved to sqlite, so far the first project goal is met.
   * For the weather forecast, we build query URL by using API key to get weather forecast from OpenWeatherMap website, the request list is transformed into dataframe and saved to sqlite. The second project goal is met.

3) Load
The final tables include:
 * NewYork_JFKflight_Delay_2013, which is created from ETL_HistoricalData.ipynb and used to show the relation of the delayed flights in New York JFK airport and the weather conditions in 2013.
 * NewYork_WeatherForecast, which is created from ETL_5DayForecast.ipynb and used to show the future 5 days weather forecast in every three hours, in order to help the JFK airport manage the air traffic.

## Limitations
The historical flight data is only available in 2013 in Kaggle, which really limits us to draw the conclusion that how the delayed flights are related to the weather conditions. 

### Created by Shuwen Zhang, Julia Nalyvaiko, Rajinder Gill
