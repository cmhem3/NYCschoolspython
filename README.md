# NYC School Test Scores
DataCamp Project: Exploring NYC Public School Test Result Scores using python

![image](https://github.com/user-attachments/assets/ba753c3b-a439-41e3-acdf-b6e20efb7fa0)
Photo by Jannis Lucas on Unsplash.

(Side note: this project is part of DataCamp's intermediate Python course, to which the "Schools" dataset is not available.  I do however, post samples of this dataset as well as the code results)

Every year, American high school students take SATs, which are standardized tests intended to measure literacy, numeracy, and writing skills. There are three sections - reading, math, and writing, each with a maximum score of 800 points. These tests are extremely important for students and colleges, as they play a pivotal role in the admissions process.

Analyzing the performance of schools is important for a variety of stakeholders, including policy and education professionals, researchers, government, and even parents considering which school their children should attend.

You have been provided with a dataset called schools.csv, which is previewed below.

You have been tasked with answering three key questions about New York City (NYC) public school SAT performance.

### Python code is below
- This project includes the python code, along with the project questions and snipits of code results.
```python 
#Install necessary packages
import pandas as pd

#Read in the data
schools = pd.read_csv("schools.csv")

#Preview the data
schools.head()
```
![image](https://github.com/user-attachments/assets/a58ad293-6499-4678-8c88-f92ae8436137)
![image](https://github.com/user-attachments/assets/33bb4fdc-bc87-4ca2-b623-5d936566663d)

## 1) Which NYC schools have the best math results?
- The best math results are at least 80% of the *maximum possible score of 800* for math.
- Save your results in a pandas DataFrame called best_math_schools, including "school_name" and "average_math" columns, sorted by "average_math" in descending order.

**#Step 1: Calculate the threshold:** 
```python
threshold = 800 * 0.8
```

**#Step 2: Filter the DataFrame:**
```python
##Next, filter the `schools` DataFrame to include only those schools where the `average_math` score meets or exceeds the threshold:

best_math_schools = schools[schools['average_math'] >= threshold]
```

**#Step 3: Select Relevant Columns and Sort**
```python
##Now, select only the `school_name` and `average_math` columns, and sort the schools by `average_math` in descending order:

best_math_schools = best_math_schools[['school_name', 'average_math']].sort_values(by='average_math', ascending=False)
print(best_math_schools)
```
![image](https://github.com/user-attachments/assets/b88898c8-b8e8-4cfb-b0fb-0abb3c17d9f7)

## 2) What are the top 10 performing schools based on the combined SAT scores? 
- Save your results as a pandas DataFrame called top_10_schools containing the "school_name" and a new column named "total_SAT", with results ordered by "total_SAT" in descending order ("total_SAT" being the sum of math, reading, and writing scores).
```python
schools["total_SAT"] = schools["average_math"] + schools["average_reading"] + schools["average_writing"]

top_10_schools = schools[["school_name", "total_SAT"]].sort_values("total_SAT", ascending=False).head(10)
print(top_10_schools)
```

![image](https://github.com/user-attachments/assets/f05a242c-424d-46e1-a5fa-d80e7d7e1001)

**3) Which single borough has the largest standard deviation in the combined SAT score?**
- Save your results as a pandas DataFrame called largest_std_dev.
- The DataFrame should contain one row, with:
-   "borough" - the name of the NYC borough with the largest standard deviation of "total_SAT".
-   "num_schools" - the number of schools in the borough.
-   "average_SAT" - the mean of "total_SAT".
-   "std_SAT" - the standard deviation of "total_SAT".
- Round all numeric values to two decimal places.

**#Step 1: Group the data by Borough**
```python
#Group the data by "borough" and find the count of schools, mean and standard deviation of "total_SAT".
stats = schools.groupby('borough')['total_SAT'].agg(['std', 'mean', 'count']).reset_index()
```

**#Step 2: Identify the Borough with the Largest Standard Deviation**
```python
#Find the borough that has the largest standard deviation in `total_SAT`. 
largest_std_borough = stats.loc[stats['std'].idxmax()]
```

**#Step 3: Format the DataFrame**
```python
#Create a new DataFrame called `largest_std_dev` with the required structure and round the numeric values.
largest_std_dev = pd.DataFrame({
    'borough': [largest_std_borough['borough']],
    'num_schools': [largest_std_borough['count']],
    'average_SAT': [round(largest_std_borough['mean'], 2)],
    'std_SAT': [round(largest_std_borough['std'], 2)]
})

print(largest_std_dev)
```
![image](https://github.com/user-attachments/assets/60973240-cdcb-4f62-93bb-bb3c11afc966)


