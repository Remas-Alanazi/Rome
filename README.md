# Rome
Python code for insights on dirbnb booking of Rome we are using calendar and listing CSV files
Please find the link attached for downloading the calendar file
https://data.insideairbnb.com/italy/lazio/rome/2024-09-11/data/calendar.csv.gz

 I have done all the calculations based on data from Rome
 
 <img src= "https://github.com/user-attachments/assets/e36d9f51-5210-4d91-88fb-c7d9a7683abf" alt="Value Counts Output" width="500"/>

```python
import pandas as pd
calendar = pd.read_csv('calendar.csv')
```

# 1 Want to know the number of available and unavailable rooms
```python
calendar.available.value_counts()
```
<img src= "https://github.com/user-attachments/assets/dcfbca5f-97fe-43e5-bae3-97d4d1b493fa" alt="Value Counts Output" width="300"/>

# 2 Purpose: Calculates the percentage of available (t) and unavailable (f) dates.

Explanation:
value_counts(normalize=True) gives proportions.
Multiplying by 100 converts the proportions into percentages

```python
availability_percentage = calendar['available'].value_counts(normalize=True) * 100
availability_percentage
```
# 3 Let`s Count the busiest day! 🚩
 Hint: We will be counting the most unavailable days (given by f)
```python
busiest_dates = calendar[calendar['available'] == 'f']['date'].value_counts()
print("Busiest Dates:")
print(busiest_dates.head())
```
# 4 Plot a bar graph to show availability percentage

```python
import matplotlib.pyplot as plt
availability_percentage.plot(kind='bar', color=['pink', 'hotpink'])
plt.title('Availability Percentages')
plt.ylabel('Percentage')
plt.xlabel('Available (t/f)')
plt.show()
```
<img src= "https://github.com/user-attachments/assets/06db87ed-b17d-48ff-a2b3-0c8f31edfd63" alt="Value Counts Output" width="500"/>

# 5 Plot the busiest day
```python
busiest_dates.head(10).plot(kind='bar', color='darkblue')
plt.title('Top 10 Busiest Dates')
plt.ylabel('Number of Listings Unavailable')
plt.xlabel('Date')
plt.show()
```
<img src= "https://github.com/user-attachments/assets/50ca3230-f314-4fcd-83b2-62aae6b64a6e" alt="Value Counts Output" width="500"/>

📄 Download listings dataset of Rome from
https://data.insideairbnb.com/italy/lazio/rome/2024-09-11/visualisations/listings.csv

```python
import pandas as pd
listings = pd.read_csv('/Users/remassaud/Desktop/listings.csv')
listings
```
<img src= "https://github.com/user-attachments/assets/7b6915e9-d59e-4f1e-b71d-7361f606891a" width="500"/>

```python
listings.columns
```
<img src= "https://github.com/user-attachments/assets/786baa46-09f6-4274-b70f-0e9bb7da425d" alt="Value Counts Output" width="500"/>

# ✅ Room type and price is given seperately

```python
import matplotlib.pyplot as plt
price_by_room = listings.groupby('room_type')['price'].mean()
print(price_by_room)

# Plot price by room type
price_by_room.plot(kind='bar', color='blue')
plt.title('Average Price by Room Type')
plt.ylabel('Average Price')
plt.xlabel('Room Type')

plt.show()
```
<img src= "https://github.com/user-attachments/assets/094878df-a17b-4b20-85c2-638711310d4e" alt="Value Counts Output" width="500"/>

# ✅ Which are the top 10 neighborhoods with the most listings?

```python
neighborhood_counts = listings['neighbourhood'].value_counts().head(10)
print("Top 10 Neighborhoods by Listings:")
print(neighborhood_counts)

# Plot neighborhoods with most listings
neighborhood_counts.plot(kind='bar', color='lightcoral')
plt.title('Top 10 Neighborhoods by Listings')
plt.ylabel('Number of Listings')
plt.xlabel('Neighborhood')
plt.xticks(rotation=90)
plt.show()
```
<img src= "https://github.com/user-attachments/assets/57c3c163-262b-4051-89ba-a4ea623e202f" alt="Value Counts Output" width="500"/>

# ✅ Geographical Distribution of Listings (Price Colored)
```python
import matplotlib.pyplot as plt
import seaborn as sns
```
```python
plt.figure(figsize=(10, 6))
sns.scatterplot(data=listings, x='longitude', y='latitude', hue='price', palette='viridis', size='price', sizes=(10, 200))
plt.title('Geographical Distribution of Listings (Price Colored)')
plt.xlabel('Longitude')
plt.ylabel('Latitude')
plt.show()
```
<img src= "https://github.com/user-attachments/assets/f24af508-d358-4c9a-b08a-3e9b1627a5ce" alt="Value Counts Output" width="500"/>

## Let us see the listings on a real map


```python
import folium
from folium.plugins import HeatMap
import pandas as pd


Rome_data = listings[['latitude', 'longitude', 'price']]  # Example, you may add more columns

# Create a base map centered around Rome
m = folium.Map(location=[41.89631237400846, 12.470023058100534], zoom_start=10)

# Prepare the data for the heatmap
heat_data = [[row['latitude'], row['longitude']] for index, row in Rome_data.iterrows()]

# Add the heatmap to the map
HeatMap(heat_data).add_to(m)

# Save the map as an HTML file to view in a browser
m.save('Rome_heatmap.html')

m
```
<img src= "https://github.com/user-attachments/assets/40e1167b-98ef-4c38-9bcc-b0fae00422b2" alt="Value Counts Output" width="600"/>








