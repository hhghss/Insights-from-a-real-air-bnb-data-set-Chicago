# Insights-from-a-real-air-bnb-data-set-Chicago
## Python code for insights on air bnb booking. We are using Calendar and listing csv files

I have done all the calculations based on data from Chicago
![image](https://github.com/user-attachments/assets/706bd744-fe30-46b3-9c57-f3a5070b7501)

Chicago Calendar Data Analysis with Pandas
```
import pandas as pd
calendar = pd.read_csv('calendar.csv')
```
# Questions that you might want to address about the given data
Let`s dive into exciting insights!

## 1- Want to know the number of available and unavailable rooms
```
calendar.available.value_counts()
```
******
## 2- Purpose: Calculates the percentage of available (t) and unavailable (f) dates
* Explanation:
* value_counts(normalize=True) gives proportions.
* Multiplying by 100 converts the proportions into percentages
```
busiest_dates = calendar[calendar['available'] == 'f']['date'].value_counts()
print("Busiest Dates:")
print(busiest_dates.head())
```

