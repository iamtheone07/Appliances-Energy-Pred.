# Appliances-Energy-Prediction
This project deals with predicting appliances energy consumption of a particular household in Belgium based on the temperature and humidity levels of different rooms in the building and the weather reports in the area over a period of 4.5 months.

The data set is at 10 min for about 4.5 months. The house temperature and humidity conditions were monitored with a ZigBee wireless sensor network. Each wireless node transmitted the temperature and humidity conditions around 3.3 min. Then, the wireless data was averaged for 10 minutes periods. The energy data was logged every 10 minutes with m-bus energy meters. Weather from the nearest airport weather station (Chievres Airport, Belgium) was downloaded from a public data set from Reliable Prognosis (rp5.ru) and merged together with the experimental data sets using the date and time column. Two random variables have been included in the data set for testing the regression models and to filter out non-predictive attributes (parameters).

Dataset Information

Number of instances: 19,735

Number of attributes: 29

Attribute Information

date: year-month-day hour:minute:second

T1: Temperature in kitchen area, in Celsius

RH_1: Humidity in kitchen area, in %

T2: Temperature in living room area, in Celsius

RH_2: Humidity in living room area, in %

T3: Temperature in laundry room area

RH_3: Humidity in laundry room area, in %

T4: Temperature in office room, in Celsius

RH_4: Humidity in office room, in %

T5: Temperature in bathroom, in Celsius

RH_5: Humidity in bathroom, in %

T6: Temperature outside the building (north side), in Celsius

RH_6: Humidity outside the building (north side), in %

T7: Temperature in ironing room, in Celsius

RH_7: Humidity in ironing room, in %

T8: Temperature in teenager room 2, in Celsius

RH_8: Humidity in teenager room 2, in %

T9: Temperature in parents’ room, in Celsius

RH_9: Humidity in parents’ room, in %

T_out: Temperature outside (from Chievres weather station), in Celsius

Pressure: (from Chievres weather station), in mm Hg

RH_out: Humidity outside (from Chievres weather station), in %

Wind speed: (from Chievres weather station), in m/s

Visibility: (from Chievres weather station), in km

T_dewpoint: (from Chievres weather station), Â°C

rv1: Random variable 1, non-dimensional

rv2: Random variable 2, non-dimensional

Lights: energy use of light fixtures in the house in Wh

Appliances: energy use in Wh (Target Variable)

DATA EXPLORATION

Number of instances: 19,735 Number of attributes: 29

No NaN Values found. No Duplicates found. As maximum value in lights attribute is 0, it wont be playing much role in our model. Hence we are dropping the lights attribute from our dataset.

Renamed Temperature and Humidity Features Accordingly using dictionary as below:

temp = { 'T1' : 'kitchen_temp', 'T2' : 'living_temp', 'T3' : 'laundry_temp', 'T4' : 'office_temp', 'T5' : 'bath_temp', 'T6' : 'outside_temp', 'T7' : 'ironing_temp', 'T8' : 'teen_temp', 'T9' : 'parents_temp', 'T_out' : 'station_temp' }

humid = { 'RH_1' : 'kitchen_humid', 'RH_2' : 'living_humid', 'RH_3' : 'laundry_humid', 'RH_4' : 'office_humid', 'RH_5' : 'bath_humid', 'RH_6' : 'outside_humid', 'RH_7' : 'ironing_humid', 'RH_8' : 'teen_humid', 'RH_9' : 'parents_humid', 'RH_out' : 'station_humid' }

INSIGHTS FROM DATA VISUALIZATION:

Observations⚡:

Average energy consumption of appliances at different time of the day over a period of 4.5 months, we observe two peak hours. One at 11 am in the morning and other at 6 PM in the evening. While the peak at 11 am is shallow and low, peak at 6 PM is comparatively higher and sharper.

We observe that over the sleeping hours (10 PM - 6 AM) the energy consumption of appliances is around 50 Wh. After about 6 AM, energy consumption starts to rise gradually up until 11 AM (probably due to morning chores). And then gradually decreases to around 100 Wh at about 3 PM. After which the energy consumption drastically shoots up up until 6 PM in the evening (probably due to requirement lights in rooms). However energy consumption of appliances reverts back to 50 Wh, as night approaches and people in the house go to bed at around 10 PM.

Insights ⚡: We observe that the energy consumption of appliances during the 8 AM - 4 PM is higher in weekends compared to the weekdays. Also, average overall consumption in weekends is pretty high.

Insights⚡:

90% of Appliance consumption is less than 200 Wh .

This column is postively skewed , most the values are around mean 100 Wh .

There will be outliers in this column.

There are small number of cases where consumption is very high.

Observations⚡:

Outside Average temperature over a period of 4.5 months is around 7.5 degrees and ranges from -6(min) to 28(max) degrees.

Inside the building avarage temperature has been around 20 degrees for all the rooms and ranges from 14(min) to 30(max) degrees.

Note: These points implies that warming appliances have been used to keep the insides of the building warm. There must be some sort of direct correlation b/w temperature and consumption of energy inside the house.

Observations⚡:

Outside the building average temp > average humidity inside the house.

Average humidity at the weather station > outside humidity near the building.

Average humidity in the bathroom > other rooms due to obvious reasons.

Kids and parent room show a comparatively higher average humidity.

OBSERVATIONS⚡:

From the correlation graph we clearly observe that the features related to temperature and features related to humidity have positive correlation within themselves whereas have a a very low or negative correlation with each other.

Humidity outside have a strong negative correlation with temperature levels.

Apart from that we observe that a couple features such as humidity at station, temperature outside the building and temperature in the living room have a comparatively high absolute correlation (above 0.12) with Appliances energy consumption.

CONCLUSION:

● Dataset doesn’t have any null values.

● We have observed very less co-relation between the target and feature variables.

● Dropped features like rv1 & rv2 as it has infinity VIF.

● Top 2 models were Extra Tree Regressor & Random Forest.

● Worked on Multi-Collinearity, but not much significant effect on the dataset.

● Tree based models are the best ones while dealing with features which has very less correlation with the target variable.

