# Surfs Up Analysis

## Finished Jupyter Notebook Deliverables:    
[Climate Analysis](/climate_analysis.ipynb)      
[Surfs Up Challenge](/SurfsUp_Challenge.ipynb)  

## Overview of Analysis
Provide June and December historical Oahu temperature data for analysis that will determine whether or not an ice cream/surf business is sustainable year-round.

## Results
In the climate analysis, I reflected tables in SQL Alchemy given a flat SQL file: [Hawaii_SQLITE](/hawaii.sqlite)    
From there, I was able to write queries to filter the database tables and retrieve answers to our pressing questions.  For the challenge, I determined the statistics for June by first querying the tables with this code:  
```
results_D1 = session.query(Measurement.tobs).filter(extract('month', Measurement.date) == '06')
```  
For December, I used "strftime" instead of "extract."  
```
results_D2 = session.query(Measurement.tobs).filter(func.strftime("%m", Measurement.date) == "12")
```  
After converting to a list and then a DataFrame, I was then able to do "df.describe()" to see the statistics:  

![June December Temps Side By Side](/June_December_Temps_Side_By_Side.png "June Temps")
  
### Three key differences
* There is more historical data for June, but still a substantial amount for a side-by-side comparison    
* June temperatures are higher for every statistical metric, but December is still very warm with a relatively low amount of deviation (only a std difference of 0.49)    
* As we near the top percentiles, differences between December and June temperatures shrink  
  -Max June temperature is only 2 degrees higher than December  
    
## Summary 
It is clear that June is a warmer month, but it's still possible that this is a viable business idea.  December has some hot days so an appetite for ice cream and surfing may make still exist in the winter months.
### Additional Queries
something, something, something
