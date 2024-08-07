# Plant Co Performance Dashboard

> This project is about building a Power BI dashboard that will show a hypothetical plant company's financial performance across multiple years.

## Overview

The aim of this project is to illustrate the process of building a Power BI dashboard, including steps such as data cleaning, modelling (DAX), building data visualisations, and formatting.

## The Dataset

Here are snapshots of the tables that I worked with in this project:

Sales (Fact Table)

<img width="508" alt="Screenshot 2024-07-14 at 09 41 47" src="https://github.com/user-attachments/assets/1daaedcc-af7a-4043-b6a9-662e420cc76c">


Accounts (Dimension Table)

<img width="641" alt="Screenshot 2024-07-14 at 09 42 08" src="https://github.com/user-attachments/assets/a10297ba-e591-42ed-b20d-f940e81a43fa">


Products (Dimension Table)

<img width="917" alt="Screenshot 2024-07-14 at 09 42 16" src="https://github.com/user-attachments/assets/ddf1220e-2313-419e-8b74-f24252a4dd5c">

## Cleaning the Data

I imported the Excel file into Power BI and decided to transform the data using the Power Query tool. What I particularly liked about this tool is that it keeps a record of all the changes made within it for each table, which is beneficial because you can delete certain changes if you wish. The transformations I made included renaming columns such as *latitude2* and *country2* for easier readability, removing duplicates and null values, and formatting the numeric data by adjusting the number of decimal places.

## Modelling the Data

Next, I used DAX to build all the measures I needed to create the dashboard. Firstly, I created a date table called *Dim_Date*, which contains dates spanning the entirety of the time period that the sales data covers. Doing this allows for straightforward implementation of time intelligence functions in Power BI such as `TOTALYTD()` and `SAMEPERIODLASTYEAR()`, and also supports constant date filtering and grouping.

I also created a table called *Slc_Values*, which I would later use to create SWITCH measures, extremely helpful for building slicers.

The next thing to do was build the key measures (Sales, Gross Profit, Quantity) that I would be using within both the SWITCH and Prior Year-To-Date (PYTD) measures, which I did within a *_Measures* table. Once these were built, I created the PYTD and YTD measures using the key measures already created.

Examples of both of these types of measures can be seen below:

<img width="360" alt="Screenshot 2024-07-15 at 21 34 11" src="https://github.com/user-attachments/assets/27041e75-2582-4485-83d9-0ede35d36c4c">

<img width="468" alt="Screenshot 2024-07-15 at 21 54 30" src="https://github.com/user-attachments/assets/3e0dc802-854f-4cd4-80eb-bac5737c2a93">


I then built SWITCH measures for both the YTD and PYTD data. Screenshots of them can be seen below:

<img width="316" alt="Screenshot 2024-07-15 at 22 05 26" src="https://github.com/user-attachments/assets/06d62318-1965-4262-8e5d-f3d77e5780db">

<img width="579" alt="Screenshot 2024-07-16 at 22 57 38" src="https://github.com/user-attachments/assets/c5583d65-ad11-48ab-8ccc-eee3ad54bc1f">


I also created a measure called *YTD vs PYTD*, which subtracts the PYTD measure from the YTD measure in question, e.g. YTD_Sales - PYTD_Sales.

One more thing I did was establish the relationships between the different tables inside *Model View*. The result can be seen below (1 represents One and * represents Many):

<img width="579" alt="Screenshot 2024-07-16 at 22 45 21" src="https://github.com/user-attachments/assets/059bc9b7-24a6-41f8-a966-305295e60e81">

## Building the Core Visuals

Now it was time to begin building the visuals that would make up the dashboard. I chose a combination of slicers and cards for the header metrics. Below, I used a treemap, as it makes efficient use of space, and a waterfall chart, as it allows you to visualise both positive and negative growth, which is important in this context due to the regular comparisons made between YTD and PYTD performance. Additionally, I included a line and stacked column chart due to its ability to visualise two related metrics simultaneously—in this case, YTD and PYTD performance. An example can be seen below:

<img width="634" alt="Screenshot 2024-07-17 at 14 29 24" src="https://github.com/user-attachments/assets/696c6571-31a6-46a8-bf2f-feb686fbc20c">

I also created a new measure called *GP%*, which gives the Gross Profit as a percentage of Sales, and added it to the card alongside *YTD*, *YTD vs PYTD*, and *PYTD*.

## Formatting and Conditional Formatting

After creating the core visuals, I began formatting them. Before anything though, I changed the theme to the built-in Storm theme.

Starting with the Performance Metrics slicer, I changed the colour of the buttons when not selected to light grey and added accent bars to them to give separation. I also adjusted the padding size to narrow, and changed the colour of the buttons when selected to dark grey, and the colour when hovering over a button to mild blue.

