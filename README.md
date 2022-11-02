# Surf's Up Challenge
Module 9 Advanced Data Storage and Retrieval Challenge Assignment
## Overview of the Statistical Analysis
The purpose of the analysis was to summarize temperature and climate data for the months of June and December in Oahu, Hawaii to determine if the surf and ice cream shop business is sustainable.
### Resources:
- Data Source: [SurfsUp_Challenge.ipynb](https://github.com/banasibb/surfs_up/blob/79544847a49a8c16ff56379493862b2f54435fce/SurfsUp_Challenge.ipynb), [hawaii.sqlite](https://github.com/banasibb/surfs_up/blob/7ffb5581e784e225a4126853e1fe9df2e37737af/hawaii.sqlite)
- Software: Python, 3.7.6, Microsoft Virtual Studio Code 1.71.1, SQLAlchemy, Jupyter Notebook 2.27.21
### Analysis Components:
As part of the module coursework (completed prior to the challenge assignment), the following tasks were undertaken to explore the provided weather data:
1. Determine the structures, interactions, and types of data of a provided dataset.
2. Differentiate between SQLite and PostgreSQL databases featured in earlier modules.
3. Use SQLAlchemy to connect to and query a SQLite database.
4. Use statistics like minimum, maximum, and average to analyze data, specifically using a .describe() function.
5. Design a Flask application using data.
## Results
There is a bulleted list that addresses the three key differences in weather between June and December.
### Deliverable 1: Summary Statistics for June

Using Python, Pandas functions and methods, and SQLAlchemy, the date column of the Measurements table in the hawaii.sqlite database was filtered to retrieve all the temperatures for the month of June. The temperatures were then converted to a list, a DataFrame was created from the list, and summary statistics were generated.<br />
<br />The code used to filter on the month of June was as follows: <br />
 ```
june = session.query(Measurement.date, Measurement.tobs).filter(extract('month',Measurement.date) ==6)
  ```
A .describe() function was used to calculate the mean, minimum, maximum, standard deviation, and percentiles. The results were as follows:<br />
![June_Temps](https://github.com/banasibb/surfs_up/blob/7ffb5581e784e225a4126853e1fe9df2e37737af/Resources/June_Summary_Stats.png)
### Deliverable 2: Summary Statistics for December
The same methods were applied as for Deliverable 1, but using the temperatures for the month of December. The temperatures were then converted to a list, a DataFrame was created from the list, and summary statistics were generated.<br />
<br />The code used to filter on the month of December was as follows: <br />
 ```
dec = session.query(Measurement.date, Measurement.tobs).filter(extract('month',Measurement.date) ==12)
  ```
A .describe() function was used to calculate the mean, minimum, maximum, standard deviation, and percentiles. The results were as follows:<br />
![Dec_Temps](https://github.com/banasibb/surfs_up/blob/7ffb5581e784e225a4126853e1fe9df2e37737af/Resources/Dec_Summary_Stats.png)
### Findings
- There were 1,700 measurements taken for the month of June, compared to 1,517 for the month of December. 
- The mean or average temperature in the month of June over the time period included in the analysis was approximately 74 degrees, compared to 71 degrees in December. 
- The minimum temperature for the month of December (56 degrees) was approximately eight degrees cooler than the minimum temperature in the month of June (64 degrees). 
## Summary
The findings showed that in terms of temperature alone, the months of June and December are not significantly different. The analysis could be improved upon if the precipitation data were incorporated into the analysis, as this may offer more insight into weather fluctuations that could impact sales.
### Additional Query 1: Include Preciptation for the Month of June
<br />The following code was used to create a new DataFrame that includes preciptation data for the month of June: <br />
 ```
juneprcptobs = session.query(Measurement.date, Measurement.prcp, Measurement.tobs).\
filter(extract('month',Measurement.date) ==6).all()
june_tobs_prcp=list((juneprcptobs))
june_tobs_prcp_df = pd.DataFrame(june_tobs_prcp,columns=['date','June Precip','June Temps'])
june_tobs_prcp_df.set_index(june_tobs_prcp_df['date'],inplace=True)
june_tobs_prcp_df.describe()
  ```
The results were as follows:<br />
![June_Rainfall_Temps](https://github.com/banasibb/surfs_up/blob/698ab82178b4b63a6e83a6437ea81a21571ab32a/Resources/June_Summary_Rainfall_Temps.png)
### Additional Query 1: Include Preciptation for the Month of December
<br />The following code was used to create a new DataFrame that includes preciptation data for the month of December: <br />
 ```
decprcptobs = session.query(Measurement.date, Measurement.prcp, Measurement.tobs).\
filter(extract('month',Measurement.date) ==12).all()
dec_tobs_prcp=list((decprcptobs))
dec_tobs_prcp_df = pd.DataFrame(dec_tobs_prcp,columns=['date','Dec Precip','Dec Temps'])
dec_tobs_prcp_df.set_index(dec_tobs_prcp_df['date'],inplace=True)
dec_tobs_prcp_df.describe()
  ```
The results were as follows:<br />
![Dec_Rainfall_Temps](https://github.com/banasibb/surfs_up/blob/caa087ca758b76a02a0931f46d9ed8901bc466af/Resources/Dec_Summary_Rainfall_Temps.png)
