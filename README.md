# Olympic Games Data Analysis



## About The Project

The motivation behind this project is to analyze the historical data of Olympic games to understand the performance of different nations and competitors.




### Built With

* [PowerBI](https://powerbi.microsoft.com/en-au/)




## Data Overview
The necessary data was first put into a SQL database and afterwards transformed using the transformations that you can see below.
```
SELECT
         [ID]
        ,[Name] AS 'Competitor Name' 
        ,CASE WHEN SEX = 'M' THEN 'Male' ELSE 'Female' END AS Sex
        ,[Age]
		,CASE	WHEN [Age] < 18 THEN 'Under 18'
				WHEN [Age] BETWEEN 18 AND 25 THEN '18-25'
				WHEN [Age] BETWEEN 25 AND 30 THEN '25-30'
				WHEN [Age] > 30 THEN 'Over 30'
		 END AS [Age Grouping]
        ,[Height]
        ,[Weight]
        ,[NOC] AS 'Nation Code'
        ,LEFT(Games, CHARINDEX(' ', Games) - 1) AS 'Year'
        ,[Sport]
        ,[Event]
        ,CASE WHEN Medal = 'NA' THEN 'Not Registered' ELSE Medal END AS Medal 
  FROM [olympic_games].[dbo].[athletes_event_results]
  WHERE RIGHT(Games,CHARINDEX(' ', REVERSE(Games))-1) = 'Summer'
```


### Data Model
Using the previous query the data was loaded into Power BI. The following image depicts the final data model. <br />
![data_model](https://github.com/AzT3Risk/Olympic-Games-Data-Analysis/blob/main/Data_model.PNG)


### Calculations
The following calculations were created in the Power BI reports using DAX (Data Analysis Expressions).

Number of Competitors:
```
# of Competitors = DISTINCTCOUNT('Olympics Games Data'[ID])
```

Number of Medals:
```
# of Medals = COUNTROWS('Olympics Games Data')
```

Number of Medals (Registered):
```
# of Medals (Registered) = 
CALCULATE (
    [# of Medals],
    FILTER (
        'Olympics Games Data',
        'Olympics Games Data'[Medal] = "Bronze"
            || 'Olympics Games Data'[Medal] = "Gold"
            || 'Olympics Games Data'[Medal] = "Silver"
    )
)

```
## Analysis
The finished dashboard consist of visualizations and filters that will give an easy option for the end users to navigate the summer games through history. Some possibilities are to filter by period using year, nation code to focus on one country or look into either a competitor or specific sports over time.
![dashboard](https://github.com/AzT3Risk/Olympic-Games-Data-Analysis/blob/main/Dashboard.PNG)







## Contact

[Souvik Mondal](https://www.linkedin.com/in/souvik-mondal-6516ba160/) - souvik.sta8@gmail.com