Moving onto the card, I initially changed the text colour to grey. I then added conditional formatting separately to the text and background of the *YTD vs PYTD* tile. The criteria for both respectively can be seen below:

<img width="906" alt="Screenshot 2024-07-17 at 17 13 26" src="https://github.com/user-attachments/assets/f32009a6-436c-4274-9b90-8569da4923c1">

<img width="906" alt="Screenshot 2024-07-17 at 17 13 35" src="https://github.com/user-attachments/assets/df370490-8ad9-4b54-9740-e39a9ba9ae77">

I then removed the borders and changed the shape of the tiles to rounded rectangles.

## Formatting the Treemap, Waterfall Chart, and Line and Stacked Column Chart

Starting with the treemap, I opted for the values to be based on *YTD vs PYTD* and adjusted the filter to show only the bottom 10 countries based on this metric, before finally adding data labels to provide clarity.

Moving onto the waterfall chart, I added data labels, a legend, as well as adding Product_Type and Product_Name to the category list, enabling us to drill down and find out more about the performance of plant types and specific plants that fall under each of those types in each country. Below you can see the sales data for all the outdoor plants sold to China in February 2024:

<img width="301" alt="Screenshot 2024-07-17 at 18 08 51" src="https://github.com/user-attachments/assets/c9d378c1-7bdb-479f-8c06-eb06e667df55">

<img width="301" alt="Screenshot 2024-07-17 at 18 09 18" src="https://github.com/user-attachments/assets/5cd2bd99-41eb-4c89-a731-41f9c0ca3bf1">

<img width="301" alt="Screenshot 2024-07-17 at 18 09 36" src="https://github.com/user-attachments/assets/25bced59-2e0e-4076-8f5b-303c5140e13b">

<img width="301" alt="Screenshot 2024-07-17 at 18 09 47" src="https://github.com/user-attachments/assets/e0ff38b6-be2d-40f4-b45d-dc81a67d218b">

With the line and stacked column chart, I changed the colour of the line to red to distinguish it from the column colour and added markers for easier visibility, in addition to adding data labels to the line for better readability. I also added a legend to distinguish between the different product types. An example for 2024 can be seen below:

<img width="314" alt="Screenshot 2024-07-17 at 18 50 07" src="https://github.com/user-attachments/assets/11d82b4b-9b3c-45fa-9ffa-21aec07a5d73">

The next thing I did was create a scatter chart with a zoom slider that would compare all companies' GP% with any of the three key metrics (Sales, Quantity, Gross Profit). I added average lines for both the X and Y axes to add more detail. An example of company sales for 2024 can be seen below:

<img width="314" alt="Screenshot 2024-07-17 at 18 46 52" src="https://github.com/user-attachments/assets/4718e2f6-db0f-4a25-b067-7d0b2fbaee01">

## Tidying Up the Dashboard

I created dynamic chart titles for the waterfall, column, and scatter charts. The measures built to create these titles, as well as the final result, can be seen below:

<img width="699" alt="Screenshot 2024-07-17 at 19 40 46" src="https://github.com/user-attachments/assets/638d4dc2-1658-4fd8-9cd2-f3309731f7c5">

<img width="699" alt="Screenshot 2024-07-17 at 19 40 58" src="https://github.com/user-attachments/assets/d9820ab4-23ec-4440-984c-f932a96878f6">

<img width="711" alt="Screenshot 2024-07-17 at 19 41 08" src="https://github.com/user-attachments/assets/65ac143b-5657-44d9-801c-c3d01205981b">

<img width="587" alt="Screenshot 2024-07-17 at 19 42 41" src="https://github.com/user-attachments/assets/834e3e12-9ad6-4970-8cba-be621d52da42">

I also created the report title using the same concept as that shown in the measure screenshots above. This can be seen below:

<img width="808" alt="Screenshot 2024-07-17 at 19 53 08" src="https://github.com/user-attachments/assets/1f22236f-4c19-4cf1-bcef-ee2969130ad4">

The last thing I did was filter out 2022 from the YTD slicer, as there is no PYTD data for 2021 in the dataset to make comparisons with, leaving only 2023 and 2024.

## Final Result

<img width="747" alt="Screenshot 2024-07-17 at 20 05 18" src="https://github.com/user-attachments/assets/16e2f4ec-1afc-4472-b306-7ae1cfb31934">

<img width="747" alt="Screenshot 2024-07-17 at 20 05 32" src="https://github.com/user-attachments/assets/29d1653b-f1e2-4d3d-bdca-3cf0e1af563c">

<img width="747" alt="Screenshot 2024-07-17 at 20 05 43" src="https://github.com/user-attachments/assets/34b563e2-d202-4382-8649-66ff6b94c10c">