# ALUNING_RYA_2A_PA4
This repository includes Python programs that provide solutions to two (2) problems from Program Assignment 4: Data Wrangling and Data Visualization.

---
## PROBLEM 1
**Problem:** Create the following data frames based on the format provided: Example: Vis = [“Name”, “Gender”, “Track”, “Math<70”]; hometown is constant as Visayas <br>
a. Filename: Instru = [“Name”, “GEAS”, “Electronics >70”]; where track is constant as Instrumentation and hometown Luzon <br>
**Code Process:**
1. The program creates a new DataFrame Instru by filtering the board DataFrame with multiple conditions:
The value of Track must be Instrumentation.

The value of Hometown must be Luzon.

The value of Electronics must be greater than 70.

After applying these filters using the & operator, only the columns Name, GEAS, and Electronics are selected.
The resulting subset is stored in the DataFrame Instru.

To improve clarity, the program renames the Electronics column to Electronics >70.
Finally, the Instru DataFrame is displayed, showing the filtered results.
