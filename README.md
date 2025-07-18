# Airbnb-Paris-Data-Analysis
Airbnb Paris data analysis project: exploring pricing trends, popular neighborhoods, and room types. Built with Python, Pandas, and Seaborn. Sample data for learning. Includes visualizations and basic insights.
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

sns.set(style="darkgrid")

# Sample Airbnb data with dates (check-in dates example)
data = {
    "neighbourhood": ["Marais", "Bastille", "Montmartre", "Marais", "Latin Quarter", "Bastille", "Montmartre", "Marais", "Latin Quarter", "Bastille"],
    "room_type": ["Entire home/apt", "Private room", "Entire home/apt", "Shared room", "Private room", "Entire home/apt", "Shared room", "Private room", "Entire home/apt", "Shared room"],
    "price": [120, 75, 200, 30, 90, 130, 45, 85, 150, 40],
    "date": ["2025-07-01", "2025-07-02", "2025-07-03", "2025-07-01", "2025-07-04", "2025-07-05", "2025-07-03", "2025-07-06", "2025-07-07", "2025-07-08"]
}

df = pd.DataFrame(data)

# Convert 'date' column to datetime type
df['date'] = pd.to_datetime(df['date'])

# Show first rows
print("Sample Airbnb data with dates:")
display(df.head())

# Price distribution
plt.figure(figsize=(10,5))
sns.histplot(df["price"], bins=10, kde=True)
plt.title("Airbnb Price Distribution in Paris")
plt.xlabel("Price (EUR)")
plt.ylabel("Count")
plt.show()

# Top 3 neighbourhoods by average price
top_neigh = df.groupby("neighbourhood")["price"].mean().sort_values(ascending=False).head(3)

plt.figure(figsize=(8,4))
top_neigh.plot(kind='bar', color='tomato')
plt.title("Top 3 Most Expensive Neighbourhoods in Paris")
plt.ylabel("Average Price (EUR)")
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

# Bonus: Price over time plot
plt.figure(figsize=(10,5))
sns.lineplot(data=df, x='date', y='price', hue='neighbourhood', marker="o")
plt.title("Price Trend Over Time by Neighbourhood")
plt.xlabel("Date")
plt.ylabel("Price (EUR)")
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
