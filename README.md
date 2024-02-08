# E-commerce sales analysis

## Table Of Contents
- [Overview](#overview)
- [Results](#results)
- [Images](#images)


### Overview
This project aims to provide a summary about E-commerce company customers. When they made a revenue by which browser, os, and etc. To help company know more about their customers to increase their revenue.

### Data Source
The company data are from these files: online_shoppers_intention.xlsx, Regions.xlsx, Browser.xlsx, and Operating Systems.xlsx

### Tools
- Excel - Data Cleaning and Analysis
- Power BI - Creating a dashboard and a report

### Data cleaning and prepration
1. install all datasets and manipualte it
2. Transforming data
3. Dealing with missing values
4. Data cleaning to ensure.

### Exploarty analysis
 - Most customer browsing from which browser, region and OS ?
 - The time average they take per page?
 - In which days of the week the made more revenue?

### Data Analysis
- Power BI Dax:
  - Adding a conditional column to know if the customer purches at the end of his session:
    ```DAX
    = Table.AddColumn(#"Changed Type", "MakeRevenue", each if [Revenue] = true then "Make Revenue " else "Don't Make Revenue")
    ```
  - Conditional column to know if its purches in the weekend or not:
      ```DAX
    = Table.AddColumn(#"Added Conditional Column", "In Weekend ?", each if [Weekend] = true then "On Weekend" else "Not Weekend")
    ```
  - And the same for a special days or NOT.

### Results 
1. The most real customers are using Android os.
2. For the browser most of them are using Chrome.
3. The most of active sessions end with revenue are in weekdays.

### Images 
![image](https://github.com/aishaalishehri/DA_Projects/assets/145159903/3588159d-35e2-4219-8b29-665682aea33a)

![image](https://github.com/aishaalishehri/DA_Projects/assets/145159903/89b1e275-dabf-4007-a88e-c5db6208c78b)

![image](https://github.com/aishaalishehri/DA_Projects/assets/145159903/68633476-c020-46f6-a78f-af3295b0069e)




