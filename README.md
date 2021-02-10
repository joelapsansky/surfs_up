# Surfs Up Analysis

###Finished Jupyter Notebook Deliverables:    
[Climate Analysis](/climate_analysis.ipynb)      
[Surfs Up Challenge](/SurfsUp_Challenge.ipynb)  

## Overview of Analysis
Provide June and December historical Oahu temperature data for analysis that will determine whether or not an ice cream/surf business is sustainable year-round.

## Results
In the climate analysis, I reflected tables in SQL Alchemy given a flat SQL file: [Hawaii](/hawaii.sqlite)    
From there, I was able to write queries to filter the database tables and retrieve answers to our pressing questions.  For the challenge, I determined the statistics for June by first querying the tables with this code:  
```
results_D1 = session.query(Measurement.tobs).filter(extract('month', Measurement.date) == '06')
```  
For December, I used "strftime" instead of "extract."  
```
results_D2 = session.query(Measurement.tobs).filter(func.strftime("%m", Measurement.date) == "12")
```  
After converting to a list and then a DataFrame, I was then able to do "df.describe()" to see the statistics:  

![June Temps](/June_Temps.png "June Temps") ![December Temps](/December_Temps.png "December Temps")  
  
### Three key differences
* Diff1  
* Diff2  
* Diff3  
    
## Summary 
High-level summary and two additional queries that gather more weather data for December and June.

### Additional Queries
something, something, something