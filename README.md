# ALUNING_RYA_2A_PA4
This repository includes Python programs that provide solutions to three (3) problems from Program Assignment 4: Data Wrangling and Data Visualization.

---
## PROBLEM 1
**Problem:** Create the following data frames based on the format provided: Filename: Instru = [“Name”, “GEAS”, “Electronics >70”]; where track is constant as Instrumentation and hometown Luzon <br>

**Code Process:** <br>
To solve this problem, the pandas library was first imported since it provides functions to manipulate tabular data. The dataset board2.csv was then loaded into a DataFrame named board to allow filtering and selection of specific data.
```Python
#Import pandas from the library
import pandas as pd

#Load and Call the dataset
board = pd.read_csv('board2.csv')
board
```
To extract only the students who satisfied the conditions, the .loc[] method was used. This method allows row filtering with multiple conditions and column selection at the same time. The conditions applied were:
* board['Track'] == 'Instrumentation' → limits results to Instrumentation track.
* board['Hometown'] == 'Luzon' → includes only students from Luzon.
* board['Electronics'] > 70 → ensures Electronics score is greater than 70. <br>
After applying these filters, only the columns Name, GEAS, and Electronics were displayed.
```Python
# Select students with: a.) Track = Instrumentation; b.) Hometown = Luzon; c.) Electronics > 70; Show only the columns Name, GEAS, and Electronics
Instru = board.loc[(board['Track'] == 'Instrumentation') &
                   (board['Hometown'] == 'Luzon') &
                   (board['Electronics']>70),
                   ['Name', 'GEAS', 'Electronics']]
```
The problem required that the column "Electronics" be renamed to "Electronics >70". The .rename() function was used for this purpose, ensuring the final DataFrame followed the specified format.
```Python
#Rename the Electronics column to Electronics >70 for clarity
Instru = Instru.rename(columns={'Electronics': 'Electronics >70'})

Instru
```

## PROBLEM 2
**Problem:** Filename: Mindy = [ “Name”, “Track”, “Electronics”, “Average >=55”]; where hometown is
constant as Mindanao and gender Female <br>

**Code Process:** <br>
The first step was to create a new column named "Average". The .mean(axis=1) function was used to compute the row-wise mean across the four subjects: Math, GEAS, Electronics, and Communication. The parameter axis=1 ensures the average is calculated across columns for each student.
```Python
#Add a new column "Average". This computes the mean score of Math, GEAS, Electronics, and Communication
#axis=1 ensures the average is taken across columns (row-wise)
board['Average'] = board[['Math', 'GEAS', 'Electronics', 'Communication']].mean(axis=1)
board['Average'] = board[['Math', 'GEAS', 'Electronics','Communication']].mean(axis=1)
board
```
Next, the .loc[] method was applied to filter students who satisfied all the following conditions:
* board['Gender'] == 'Female' → includes only female students.
* board['Hometown'] == 'Mindanao' → limits results to those from Mindanao.
* board['Average'] >= 55 → ensures only students with an average score of 55 or higher are included.
Only the columns Name, Track, Electronics, and Average were selected for display.
```Python
#Select students with: a.) Gender = Female; b.) Hometown = Mindanao; c.) Average >= 55; Show only the columns Name, Track, Electronics, and Average
Mindy = board.loc[(board['Gender'] == 'Female') & 
                    (board['Hometown'] == 'Mindanao') & 
                    (board['Average'] >= 55), 
                    ['Name', 'Track', 'Electronics', 'Average']]
```
Finally, the "Average" column was renamed to "Average >=55" for clarity, using the .rename() function. This ensured that the output DataFrame clearly indicated the condition applied to the average score.
```Python
# Rename the Average column to "Average >=55" for clarity
Mindy = Mindy.rename(columns={'Average': 'Average >=55'})

Mindy
```

## PROBLEM 3
**Problem:** Create a visualization that shows how the different features contribute to the average grade. Determine whether the chosen track in college, gender, or hometown contributes to a higher average score. <br>

**Code Process:** <br>
For this problem, the matplotlib library was used because it is one of the most widely used visualization libraries in Python. Specifically, the submodule pyplot was imported as plt. In this problem, matplotlib.pyplot was needed because the results of the grouped averages had to be visualized.
```Python
import matplotlib.pyplot as plt
```
The DataFrame was grouped by Track, and the mean of the Average column was calculated. A bar chart was then created using plot(kind="bar"). This type of visualization was chosen because it makes categorical comparisons clearer than raw numbers.
```Python
#Group the DataFrame by Track and calculate the mean Average score
track_avg = board.groupby('Track')['Average'].mean()

#Plot a bar graph for average scores by Track
plt.figure(figsize=(8,5))
track_avg.plot(kind="bar")
plt.title('Average Scores by Track')
plt.ylabel('Average Score')
plt.xlabel('Track')
plt.xticks(rotation=-25)  #rotate labels for readability
plt.show()
```
The same approach was applied to Gender. By grouping the DataFrame according to Gender and plotting the mean Average values, the chart allowed an easy comparison of male and female performance.
```Python
#Group the DataFrame by Gender and calculate the mean Average score
track_avg = board.groupby('Gender')['Average'].mean()

#Plot a bar graph for average scores by Gender
plt.figure(figsize=(8,5))
track_avg.plot(kind="bar")
plt.title('Average Scores by Gender')
plt.ylabel('Average score')
plt.xlabel('Gender')
plt.xticks(rotation=-25)
plt.show()
```
Finally, the same steps were applied to Hometown. Grouping the data by this feature made it possible to compare the average scores of students from Luzon, Visayas, and Mindanao. The bar chart highlighted differences between the groups in a visual way that would not be as obvious in a table.
```Python
#Group the DataFrame by Hometown and calculate the mean Average score
track_avg = board.groupby('Hometown')['Average'].mean()

#Plot a bar graph for average scores by Hometown
plt.figure(figsize=(8,5))
track_avg.plot(kind="bar")
plt.title('Average Scores by Hometown')
plt.ylabel('Average score')
plt.xlabel('Hometown')
plt.xticks(rotation=-25)
plt.show()
```
*Version 2*
