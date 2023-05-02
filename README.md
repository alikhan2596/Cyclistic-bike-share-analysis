# **Cyclistic bike-share analysis**

![cover](https://user-images.githubusercontent.com/25352514/235770671-4e2c092b-9265-49fd-8e8c-93ef9b765978.jpg)


# **About Company**

Cyclistic is a bike-share program in Chicago that offers a fleet of 5,824 bicycles and 692 stations, including options for people with disabilities. Their marketing strategy has previously focused on building general awareness and attracting casual riders through flexible pricing plans, but they now want to maximize the number of annual memberships, which are more profitable. The director of marketing wants to convert casual riders into members and has set a clear goal for the marketing analyst team to design strategies to achieve this. The team plans to analyze historical bike trip data to better understand the differences between annual members and casual riders and identify trends.

**PHASE 1: ASK**


The director of marketing at Cyclistic wants to convert casual riders into annual members to maximize profitability. The marketing analyst team needs to understand the differences between annual members and casual riders and identify trends.

Questions that will guide the future marketing program:

1. How do annual members and casual riders use Cyclistic bikes differently?
1. Why would casual riders buy Cyclistic annual memberships?
1. How can Cyclistic use digital media to influence casual riders to become members?

The team will produce a report to answer the first question of how annual members and casual riders use Cyclistic bikes differently.

Report Deliverables:

* Business Task: Clear statement of the business task.
* Data Sources: Description of all data sources used.
* Data Cleaning and Manipulation: Documentation of any cleaning or manipulation of data.
* Analysis Summary: A summary of the analysis performed.
* Visualizations and Key Findings: Supporting visualizations and key findings.
* Recommendations: Top three recommendations based on the analysis.

**PHASE 3: PROCESS**
​
To manage and format the data, Microsoft Excel will be used before importing it into CSV files to be transferred to Microsoft SQL SERVER. As there are 12 datasets, totaling more than 1 million rows, Excel would be unable to handle the heavy load. SQL is capable of performing several tasks, including merging files and generating tables, making it the ideal application to use in this case.
​
The following actions have been completed:
​
* Modified the format of the "started_at" and "ended_at" rows to date.
* Changed the format of the "start_lat," "start_lng," "end_lat," and "end_lng" rows to numbers.
* Generated a new column named "ride_duration." The duration of each ride was calculated by subtracting the "started_at" column from the "ended_at" column and formatting it as HH:MM:SS using Format > Cells > Time > 37:30:55.
* Produced a new column named "day_name," which used the "WEEKDAY" command to compute the day of the week that each ride began. The format was set to General or a number with no decimal points.
* Formulated a new column called "month_name," which used the "MONTH" command to determine the month of the year that each ride began. The format was set to General or a number with no decimal points.


		SQL Query for combining all the csv files tables into new table named "year2022_divvy_tripdata"

		SELECT *
		  INTO  year2022_divvy_tripdata
		FROM
		(
			SELECT *
			  FROM [dbo].[202201-divvy-tripdata]

			UNION ALL

			SELECT *
			  FROM [dbo].[202202-divvy-tripdata]

			  UNION ALL

			SELECT *
			  FROM [dbo].[202203-divvy-tripdata]

			  UNION ALL

			SELECT *
			  FROM [dbo].[202204-divvy-tripdata]

			  UNION ALL

			SELECT *
			  FROM [dbo].[202205-divvy-tripdata]

			  UNION ALL

			SELECT *
			  FROM [dbo].[202206-divvy-tripdata]

			  UNION ALL

			SELECT *
			  FROM [dbo].[202207-divvy-tripdata]

			  UNION ALL

			SELECT *
			  FROM [dbo].[202208-divvy-tripdata]

			  UNION ALL

			SELECT *
			  FROM [dbo].[202209-divvy-tripdata]

			  UNION ALL

			SELECT *
			  FROM [dbo].[202210-divvy-tripdata]

			  UNION ALL

			SELECT *
			  FROM [dbo].[202211-divvy-tripdata]

			  UNION ALL

			SELECT *
			  FROM [dbo].[202212-divvy-tripdata]

		)  a



		SQL Query for cleaning NULL values and store it into new table called "cyclistic_2022"

		SELECT *
		  INTO  cyclistic_2022
		FROM
		(
			select 
				* 
			from
				year2022_divvy_tripdata
			where 
				start_station_name IS NOT NULL
				AND end_station_name IS NOT NULL
				AND start_lat IS NOT NULL
				AND start_lng IS NOT NULL
				AND end_lat IS NOT NULL
				AND end_lng IS NOT NULL
		) a


The final step involved exporting the table "cyclistic_2022" as a CSV file, making it ready to be used for analysis.

**PHASE 4: ANALYSIS and SHARE**

In the subsequent stage, I utilized Tableau software to design and generate interactive visualizations for the data that was previously collected and processed. This step involved selecting appropriate charts and graphs to present the data in a clear and concise manner, allowing for easy interpretation and analysis of the trends and patterns that emerged from the data.

![monthly_usage](https://user-images.githubusercontent.com/25352514/235771943-ab56b92a-d93d-47ad-a88b-a55f64382018.PNG)

The graph illustrates the monthly usage of bikes by members and casual riders from January to December. The total number of rides per month is shown, categorized as member or casual riders. The highest usage was in May with 282,277 rides by members and 220,227 rides by casual riders. The lowest usage was in January, with 67,511 rides by members and 12,604 rides by casual riders. There is a trend of increased usage during summer months and decreased usage during winter months.

![weekly_usage](https://user-images.githubusercontent.com/25352514/235772027-7ced681c-9dea-476d-995d-dde9d7f60b17.PNG)

This data shows the number of bike rides taken by members and casual riders for each day of the week. The highest number of rides were taken by members on Thursdays with a count of 308,518, followed by Wednesdays with 301,487 and Tuesdays with 306,339. For casual riders, the highest number of rides were taken on Sundays with a count of 216,354, followed by Saturdays with 259,729 and Fridays with 177,706. It is interesting to note that the number of rides taken by members is higher than casual riders on weekdays, whereas casual riders took more rides on weekends.

![ride_duration](https://user-images.githubusercontent.com/25352514/235772102-bfb7914f-ef21-454a-9ad7-8cb2c44844fd.PNG)

The data shows the average ride duration for casual and member riders. Casual riders have an average ride duration of 25 minutes, while members have an average ride duration of 11 minutes and 12 seconds.

![rideable_type](https://user-images.githubusercontent.com/25352514/235772162-0dc19fb9-b511-4ca6-8037-c821184ca819.PNG)

The data shows the total count of rides taken by both members and casual riders based on the type of rideable. Classic bikes were used more by members than casual riders, while electric bikes were used more by casual riders. There were also a significant number of rides taken on docked bikes by casual riders.

**PHASE 5: INSIGHT**

* The graph indicates a higher usage of bikes during summer months, specifically in May, while January shows the lowest usage. Members and casual riders both show this trend.
* The data for daily bike rides shows that members tend to use the bike sharing service more on weekdays, possibly for commuting to work, while casual riders use it more on weekends for leisure activities.
* Casual riders tend to have longer average ride durations compared to members.
* Classic bikes are more popular among members, whereas casual riders prefer electric bikes. However, there is also a significant number of casual riders who use docked bikes.

**PHASE 6: ACT**

Based on the insights provided, the following recommendations can be made:

* Target marketing to convert casual riders to annual members, highlighting benefits like cost savings and priority access.
* Offer promotions and incentives to encourage annual membership, such as discounted rates and free trial periods.
* Develop separate marketing for classic and electric bikes, promoting unique features.
* Adjust pricing plans to incentivize annual membership.
* Expand marketing efforts during summer and promote leisure activities.
* Develop partnerships with local businesses for exclusive discounts.
* Collect more data on customer demographics and preferences.

Next steps for the team and stakeholders could include:

* Implement recommendations in targeted marketing campaign to convert casual riders to annual members
* Monitor impact of campaign through metrics such as annual membership sign-ups, bike usage rates, and revenue generated
* Collect and analyze customer data to inform future marketing strategies and pricing plans.

Additional data that could be useful in expanding on the findings includes:

* Customer feedback and satisfaction surveys to understand their preferences and factors influencing their decisions.
* Data on customer demographics and location to better segment the customer base for targeted marketing.
* Data on external factors such as weather patterns and events to understand their impact on bike usage rates and customer behavior.
