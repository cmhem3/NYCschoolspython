# NYC School Test Scores
DataCamp Project: Exploring NYC Public School Test Result Scores using python

![image](https://github.com/user-attachments/assets/ba753c3b-a439-41e3-acdf-b6e20efb7fa0)
Photo by Jannis Lucas on Unsplash.

Every year, American high school students take SATs, which are standardized tests intended to measure literacy, numeracy, and writing skills. There are three sections - reading, math, and writing, each with a maximum score of 800 points. These tests are extremely important for students and colleges, as they play a pivotal role in the admissions process.

Analyzing the performance of schools is important for a variety of stakeholders, including policy and education professionals, researchers, government, and even parents considering which school their children should attend.

You have been provided with a dataset called schools.csv, which is previewed below.

You have been tasked with answering three key questions about New York City (NYC) public school SAT performance.

# Install necessary packages
import pandas as pd

# Read in the data
schools = pd.read_csv("schools.csv")

# Preview the data
schools.head()
![image](https://github.com/user-attachments/assets/18202d32-2acb-488e-a6c4-64e69d6df6c1)
![image](https://github.com/user-attachments/assets/33bb4fdc-bc87-4ca2-b623-5d936566663d)

1) Which NYC schools have the best math results?
- The best math results are at least 80% of the *maximum possible score of 800* for math.
- Save your results in a pandas DataFrame called best_math_schools, including "school_name" and "average_math" columns, sorted by "average_math" in descending order.

#1) BEST MATH SCHOOLS:
###a) Calculate the threshold: 

  -threshold = 800 * 0.8

### Step 2: Filter the DataFrame
    #Next, filter the `schools` DataFrame to include only those schools where the `average_math` score meets or exceeds the threshold:

  -best_math_schools = schools[schools['average_math'] >= threshold]

### Step 3: Select Relevant Columns and Sort
    #Now, select only the `school_name` and `average_math` columns, and sort the schools by `average_math` in descending order:

  -best_math_schools = best_math_schools[['school_name', 'average_math']].sort_values(by='average_math', ascending=False)
    
  -print(best_math_schools)
