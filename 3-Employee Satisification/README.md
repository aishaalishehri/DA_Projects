# Employees Satisification Project

## Table Of Contents
- [Overview](#overview)
- [Results](#results)

### Overview
It's a small project  contain a small data. Trying to determine if the employees are satisified depending on some factors,
which analysis languages they prefer, average salary based on position.

### Data Source
- The file: Survey.xlsx
  
### Tools
- Power BI - Data cleaning, transforming, visualizing.

### Data cleaning and prepration
1. install all datasets and manipualte it
2. Transforming data
3. Dealing with missing values
4. Data cleaning to ensure.

### Exploarty analysis
- Is the position affect on the annual salary?
- Which languages are preferred based on position?
- How much they are satisified out of 10?
- 
### Data Analysis
1. Split columns with dropdwon by demilter to avoid Other option to reduce the respones number. Same with countries and data languages.
2. Split the salary column twice to make this synatx 0-10 the 0 in one column and the 10 in other to take the average.
3. Conditional Average column:
   ```DAX
   = Table.AddColumn(#"Changed Type4", "Average Salary ", each ([#"Q3 - Current Yearly Salary (in USD) - Copy.1"] + [#"Q3 - Current Yearly Salary (in USD) - Copy.2"]) / 2)
   ```

### Results 
1. Most of who took this survey and give us this bad impression are Adults.
2. Data positions made more money.
3. Python is the winner! and Java is dead.
4. Female make more money 🕶️!
5. The average rate for all factors is 5 out 10! Baaaaaad news 🆘

