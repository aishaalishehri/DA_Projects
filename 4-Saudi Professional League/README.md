# Employees Satisification Project

## Table Of Contents
- [Overview](#overview)
- [Images](#images)
- [Results](#results)

### Overview
The project involves analyzing data from the Saudi Professional League (SPL), a professional football league in Saudi Arabia. The analysis aims to gain insights into various aspects of the league, such as highest cost transfers, how the age or rating impact the average of the transfer and so on.
### Data Source
- The file: saudi-pro-league.csv
  
### Tools
- Python
  
### Data cleaning and prepration
1. import the libraries will be used in the analysis such as:
   - pandas
   - matplotlib.pyplot
   - numpy
2. Check for nulls values and manipulate it (Fee & Age columns). Fill it with the average
3. change fee column type to be numeric to do some mathematical ops by using lambda.
3. Split the season column to reach the 1st year only.
4.Create a new column to rate the transfer in ( low - mid - high).
5. Create sperate dfs to visualize them.

### Exploarty analysis
- Who are Top 5 player deals (In/Out)?
- How many deals the club did with the percentage for top 10 clubs.
- Top 5 clubs have did deals. & have more expensive deals.
- Total cost per year. & Total Cost based on Period per year
- Average price based on the rating. & Age & Position
- 
### Data Analysis
1. Create a new column to classify the position only to 4 categories to be able to calculate the average from this column thin fill it to each position related to the same category:
```python
#Define the conditions and corresponding values for the new column
conditions = [
    df['position'].isin(['Centre-Forward', 'Second Striker', 'Attack']),
    df['position'].isin(['Midfield', 'Attacking Midfield', 'Central Midfield', 
                         'Defensive Midfield', 'Left Midfield', 'Left Winger', 
                         'Right Midfield', 'Right Winger']),
    df['position'].isin(['Sweeper', 'Defence', 'Left-Back', 'Right-Back', 'Centre-Back']),
    df['position'] == 'Goalkeeper'
]
values = ['Forwards', 'Midfielders', 'Defenders', 'Goalkeeper']

#Create a new column 'position_category' based on the conditions
df['position_category'] = np.select(conditions, values, default=np.nan)

#Then fill fee nulls
Avg_Fees = df.groupby(['position_category']).agg(
    avg_fee=('fee', 'mean'),
).reset_index().round({'avg_fee': 0})

#2 to fill ages nulls
position_avg_fee = Avg_Fees.set_index('position_category')['avg_fee'].to_dict()

# Fill null values based on average fee for the same position
df['fee'] = df.apply(lambda row: position_avg_fee[row['position_category']] if pd.isnull(row['fee']) else row['fee'], axis=1)
```

2. Change type of fee column and remove any string by using Lambda Function them applied it on fee:
```python
re_fun = lambda x: pd.to_numeric(str(x).replace('€', '').replace('m', ''), errors='coerce')
#Apply the lambda function to the 'fee' column
df['fee'] = df['fee'].apply(re_fun)
```

3. Split the season column to reach the 1st year only:
```python
df['year'] = df['season'].apply(lambda x: x.split('/')[0])
```

4. Define the conditions and  ratings to create a new col = rating_deal:

```python
conditions = [
    (df['fee'] >= 0) & (df['fee'] < 10),
    (df['fee'] >= 10) & (df['fee'] < 35),
    (df['fee'] >= 35)
]

ratings = ['Low', 'Mid', 'High']
#Create the new col
df['rating_deal'] = np.select(conditions, ratings, default=np.nan)
```

5. One of the chart code:
```python
#Create a figure and axis object
fig, ax1 = plt.subplots(figsize=(12, 6))

#Plot the percentage as a line chart
ax1.bar(percent_df['club_name'], percent_df['num_deals'], color='green', label='Number of Deals')
ax1.set_ylabel('Number of deals', color='black')

#Reverse the order of the values for percentage
percent_df_reverse = percent_df.iloc[::-1]

#Create a secondary y-axis for num_deals as a clustered column chart
ax2 = ax1.twinx()
ax2.plot(percent_df_reverse['percentage'], marker='o', color='red', label='Percentage')
ax2.set_ylabel('Percentage', color='black')
ax2.set_xlabel('Club Name')
ax2.set_title('Number of Deals and its Percentage for each Club')

#Show legend
ax1.legend(loc='upper left')
ax2.legend(loc='upper center')

#Rotate x-axis labels & show
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```

### Images
- Who are the Top 5 player deals (In/Out)?
  ![image](https://github.com/aishaalishehri/DA_Projects/assets/145159903/7f0ce806-851e-4a3b-bac9-00ff5bb80a73)
  
- How many deals the club did with the percentage for top 10 clubs.
  ![image](https://github.com/aishaalishehri/DA_Projects/assets/145159903/1485401a-7fe5-42d5-90cd-70936e9b05de)

- Top 5 clubs have did deals. & have more expensive deals.
  ![image](https://github.com/aishaalishehri/DA_Projects/assets/145159903/e3bfd5ee-f217-4747-9f9a-e318ca9012b6)
  &
  ![image](https://github.com/aishaalishehri/DA_Projects/assets/145159903/7938cd95-80d0-4a6e-abd3-f38862ae34f3)

- Total cost per year. & Total Cost based on Period per year
  ![image](https://github.com/aishaalishehri/DA_Projects/assets/145159903/c11b6a59-6e51-4754-aa0c-e407150cb989)
  &
  ![image](https://github.com/aishaalishehri/DA_Projects/assets/145159903/f5f80314-8420-4ea5-b3e0-0938a60cd394)

- Average price based on the rating. & Average price based on Age.
  ![image](https://github.com/aishaalishehri/DA_Projects/assets/145159903/a972c8f6-de82-4b74-b531-5ea46ae5d1b2)
  &
  ![image](https://github.com/aishaalishehri/DA_Projects/assets/145159903/e8770d38-6137-4e9a-9425-2b4c6a9167c6)

- Average price based on Position? & Position_category to be in overall
  ![image](https://github.com/aishaalishehri/DA_Projects/assets/145159903/38900d15-2066-48bf-85f3-9fb5deea697b)
  &
  ![image](https://github.com/aishaalishehri/DA_Projects/assets/145159903/99737be3-c23a-483b-bdea-2cedc65e8fed)


### Results










  


    

