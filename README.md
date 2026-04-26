Indego Bike Ridership As A Function of Average Temperature

Introduction

Indego is a bike-sharing service serving the Philadelphia area. The purpose of this project is to analyze bike usage as a function of local weather conditions. It is expected that bike usage will peak at average temperatures and decline at both hotter and colder temperatures, as such conditions would be less favorable to biking.

Data Sources

For the bike share data, Indego’s publicly available datasets for 2024 Q3, 2024 Q4, 2025 Q1, 2025 Q2, and 2025 Q3 were utilized. Weather data was sourced from the National Centers for Environmental Information, and data measuring temperatures from 8/01/2024 to 8/25/2025 at the Philadelphia International Airport was utilized.

Data Cleaning

The weather data was cleaned by applying a filter to the “DailyAverageDryBulbTemperature” column to highlight all rows with no data in that field, and then those rows were deleted. This resulted in a dataset with one temperature observation for each day between 8/01/2024 and 8/25/2025. Next, there was a duplicate column “REPORT_TYPE,” so the duplicate was deleted. No further data cleaning steps were required.

The bike share data was cleaned by applying a “SELECT DISTINCT” SQL Query and verifying that the resulting dataset had the same number of rows as the original dataset. It was determined that no further cleaning was required.

Data Processing

The Indego datasets for 2024 Q3, 2024 Q4, 2025 Q1, 2025 Q2, and 2025 Q3 were imported into a Google Colab notebook and concatenated into one dataframe using the pd.concat() function. Afterwards, using Boolean masking, data before 8/01/2024 and after 8/25/2025 was dropped from the concatenated data. The resulting dataframe was then exported as a new csv file, named as “Indego_trips_2024_2025.csv”. 

The cleaned weather data and Indego_trips_2024_2025.csv were then both imported into BigQuery datasets. Using the following SQL query, the bike ride data was first aggregated to show the total number of rides per date. The aggregated data was then merged with the weather data using an inner join, resulting in a dataset with the number of rides and average temperature for each date between 8/01/2024 and 8/25/2025. This dataset was then exported from BigQuery and saved as a csv.

SQL Query:


Data Visualization

Lastly, the csv file resulting from the above SQL Query was imported into Tableau and used to plot daily number of bike rides as a function of average temperature for each date between 8/01/2024 and 8/25/2025. This resulted in a graph which can be seen in the "Indego Project Report" file.

The trend line had the following values:

Avg. Num Rides = 57.5412*Avg. Daily Average Dry Bulb Temperature + 217.636
R-Squared: 0.635435
P-value: < 0.0001

Conclusion

The data visualization in Tableau demonstrates that despite expectations, average ridership increases as a function of temperature and does not decrease at hotter temperatures, resulting in a linear relationship. Further research could investigate ridership as a function of different weather conditions, such as rain or snow.
