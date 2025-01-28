# Rome
Python code for insights on dirbnb booking of Rome we are using calendar and listing CSV files
Please find the link attached for downloading the calendar file
https://data.insideairbnb.com/italy/lazio/rome/2024-09-11/data/calendar.csv.gz

 I have done all the calculations based on data from Rome
![image](https://github.com/user-attachments/assets/e36d9f51-5210-4d91-88fb-c7d9a7683abf)
import pandas as pd
calendar = pd.read_csv('calendar.csv')

# 1 Want to know the number of available and unavailable rooms

calendar.available.value_counts()

![image](https://github.com/user-attachments/assets/dcfbca5f-97fe-43e5-bae3-97d4d1b493fa)

# 2 Purpose: Calculates the percentage of available (t) and unavailable (f) dates.

Explanation:
value_counts(normalize=True) gives proportions.
Multiplying by 100 converts the proportions into percentages

```
availability_percentage = calendar['available'].value_counts(normalize=True) * 100
availability_percentage
```
# 3 Let`s Count the busiest day! 🚩
 Hint: We will be counting the most unavailable days (given by f)
```
busiest_dates = calendar[calendar['available'] == 'f']['date'].value_counts()
print("Busiest Dates:")
print(busiest_dates.head())
```
# 4 Plot a bar graph to show availability percentage

```
import matplotlib.pyplot as plt
availability_percentage.plot(kind='bar', color=['pink', 'hotpink'])
plt.title('Availability Percentages')
plt.ylabel('Percentage')
plt.xlabel('Available (t/f)')
plt.show()
```
<img src= "https://github.com/user-attachments/assets/06db87ed-b17d-48ff-a2b3-0c8f31edfd63" alt="Value Counts Output" width="600"/>

# 5 Plot the busiest day
```
busiest_dates.head(10).plot(kind='bar', color='darkblue')
plt.title('Top 10 Busiest Dates')
plt.ylabel('Number of Listings Unavailable')
plt.xlabel('Date')
plt.show()
```
<img src= "https://github.com/user-attachments/assets/50ca3230-f314-4fcd-83b2-62aae6b64a6e" alt="Value Counts Output" width="600"/>
📄 Download listings dataset of Rome from
https://data.insideairbnb.com/italy/lazio/rome/2024-09-11/visualisations/listings.csv

```
import pandas as pd
listings = pd.read_csv('/Users/remassaud/Desktop/listings.csv')
listings
```
<img src= "https://github.com/user-attachments/assets/7b6915e9-d59e-4f1e-b71d-7361f606891a" width="600"/>

```
listings.columns
```
![image](https://github.com/user-attachments/assets/786baa46-09f6-4274-b70f-0e9bb7da425d)

# ✅ Room type and price is given seperately

```
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
![image](https://github.com/user-attachments/assets/094878df-a17b-4b20-85c2-638711310d4e)

# ✅ Which are the top 10 neighborhoods with the most listings?

```
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
![image](https://github.com/user-attachments/assets/57c3c163-262b-4051-89ba-a4ea623e202f)

# ✅ Geographical Distribution of Listings (Price Colored)







