

# Airline Data Analysis Using SQL

## Overview
This project focuses on analyzing airline data using SQL queries to gain insights into flight operations, delays, and passenger trends. The dataset includes flight records, airport information, and delay statistics to help understand patterns in airline performance.

## Dataset Description
The dataset consists of real-world airline operations data, including:
- Flight details such as airline, flight number, origin, and destination.
- Departure and arrival times.
- Delay reasons and durations.
- Passenger traffic and airline performance metrics.

## Technologies Used
- SQL (Structured Query Language)
- Jupyter Notebook
- SQLite / PostgreSQL / MySQL (depending on user preference)
- Pandas for data manipulation
- Matplotlib and Seaborn for data visualization

## Installation & Setup
1. Clone the repository:
   ```sh
   git clone https://github.com/yourusername/Airline_data_analysis.git
   ```
2. Install dependencies:
   ```sh
   pip install jupyter pandas sqlalchemy matplotlib seaborn
   ```
3. Run Jupyter Notebook:
   ```sh
   jupyter notebook
   ```
4. Open the `Airline_data_analysis_using_sql.ipynb` file.

## Project Structure
```
├── Airline_data_analysis_using_sql.ipynb  # Jupyter Notebook with SQL queries
├── dataset/                               # Folder containing dataset files
├── README.md                              # Project documentation
└── requirements.txt                       # List of dependencies
```

## Data Cleaning and Validation
- Removed missing or duplicate values to ensure data integrity.
- Standardized date and time formats for consistency.
- Validated airport codes and airline names against official records.
- Checked for anomalies in flight delay records and corrected inconsistencies.

### Data Cleaning Code Example:
```python
import pandas as pd
# Load dataset
flights = pd.read_csv('dataset/flights.csv')
# Remove duplicates
flights.drop_duplicates(inplace=True)
# Handle missing values
flights.dropna(subset=['departure_time', 'arrival_time'], inplace=True)
# Standardize date format
flights['date'] = pd.to_datetime(flights['date'])
```

## Data Analysis
- **Flight Delays:** Identified the factors contributing to delays, such as weather, air traffic, and operational issues.
- **Airline Performance:** Compared on-time performance across different airlines.
- **Passenger Trends:** Analyzed peak travel seasons and high-demand routes.
- **Airport Congestion:** Evaluated the busiest airports and their impact on scheduling.

### SQL Query Example:
```sql
SELECT airline, AVG(delay) AS avg_delay 
FROM flights 
GROUP BY airline 
ORDER BY avg_delay DESC;
```

## Data Visualization
### AirPlane Models with their ranges
sns.set_style('whitegrid')
fig,axes = plt.subplots(figsize=(12,8))
ax = sns.barplot(x='model',y='range', data=aircrafts_data, palette = 'Paired')
for container in ax.containers:
    ax.bar_label(container)
plt.title('AirPlane Models with their ranges')
plt.xticks(rotation=45)
plt.show()
![image](https://github.com/user-attachments/assets/1da59720-0ad8-4ebf-8058-ce32507901bc)

### Number of Tickets Booked on Each Date
tickets = pd.read_sql_query("""select * from tickets inner join bookings
                    on tickets.book_ref = bookings.book_ref""", conn)

tickets['book_date'] = pd.to_datetime(tickets['book_date'])
tickets['date'] = tickets['book_date'].dt.date
tickets_count = tickets.groupby('date')[['date']].count()
plt.figure(figsize=(18,6))
plt.plot(tickets_count.index, tickets_count['date'], color='green', scalex=True, marker = "*")
plt.title('Number of Tickets Booked on Each Date', fontsize=30)
plt.xlabel('Date', fontsize=20)
plt.ylabel('Number of Tickets', fontsize=20)
plt.grid('b')
plt.show()
![image](https://github.com/user-attachments/assets/038192af-c917-453c-8783-b526fb26f275)

### Bar Chart - Flight Delays per Airline
```python
import matplotlib.pyplot as plt
import seaborn as sns

# Plot bar chart of delays per airline
plt.figure(figsize=(10,5))
sns.barplot(x='airline', y='delay', data=flights)
plt.xlabel('Airline')
plt.ylabel('Average Delay (mins)')
plt.title('Average Flight Delay by Airline')
plt.xticks(rotation=45)
plt.show()
```

### Line Graph - Trends in Delays Over Time
```python
flights.groupby('date')['delay'].mean().plot(kind='line', figsize=(12,6), title='Average Flight Delay Over Time')
plt.xlabel('Date')
plt.ylabel('Average Delay (mins)')
plt.show()
```

### Heatmap - Delay Reasons vs. Time of Day
```python
import numpy as np
pivot_table = flights.pivot_table(values='delay', index='hour', columns='reason', aggfunc=np.mean)
sns.heatmap(pivot_table, cmap='coolwarm', annot=True)
plt.title('Heatmap of Delay Reasons by Hour of Day')
plt.show()
```

## Key Insights
- Analyzed the impact of weather and operational factors on flight delays.
- Identified the most and least punctual airlines.
- Examined seasonal flight trends and passenger travel patterns.
- Assessed airport congestion levels and their effect on flight schedules.

## Usage
Users can modify and execute the SQL queries in the notebook to explore airline trends further. Additional queries can be added to analyze specific performance metrics or operational issues. The visualizations provide a clearer understanding of trends and correlations in the dataset.

## Contributing
Contributions are welcome! Fork this repository and submit pull requests to improve queries, visualizations, or data analysis approaches.

## License
This project is licensed under the MIT License.





