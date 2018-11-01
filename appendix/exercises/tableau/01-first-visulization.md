# \#01 - First Visulization

{% hint style="info" %}
Before you start this exercise, you need to download and install Tableau Desktop. You can download it [here](https://www.tableau.com/tft/activation), please ask me for a student license key. Alternatively, you can apply for your own free student key [here](https://www.tableau.com/de-de/academic/students).
{% endhint %}

## 1. Get the data

Tableau requires a structured dataset with atomic values in columns and records in rows. In this exercise, we're going to create a map visualization that gives a quick overview of all incidents of prostitution in chicago in the year 2018. There are two ways to get the dataset:

1. [Download](https://s3.amazonaws.com/nicolas.meseth/data+sets/crimes/crimes_chicago_2018.csv) the full crimes data set for 2018
2. Extract only the prostitution data using SQL and Databricks and download it as a CSV file

In this exercise, we assume you use the second option, so you have a pre-filtered data set with only prostitution incidents. Make sure you select at least the following information in your SQL extract:

* Date
* Block
* Location Description
* Description
* Longitude
* Latitude

## 2. Load the data in Tableau

Load the locally saved `.csv` file in Tableau. Check the column's detected data types and correct them if necessary. Create a new Tableau worksheet based on that data.

## 3.  Create a map visualization

Tableau is a leading visualization tool, but one great strength is how easy you can create map visualization if you have geo-related data. Create a map of Chicago and visualize the prostitution incidents:

1. Show all incidents a red dots on the map
2. Format the map so that it shows the street names. Make the map look darker, so that the red dots are better visible.
3. Group the dots by `block` and change the size of a dot depending on the number of incidents on that block.
4. Additionally, show blocks with many incidents in a darker red, and blocks with fewer incidents in orange.
5. Allow the incidents to be filtered by date. Present the control of the filter as a slider.
6. Now change the color of the dots so that each incident description is shown in a different color.
7. Finally, add a label to each dot to show the location description on the map.

## 4. Create a new field for the street

We would like to know which streets are hot spots for prostitution. Unfortunately, we don't have the street as a field in our data. However, the `block` field contains the street, and we can extract the street from there:

1. Create a new field `street` that contains the street name of the incident.
2. Update the map to group the data by street \(and not by block as before\).

## 5. Create a bar chart for the incidents per street

The map is nice to quickly see patterns related to the locations of the prostitution incidents. If we want to compare numbers, other charts are better suited. Let's create an analysis based on the new `street` field, and compare the absolute number of incidents on each street in a bar chart:

1. Create a bar chart and order the chart by number of incidents
2. Show the values as percentage of the total number
3. Change the bars to stacked bars that also show the location description in different colors.

## 6. Export the data and chart

You want to send the results of the prostitution by street analysis to a colleague, who doesn't have a Tableau license. Export the data to Excel and save the chart as an image file.

