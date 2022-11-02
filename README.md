# Surf's Up Challenge
Module 9 Advanced Data Storage and Retrieval Challenge Assignment
## Overview of the Statistical Analysis
The purpose of the analysis was to summarize temperature data for the months of June and December in Oahu to determine if the surf and ice cream shop business is sustainable year-round.
### Resources:
- Data Source: [SurfsUp_Challenge.ipynb](https://github.com/banasibb/surfs_up/blob/79544847a49a8c16ff56379493862b2f54435fce/SurfsUp_Challenge.ipynb), [hawaii.sqlite](https://github.com/banasibb/surfs_up/blob/7ffb5581e784e225a4126853e1fe9df2e37737af/hawaii.sqlite)
- Software: Python, 3.7.6, Microsoft Virtual Studio Code 1.71.1, SQLAlchemy, Jupyter Notebook 2.27.21
### Analysis Components:
As part of the module coursework (completed prior to the challenge assignment), tasks #1 through #5 below were required. Tasks #6 through #8 were required as part of the PyPoll Challenge :
  1. Calculate a total number of votes cast.
  2. Get a complete list of candidates who received votes.
  3. Calculate the total number of votes each candidate received.
  4. Calculate the percentage of votes each candidate won.
  5. Determine the winner of the election based on popular vote.
  6. Calculate voter turnout for each county.
  7. Calculate the percentage of votes from each county out of the total count.
  8. Determine the county with the highest turnout.
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
## Summary
There is a high-level summary of the results and there are two additional queries to perform to gather more weather data for June and December
### Include Preciptation for the Month of June
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
![March_Temps](https://github.com/banasibb/surfs_up/blob/e511fd8ca74bbba6845f46f5ddf78485a7acada3/Resources/March_Summary_Stats.png)
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
![March_Temps](https://github.com/banasibb/surfs_up/blob/e511fd8ca74bbba6845f46f5ddf78485a7acada3/Resources/March_Summary_Stats.png)
Using a bulleted list, address the following election outcomes. Use images or examples of your code as support where necessary.
- How many votes were cast in this congressional election?<br />
  The total number of votes cast in the election was 369,711.

- Provide a breakdown of the number of votes and the percentage of the total votes each candidate received.<br />
  Charles Casper Stockham: 23.0% (85,213)<br />
  Diana DeGette: 73.8% (272,892)<br />
  Raymon Anthony Doane: 3.1% (11,606)<br />
  <br />The following excerpt of code was written to conduct this analysis:<br />
 ```
    for candidate_name in candidate_votes:
        # Retrieve vote count and a percentage of votes.
        votes = candidate_votes[candidate_name]
        vote_percentage = float(votes) / float(total_votes) * 100
        candidate_results = (
            f"{candidate_name}: {vote_percentage:.1f}% ({votes:,})\n")
  ```
  
- Which candidate won the election, what was their vote count, and what was their percentage of the total votes?<br />
    The winner of the election was Diana DeGette, with a total of 272,892 votes or 73.8% of the total votes.<br />
    <br />The following code was required to conduct this analysis and print the results to the terminal: <br />
 ```
june = session.query(Measurement.date, Measurement.tobs).filter(extract('month',Measurement.date) ==6)
  ```
- Provide a breakdown of the number of votes and the percentage of total votes for each county in the precinct.<br />
    The results for each county are as follows:<br />
     Jefferson: 10.5% (38,855)<br />
     Denver: 82.8% (306,055)<br />
     Arapahoe: 6.7% (24,801)<br />
     <br />The following code was required to conduct this analysis and print the results to the terminal: <br />
 ```
    for county in county_options:
        county_vote = county_votes[county]
        county_vote_percentage = float(county_vote) / float(total_votes) * 100
        county_results = (
            f"{county}: {county_vote_percentage:.1f}% ({county_vote:,})\n"
            )
        print(county_results, end="")
        txt_file.write(county_results)
  ```
- Which county had the largest number of votes?<br />
    Denver County had the largest voter turnout with 306,055 votes or 82.8% of total votes cast.<br />
     <br />The following code was required to conduct this analysis and print the results to the terminal: <br />
 ```
        if (county_vote > largest_county_turnout_votes) and (
            county_vote_percentage > largest_county_turnout_percentage):
            largest_county_turnout_votes = county_vote
            largest_county_turnout_percentage = county_vote_percentage
            largest_county_turnout = county

    winning_county_summary = (
        f"-------------------------\n"
        f"Largest County Turnout: {largest_county_turnout}\n"
        f"-------------------------\n"
        )
    print(winning_county_summary)
    txt_file.write(winning_county_summary)
  ```
## Election-Audit Summary
This script could be used to analyze the results of any election, and may be improved upon if it also included an analysis of the total and percentage of total votes by candidate by individual county, which could be used for campaign strategy purposes in future elections. This could help candidates target key geographic areas underserved by their messaging. The analysis may also be improved by the incorporation of the population of each county to identify geographic regions where voter turnout is low. This information could be used to target key areas that may have low percentages of the population that are registered to vote or lack awareness of upcoming elections.

