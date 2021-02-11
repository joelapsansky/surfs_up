# Surfs Up Analysis

## Finished Jupyter Notebook Deliverables:      
[Climate Analysis](/climate_analysis.ipynb)  
[Surfs Up Challenge](/SurfsUp_Challenge.ipynb)  

## Overview of Analysis
Provide June and December historical Oahu temperature data for an analysis that will determine whether or not an ice cream/surf business is sustainable year-round.

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

![June December Temps Side By Side](/June_December_Temps_Side_By_Side.png "June & December Temps")
  
### Three key differences
* There is more historical data for June evident by the counts, but still a substantial amount of data for a side-by-side comparison    
* June temperatures are higher for every statistical metric, but December is still very warm with a relatively low amount of deviation (only a std difference of 0.49)    
* As we near the top percentiles, differences between December and June temperatures shrink  
  -Max June temperature is only 2 degrees higher than December  
    
## Summary 
It is clear that June is a warmer month, but it's still possible that this is a viable, year-round business.  December has some hot days so an appetite for ice cream and surfing may still exist in the winter months.
### Additional Queries
Digging further, we can look at precipitation as a guide to help us with our decision.  June shows us a total precipitation level of 194.11 inches whereas December shows 304.63.  These results come from this code, which passes December and June into the query:  
  
```
month = ['6','12']
year = '2017'
prcp_results = session.query(func.sum(Measurement.prcp)).\
    filter(extract('year', Measurement.date) < year).\
    filter(extract('month', Measurement.date).in_(month)).\
    group_by(extract('month', Measurement.date)).all()
prcp_results = [round(prcp, 2) for prcp in list(np.ravel(prcp_results))]
prcp_results
```  
  
The results are reduced to earlier than 2017 to make sure we're calculating statistics on an even number of summers and winters.  We did not have December 2017 data available.   
    
It's also useful to calculate statistics for all rainy days in both June and December.  
  
```
# June Precipitation Statistics
stats_June = session.query(Measurement.prcp).\
    filter(extract('year', Measurement.date) < '2017').\
    filter(extract('month', Measurement.date) == '6').\
    filter(Measurement.prcp > 0.0)
stats_June = [result[0] for result in stats_June]
stats_June = pd.DataFrame(stats_June, columns=['June Precipitation Stats'])
stats_June.describe()
```  
  
The code above only returns days in June with precipitation greater than 0 (no rain).  If we run it for December as well, the side-by-side results look like this:  
![June December Prcp Side By Side](/June_December_Prcp_Side_By_Side.png "June & December Prcp")  
It is fairly clear that June is more desirable as it has less rainy days, a lower average, a lower total, and less variation.  This means that June is dryer, more predictable, and thus way more likely to generate higher sales.
