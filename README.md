# ALUNING_RYA_2A_PA4
This repository includes Python programs that provide solutions to three (3) problems from Program Assignment 4: Data Wrangling and Data Visualization.

---
## PROBLEM 1
**Problem:** Create the following data frames based on the format provided: Example: Vis = [“Name”, “Gender”, “Track”, “Math<70”]; hometown is constant as Visayas <br>
a. Filename: Instru = [“Name”, “GEAS”, “Electronics >70”]; where track is constant as Instrumentation and hometown Luzon <br>
**Code Process:**
1. The program creates a new DataFrame Instru by filtering the board DataFrame with multiple conditions:
   * The value of Track must be Instrumentation.
   * The value of Hometown must be Luzon.
   * The value of Electronics must be greater than 70.
2. After applying these filters using the & operator, only the columns Name, GEAS, and Electronics are selected.
3. The resulting subset is stored in the DataFrame Instru.
4. To improve clarity, the program renames the Electronics column to Electronics >70.
5. Finally, the Instru DataFrame is displayed, showing the filtered results.

```Python
import pandas as pd

board = pd.read_csv('board2.csv')
board

Vis = board.loc[(board['Math'] <70) & (board['Hometown'] == 'Visayas'), 
                ['Name', 'Gender', 'Track', 'Math']]
Vis

Instru = board.loc[(board['Track'] == 'Instrumentation') &
                   (board['Hometown'] == 'Luzon') &
                   (board['Electronics']>70),
                   ['Name', 'GEAS', 'Electronics']]
Instru = Instru.rename(columns={'Electronics': 'Electronics >70'})
Instru
```

## PROBLEM 2
**Problem:** Filename: Mindy = [ “Name”, “Track”, “Electronics”, “Average >=55”]; where hometown is
constant as Mindanao and gender Female <br>
**Code Process:** 
1. The program filters the board DataFrame using conditions:
   * The value of Gender must be Female.
   * The value of Hometown must be Mindanao.
   * The value of Average must be greater than or equal to 55.
2. Only the columns Name, Track, Electronics, and Average are selected.
3. The filtered data is stored in the DataFrame Mindy.
4. To make the output more descriptive, the Average column is renamed to Average >=55.
5. The Mindy DataFrame is then displayed with the chosen conditions applied.

```Python
board['Average'] = board[['Math', 'GEAS', 'Electronics','Communication']].mean(axis=1)
board

Mindy = board.loc[(board['Gender'] == 'Female') & 
                    (board['Hometown'] == 'Mindanao') & 
                    (board['Average'] >= 55), 
                    ['Name', 'Track', 'Electronics', 'Average']]
Mindy = Mindy.rename(columns={'Average': 'Average >=55'})
Mindy
```

## PROBLEM 3
**Problem:** Create a visualization that shows how the different features contribute to the average grade. Determine whether the chosen track in college, gender, or hometown contributes to a higher average score. <br>
**Code Process:** 
1. The program begins by importing the matplotlib.pyplot library as plt.
2. It groups the board DataFrame by Track, calculating the mean of the Average column.
3. A bar graph is plotted to show the Average Scores by Track.
4. It then groups the board DataFrame by Gender, again computing the mean of the Average column.
5. A bar graph is plotted to show the Average Scores by Gender.
6. Lastly, it groups the board DataFrame by Hometown, calculating the mean of the Average column
7. A bar graph is plotted to show the Average Scores by Hometown.
8. Each visualization is displayed separately with proper titles, labels, and rotated x-axis ticks for readability.

```Python
import matplotlib.pyplot as plt

track_avg = board.groupby('Track')['Average'].mean()

plt.figure(figsize=(8,5))
track_avg.plot(kind="bar")
plt.title('Average Scores by Track')
plt.ylabel('Average Score')
plt.xlabel('Track')
plt.xticks(rotation=-25)
plt.show()

track_avg = board.groupby('Gender')['Average'].mean()

plt.figure(figsize=(8,5))
track_avg.plot(kind="bar")
plt.title('Average Scores by Gender')
plt.ylabel('Average score')
plt.xlabel('Gender')
plt.xticks(rotation=-25)
plt.show()

track_avg = board.groupby('Hometown')['Average'].mean()

plt.figure(figsize=(8,5))
track_avg.plot(kind="bar")
plt.title('Average Scores by Hometown')
plt.ylabel('Average score')
plt.xlabel('Hometown')
plt.xticks(rotation=-25)
plt.show()
```
