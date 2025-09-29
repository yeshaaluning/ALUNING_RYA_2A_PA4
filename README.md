# ALUNING_RYA_2A_PA4
This repository includes Python programs that provide solutions to three (3) problems from Program Assignment 4: Data Wrangling and Data Visualization.

---

## PROBLEM 1

**Problem:** Create the following data frames based on the format provided:
Filename: `Instru = [“Name”, “GEAS”, “Electronics >70”]`; where track is constant as Instrumentation and hometown Luzon.

### Explanation

To solve this, the **pandas library** was imported first because it provides powerful tools for handling tabular data. The dataset `board2.csv` was then loaded into a DataFrame named `board`. This allows us to access, filter, and manipulate student records efficiently.

```python
#Import pandas from the library
import pandas as pd

#Load and call the dataset
board = pd.read_csv('board2.csv')
board
```

Next, the `.loc[]` method was used for filtering. This function enables us to select rows based on conditions while also specifying which columns to display. The conditions applied were:
* `board['Track'] == 'Instrumentation'` → only students from Instrumentation track.
* `board['Hometown'] == 'Luzon'` → only students from Luzon.
* `board['Electronics'] > 70` → only students with Electronics scores above 70.
After filtering, only the columns Name, GEAS, and Electronics were selected.

```python
#Select students with: 
#a.) Track = Instrumentation 
#b.) Hometown = Luzon 
#c.) Electronics > 70 
#Show only the columns Name, GEAS, and Electronics
Instru = board.loc[(board['Track'] == 'Instrumentation') &
                   (board['Hometown'] == 'Luzon') &
                   (board['Electronics'] > 70),
                   ['Name', 'GEAS', 'Electronics']]
```

Finally, the problem required renaming the "Electronics" column to "Electronics >70". The `.rename()` function was applied to make the DataFrame’s output match the specified format.

```python
#Rename the Electronics column to Electronics >70
Instru = Instru.rename(columns={'Electronics': 'Electronics >70'})

Instru
```

---

## PROBLEM 2

**Problem:** Filename: `Mindy = [“Name”, “Track”, “Electronics”, “Average >=55”]`; where hometown is constant as Mindanao and gender Female.

### Explanation

The first step was to compute an **Average score** for each student. Using `.mean(axis=1)`, the program calculated the row-wise mean across four subjects: Math, GEAS, Electronics, and Communication. The parameter `axis=1` ensures the function averages values across columns instead of down rows.

```python
#Add a new column "Average". 
#Computes the mean score of Math, GEAS, Electronics, and Communication
board['Average'] = board[['Math', 'GEAS', 'Electronics', 'Communication']].mean(axis=1)
board
```

After computing averages, `.loc[]` was applied to filter female students from Mindanao with an Average ≥ 55. This ensured only the qualified subset of students appeared in the new DataFrame. Selected columns included Name, Track, Electronics, and Average.

```python
#Select students with: 
#a.) Gender = Female 
#b.) Hometown = Mindanao 
#c.) Average >= 55 
#Show only the columns Name, Track, Electronics, and Average
Mindy = board.loc[(board['Gender'] == 'Female') & 
                  (board['Hometown'] == 'Mindanao') & 
                  (board['Average'] >= 55), 
                  ['Name', 'Track', 'Electronics', 'Average']]
```

Lastly, to make the DataFrame clearer, the "Average" column was renamed to "Average >=55" using `.rename()`. This explicitly shows that the filter condition was based on average scores greater than or equal to 55.

```python
#Rename the Average column to "Average >=55"
Mindy = Mindy.rename(columns={'Average': 'Average >=55'})

Mindy
```

---

## PROBLEM 3

**Problem:** Create a visualization that shows how the different features contribute to the average grade. Determine whether the chosen track in college, gender, or hometown contributes to a higher average score.

### Explanation

For visualization, the **matplotlib library** was used, particularly the `pyplot` submodule (`import matplotlib.pyplot as plt`). This is because tabular comparisons are more meaningful when shown graphically rather than in raw numbers.

```python
#Import matplotlib for visualization
import matplotlib.pyplot as plt
```

The DataFrame was first grouped by **Track**, and the mean of Average scores was calculated. A bar chart was plotted since bar graphs provide clear comparisons across categorical data.

```python
#Group by Track and calculate mean Average
track_avg = board.groupby('Track')['Average'].mean()

#Plot bar chart for average scores by Track
plt.figure(figsize=(8,5))
track_avg.plot(kind="bar")
plt.title('Average Scores by Track')
plt.ylabel('Average Score')
plt.xlabel('Track')
plt.xticks(rotation=-25)
plt.show()
```

The same procedure was repeated for **Gender**. Grouping by gender allows easy comparison of performance between male and female students.

```python
#Group by Gender and calculate mean Average
gender_avg = board.groupby('Gender')['Average'].mean()

#Plot bar chart for average scores by Gender
plt.figure(figsize=(8,5))
gender_avg.plot(kind="bar")
plt.title('Average Scores by Gender')
plt.ylabel('Average Score')
plt.xlabel('Gender')
plt.xticks(rotation=-25)
plt.show()
```

Finally, the grouping was done by **Hometown**, comparing Luzon, Visayas, and Mindanao. This visual approach highlights regional performance trends better than tables.

```python
#Group by Hometown and calculate mean Average
home_avg = board.groupby('Hometown')['Average'].mean()

# Plot bar chart for average scores by Hometown
plt.figure(figsize=(8,5))
home_avg.plot(kind="bar")
plt.title('Average Scores by Hometown')
plt.ylabel('Average Score')
plt.xlabel('Hometown')
plt.xticks(rotation=-25)
plt.show()
```

---

## Conclusion

Program Assignment 4 demonstrated how data wrangling and visualization can turn raw data into meaningful insights.

1. In **Problem 1**, conditional filtering and column renaming were used to create a specific DataFrame.
2. In **Problem 2**, calculating averages and filtering by multiple conditions showed how to extract valuable subsets.
3. In **Problem 3**, grouping and bar chart visualization made it easier to compare student performance across **Track, Gender, and Hometown**.

Overall, this assignment strengthened the use of pandas for data manipulation and matplotlib for visualization, essential tools in analyzing and presenting structured data.

---
*Version 2*
