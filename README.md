# Insights-from-a-real-air-bnb-data-set-Chicago
## Python code for insights on air bnb booking. We are using Calendar and listing csv files

I have done all the calculations based on data from Chicago
![image](https://github.com/user-attachments/assets/706bd744-fe30-46b3-9c57-f3a5070b7501)
******
# Calendar dataset of Chicago
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
![image](https://github.com/user-attachments/assets/054ae69c-9f9b-4bac-9b65-785877d80da9)

f (false) means not available, t(true) means available

## 2- Purpose: Calculates the percentage of available (t) and unavailable (f) dates
* Explanation:
* value_counts(normalize=True) gives proportions.
* Multiplying by 100 converts the proportions into percentages
```
busiest_dates = calendar[calendar['available'] == 'f']['date'].value_counts()
print("Busiest Dates:")
print(busiest_dates.head())
```

## 3- Count the busiest day
We will be counting the most unavailable days (given by f)
```
busiest_dates = calendar[calendar['available'] == 'f']['date'].value_counts()
print("Busiest Dates:")
print(busiest_dates.head())
```

## 4- Plot a bar graph to show availability percentage
```
import matplotlib.pyplot as plt
availability_percentage.plot(kind='bar', color=['darkgreen', 'darkred'])
plt.title('Availability Percentages')
plt.ylabel('Percentage')
plt.xlabel('Available (t/f)')
plt.show()
```
<img src="https://github.com/user-attachments/assets/4dd1e6ff-dd76-4acc-bb33-7f6f3e66a1a6" alt="Value Counts Output" width="600"/>

## 5- Plot the busiest day
```
busiest_dates.head(10).plot(kind='bar', color='rebeccapurple')
plt.title('Top 10 Busiest Dates')
plt.ylabel('Number of Listings Unavailable')
plt.xlabel('Date')
plt.show()
```
<img src="https://github.com/user-attachments/assets/d2a16f34-4438-4e6c-9432-758f19067d12" alt="Value Counts Output" width="600"/>

******
# Listings dataset of Chicago
```
import pandas as pd
listings = pd.read_csv('listings.csv')
```
## Listings columns
```
listings.columns
```
<img src="https://github.com/user-attachments/assets/b265ad4b-69a0-4770-8c35-467a999aa6cd" alt="Value Counts Output" width="600"/>

## Room type and price is given separately
Let`s Combine and visualize them
```
import matplotlib.pyplot as plt
price_by_room = listings.groupby('room_type')['price'].mean()
print(price_by_room)

# Plot price by room type
price_by_room.plot(kind='bar', color='indianred')
plt.title('Average Price by Room Type')
plt.ylabel('Average Price')
plt.xlabel('Room Type')

plt.show()
```
<img src="https://github.com/user-attachments/assets/dc883e9b-1b09-44e9-abf4-44b5fd6fae10" alt="Value Counts Output" width="600"/>

## The top 10 neighborhoods with the most listings
```
neighborhood_counts = listings['neighbourhood'].value_counts().head(10)
print("Top 10 Neighborhoods by Listings:")
print(neighborhood_counts)

# Plot neighborhoods with most listings
neighborhood_counts.plot(kind='bar', color='steelblue')
plt.title('Top 10 Neighborhoods by Listings')
plt.ylabel('Number of Listings')
plt.xlabel('Neighborhood')
plt.xticks(rotation=90)
plt.show()
```
<img src="https://github.com/user-attachments/assets/90ceec6c-fb76-4ea0-8929-ecb8fc439417" alt="Value Counts Output" width="600"/>

## Geographical Distribution of Listings (Price Colored)
```
import matplotlib.pyplot as plt
import seaborn as sns
```
```
plt.figure(figsize=(10, 6))
sns.scatterplot(data=listings, x='longitude', y='latitude', hue='price', palette='viridis', size='price', sizes=(10, 200))
plt.title('Geographical Distribution of Listings (Price Colored)')
plt.xlabel('Longitude')
plt.ylabel('Latitude')
plt.show()
```
<img src="https://github.com/user-attachments/assets/7841ac73-e344-4b13-81d4-c640dcc26e3e" alt="Value Counts Output" width="600"/>


## The listings on a real map
* Hot Colors (Red/Yellow): Indicate high-density areas, typically popular locations like tourist attractions, central neighborhoods, or high-demand zones.
* Cold Colors (Green/Blue): Represent low-density areas, which may be less popular, more affordable, or farther from key attractions.
* Patterns: Clustered heat spots highlight high-demand regions, while uniform spreads suggest balanced listing distribution.
```
import folium
from folium.plugins import HeatMap
import pandas as pd


hawaii_data = listings[['latitude', 'longitude', 'price']]  # Example, you may add more columns

# Create a base map centered around Chicago
m = folium.Map(location=[41.87914772760063, -87.62761455072854], zoom_start=10)

# Prepare the data for the heatmap
heat_data = [[row['latitude'], row['longitude']] for index, row in hawaii_data.iterrows()]

# Add the heatmap to the map
HeatMap(heat_data).add_to(m)

# Save the map as an HTML file to view in a browser
m.save('hawaii_heatmap.html')

# If you're using Jupyter Notebook, you can display the map directly in the notebook:
m
```
<img src="https://github.com/user-attachments/assets/f271fec2-358d-4d8c-81aa-f64f56e970eb" alt="Value Counts Output" width="600"/>








