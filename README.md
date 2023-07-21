---
title: Exploring Academic Performance in General Mathematics 1
description: A Case Study of Students at AmirKabir University of Technology
by: Koorosh Komeilizadeh
---

Open Project Notebook for a better experience: [project_notebook.ipynb](https://github.com/kooroshkz/math_grades_analysis/blob/main/project_notebook.ipynb)

<div class="cell markdown">

<img src="https://www.irangi.org/uploads/images/4_1560089256_1291127534.png" style=".invert{  filter: invert(0%);};display: block;margin-left: auto;margin-right: auto;width: 20%;">

</div>

<div class="cell markdown">

<h2 style="text-align: center;">Exploring Academic Performance in General Mathematics 1</h2>
<h3 style="text-align: center;">A Case Study of Students at AmirKabir University of Technology</h3>
<h4 style="text-align: center;">by Koorosh Komeilizadeh</h4>

</div>

<div class="cell markdown">

<div style="text-align: center;">
  <a href="mailto:kkomeilizadeh@gmail.com" target="_blank">
    <i class="fa fa-envelope" style="font-size: 24px; color: #808080;"></i>
  </a>
  &nbsp;&nbsp;&nbsp;
  <a href="https://kooroshkz.com/" target="_blank">
    <i class="fa fa-globe" style="font-size: 24px; color: #808080;"></i>
  </a>
  &nbsp;&nbsp;&nbsp;
  <a href="https://github.com/kooroshkz" target="_blank">
    <i class="fa fa-github" style="font-size: 24px; color: #808080;"></i>
  </a>
  &nbsp;&nbsp;&nbsp;
  <a href="https://www.linkedin.com/in/kooroshkz/" target="_blank">
    <i class="fa fa-linkedin" style="font-size: 24px; color: #808080;"></i>
  </a>
</div>

</div>

<div class="cell markdown">

## Project Introduction

<p>In this project, our primary objective is to conduct a meticulous analysis of student and instructor performance during the grading process for General Mathematics 1 at AmirKabir University of Technology for the 1401 academic year. Leveraging a dataset generously provided by the esteemed Faculty of Mathematics and Computer Science, we will employ advanced data retrieval and cleaning techniques to ensure data accuracy and consistency. By scrutinizing the information meticulously, we aim to discern insightful trends and patterns that can shed light on the efficacy of the grading system and identify areas for potential improvement. Our findings will serve as a valuable resource for enhancing the overall educational experience and fostering an environment of academic excellence at the university.</p>

</div>

<div class="cell markdown" tags="[]">

## Outlines

-   [1 Preview](#Preview)
    -   [  1.1 Dataset](#Dataset)
    -   [  1.2 Goals](#Goals)
    -   [  1.3 Tools](#Tools)
    -   [  1.4 Author and Analyst](#bio)
-   [2 Data Processing](#Data_Processing)
    -   [  2.1 Import Data](#importdata)
    -   [  2.2 Data Cleaning](#clean)
    -   [  2.2 Data Output to CSV](#csvout)
-   [3 Data Visualisation](#visual)
    -   [  3.1 Data Overview](#Overview)
    -   [  3.2 Grades by Professors](#gradbyp)
-   [4 Correlation of Clusters with Grades](#stu)
    -   [  4.1 Correlation between majors and grades](#major)
    -   [  4.2 Mean math grades for majors](#mean)
    -   [  4.3 Majors on Mid-Final Plot](#mmf)
-   [5 Machine Learning Model](#ml)
    -   [  5.1 Data Processing](#mldp)
    -   [  5.2 Single Linear Regression Model](#slrm)
    -   [  5.3 Multi Linear Regression Model](#mlrm)

</div>

<div class="cell markdown" jp-MarkdownHeadingCollapsed="true" tags="[]">

<a name="Preview"></a>

## 1- Preview

</div>

<div class="cell markdown" tags="[]">

<a name="Dataset"></a>

### 1.1 Dataset

The Faculty of Mathematics and Computer Science at AmirKabir University
of Technology provides reports in Excel format, transparently disclosing
students' detailed grades for each semester. Our objective is to import
this data into a data frame, perform data cleaning, and eliminate any
outliers to conduct appropriate data analysis. The dataset pertains to
General Mathematics 1 for the 1401 academic year at AmirKabir University
of Technology

</div>

<div class="cell markdown" jp-MarkdownHeadingCollapsed="true" tags="[]">

<a name="Goals"></a>

### 1.2 Goals

    - Understanding Grade Distribution of Students.
    - Exploring the Correlation between Instructors and Average Grades.
    - Investigating the Relationship Between Students' Majors and Grade Status.
    - Predicting Final Grades based on Midterm and Homework Scores.
    - Providing a Clean Dataset of Grades for Future Research Purposes.

</div>

<div class="cell markdown">

<a name="Tools"></a>

### 1.3 Tools

-   ##### Pandas

    Utilized to convert the data into a data frame format, enabling
    efficient data cleaning and storage.

-   ##### Numpy

    Employed for advanced mathematical functions and array operations.

-   ##### Matplotlib

    Used for data visualization and generating various types of plots
    and graphs to better understand the data.

-   ##### Scikit-learn

    Applied to develop Linear regression models for predictive analysis
    and Encoding Labels for non-numeric datas

</div>

<div class="cell markdown">

<a name="bio"></a>

### 1.4 Author and Analyst

#### Koorosh Komeilizadeh

##### Data Science and Artificial Intelligence <br>undergraduate student at Leiden University

Passionate Data Science & AI student with expertise in Python, Machine
Learning, and Data Analysis. Eager to explore innovative applications of
AI and committed to driving data-driven solutions for impactful
research.

Email : <kkomeilizadeh@gmail.com><br>Website :
<a href="https://kooroshkz.com">www.kooroshkz.com</a><br>Github &
LinkedIn : kooroshkz

</div>

<div class="cell markdown" jp-MarkdownHeadingCollapsed="true" tags="[]">

<a name="Data_Processing"></a>

## 2- Data Processing

</div>

<div class="cell markdown" jp-MarkdownHeadingCollapsed="true" tags="[]">

<a name="importdata"></a>

### 2.1 Import Data

Importing data from excel file, then merge sheets into a single
DataFrame via pandas

</div>

<div class="cell code" execution_count="1">

``` python
import pandas as pd
```

</div>

<div class="cell code" execution_count="2">

``` python
all_sheets = pd.read_excel("grades.xlsx", sheet_name=None)
```

</div>

<div class="cell code" execution_count="3">

``` python
merged_df = pd.concat(all_sheets.values(), ignore_index=True)
```

</div>

<div class="cell code" execution_count="4">

``` python
merged_df
```

<div class="output execute_result" execution_count="4">

          گروه درس  شماره دانشجو  تکلیف1  تکلیف2  تکلیف3  تکلیف4  تکلیف5  تکلیف6  \
    0            1      40027008    40.0    33.0     0.0    35.0    40.0      40   
    1            1      40113901    37.0    33.0    38.0     0.0    40.0      40   
    2            1      40122045    24.0    32.0    40.0    20.0    15.0      40   
    3            1      40122046     0.0    36.0    40.0    40.0    40.0      40   
    4            1      40122047     0.0     0.0     0.0     0.0     0.0      40   
    ...        ...           ...     ...     ...     ...     ...     ...     ...   
    1276        19      40132012     0.0    40.0    40.0    36.0    35.0       0   
    1277        19      40132013    25.0    20.0    20.0    37.0    40.0      40   
    1278        19      40132021    40.0    34.0    40.0    40.0    40.0      40   
    1279        19      40132033     0.0     0.0    40.0    38.0    35.0      40   
    1280        19      40132048    37.0    39.0    38.0    38.0    35.0      40   

         تکلیف7  تکلیف8  ...  پایانترم از 9  میانترم از7  نهایی 1  پایانترم از13  \
    0        35     0.0  ...            0.5          2.2     4.93       0.722222   
    1        40    40.0  ...            3.0          3.1     8.78       4.333333   
    2        35    18.0  ...            1.0          4.3     7.54       1.444444   
    3        35    40.0  ...            1.9          0.1     4.71       2.744444   
    4         0     0.0  ...            0.0          1.1     1.50       0.000000   
    ...     ...     ...  ...            ...          ...      ...            ...   
    1276     35    22.0  ...            3.5          3.9     9.48       5.055556   
    1277     40     0.0  ...            6.3          0.0     8.52       9.100000   
    1278     40    40.0  ...            8.6          5.6    17.34      12.422222   
    1279     40     0.0  ...            5.8          2.3    10.03       8.377778   
    1280     40    40.0  ...            8.5          0.0    11.57      12.277778   

          میانترم از3     نهایی2  نمره تدریس یار  کلاسی استاد    ماکسیمم  \
    0        0.942857   3.895079             NaN          NaN   4.930000   
    1        1.328571   8.341905             NaN          NaN   8.780000   
    2        1.842857   5.527302             NaN          NaN   7.540000   
    3        0.042857   5.497302             NaN          NaN   5.497302   
    4        0.471429   0.871429             NaN          NaN   1.500000   
    ...           ...        ...             ...          ...        ...   
    1276     1.671429   8.806984             NaN          NaN   9.480000   
    1277     0.000000  11.320000             NaN          NaN  11.320000   
    1278     2.400000  17.962222             NaN          NaN  17.962222   
    1279     0.985714  11.293492             NaN          NaN  11.293492   
    1280     0.000000  15.347778             NaN          NaN  15.347778   

               استاد  
    0     دکتر کیانی  
    1     دکتر کیانی  
    2     دکتر کیانی  
    3     دکتر کیانی  
    4     دکتر کیانی  
    ...          ...  
    1276  دکترشریعتی  
    1277  دکترشریعتی  
    1278  دکترشریعتی  
    1279  دکترشریعتی  
    1280  دکترشریعتی  

    [1281 rows x 28 columns]

</div>

</div>

<div class="cell markdown">

<a name="clean"></a>

### 2.2 Data Cleaning

Remove extra features

</div>

<div class="cell code" execution_count="5">

``` python
columns = merged_df.columns.tolist()
extra_columns = columns[0:1] + columns[10:19] + columns[21:-1]
merged_df.drop(extra_columns, axis=1, inplace=True)
```

</div>

<div class="cell code" execution_count="6">

``` python
merged_df
```

<div class="output execute_result" execution_count="6">

          شماره دانشجو  تکلیف1  تکلیف2  تکلیف3  تکلیف4  تکلیف5  تکلیف6 تکلیف7  \
    0         40027008    40.0    33.0     0.0    35.0    40.0      40     35   
    1         40113901    37.0    33.0    38.0     0.0    40.0      40     40   
    2         40122045    24.0    32.0    40.0    20.0    15.0      40     35   
    3         40122046     0.0    36.0    40.0    40.0    40.0      40     35   
    4         40122047     0.0     0.0     0.0     0.0     0.0      40      0   
    ...            ...     ...     ...     ...     ...     ...     ...    ...   
    1276      40132012     0.0    40.0    40.0    36.0    35.0       0     35   
    1277      40132013    25.0    20.0    20.0    37.0    40.0      40     40   
    1278      40132021    40.0    34.0    40.0    40.0    40.0      40     40   
    1279      40132033     0.0     0.0    40.0    38.0    35.0      40     40   
    1280      40132048    37.0    39.0    38.0    38.0    35.0      40     40   

          تکلیف8  میانترم از7  نهایی 1       استاد  
    0        0.0          2.2     4.93  دکتر کیانی  
    1       40.0          3.1     8.78  دکتر کیانی  
    2       18.0          4.3     7.54  دکتر کیانی  
    3       40.0          0.1     4.71  دکتر کیانی  
    4        0.0          1.1     1.50  دکتر کیانی  
    ...      ...          ...      ...         ...  
    1276    22.0          3.9     9.48  دکترشریعتی  
    1277     0.0          0.0     8.52  دکترشریعتی  
    1278    40.0          5.6    17.34  دکترشریعتی  
    1279     0.0          2.3    10.03  دکترشریعتی  
    1280    40.0          0.0    11.57  دکترشریعتی  

    [1281 rows x 12 columns]

</div>

</div>

<div class="cell markdown">

Rename headers

</div>

<div class="cell code" execution_count="7">

``` python
merged_df.columns = ["ID"] + [f"HW{x}" for x in range(1,9)] + ["mid", "final", "prof"]
```

</div>

<div class="cell markdown">

Fix duplicate prof name error

</div>

<div class="cell code" execution_count="8">

``` python
merged_df.replace("دکترخسروی", "دکتر خسروی", inplace=True)
merged_df.replace("شجاعی", "دکترشجاعی", inplace=True)
```

</div>

<div class="cell markdown">

Rename instructors names to English

</div>

<div class="cell code" execution_count="9">

``` python
prof_names = {
    "دکتر ایمانفر": "Dr. Imanfar",
    "دکتر خسروی": "Dr. Khosravi",
    "دکتر رحمتی": "Dr. Rahmati",
    "دکتر رستمی": "Dr. Rostami",
    "دکتر نجفی": "Dr. Najafi",
    "دکتر کیانی": "Dr. Kiani",
    "دکتراخلاقی": "Dr. Akhlaghi",
    "دکتربروجردیان": "Dr. Boroujerdiyan",
    "دکتربیاتی": "Dr. Bayati",
    "دکترتوانا": "Dr. Tavana",
    "دکتررضی": "Dr. Razi",
    "دکترسعیدی مدنی": "Dr. Saeidi Madani",
    "دکترشجاعی": "Dr. Shojai",
    "دکترشریعتی": "Dr. Shariaty"
}
```

</div>

<div class="cell code" execution_count="10">

``` python
merged_df["prof"] = merged_df["prof"].replace(prof_names)
```

</div>

<div class="cell markdown">

Label encoding the professors' names using scikit-learn label encoder.

</div>

<div class="cell code" execution_count="11">

``` python
from sklearn.preprocessing import LabelEncoder
```

</div>

<div class="cell code" execution_count="12">

``` python
label_encoder = LabelEncoder()

merged_df['prof'] = label_encoder.fit_transform(merged_df['prof'])
encoded_dict = {label: index for index, label in enumerate(label_encoder.classes_)}
encoded_dict = pd.DataFrame(encoded_dict.items(), columns=['profname', 'Encoded number'])
```

</div>

<div class="cell code" execution_count="13">

``` python
encoded_dict.T
```

<div class="output execute_result" execution_count="13">

                              0           1                  2            3   \
    profname        Dr. Akhlaghi  Dr. Bayati  Dr. Boroujerdiyan  Dr. Imanfar   
    Encoded number             0           1                  2            3   

                              4          5           6            7         8   \
    profname        Dr. Khosravi  Dr. Kiani  Dr. Najafi  Dr. Rahmati  Dr. Razi   
    Encoded number             4          5           6            7         8   

                             9                  10            11          12  \
    profname        Dr. Rostami  Dr. Saeidi Madani  Dr. Shariaty  Dr. Shojai   
    Encoded number            9                 10            11          12   

                            13  
    profname        Dr. Tavana  
    Encoded number          13  

</div>

</div>

<div class="cell markdown">

Drop rows with any non-numeric values and reset the indexes.

</div>

<div class="cell code" execution_count="14">

``` python
merged_df = merged_df.apply(pd.to_numeric, errors='coerce')
merged_df = merged_df.dropna()
merged_df.reset_index(drop=True, inplace=True)
```

</div>

<div class="cell code" execution_count="15">

``` python
cleaned_df = merged_df
cleaned_df
```

<div class="output execute_result" execution_count="15">

                ID   HW1   HW2   HW3   HW4   HW5  HW6   HW7   HW8  mid  final  \
    0     40027008  40.0  33.0   0.0  35.0  40.0   40  35.0   0.0  2.2   4.93   
    1     40113901  37.0  33.0  38.0   0.0  40.0   40  40.0  40.0  3.1   8.78   
    2     40122045  24.0  32.0  40.0  20.0  15.0   40  35.0  18.0  4.3   7.54   
    3     40122046   0.0  36.0  40.0  40.0  40.0   40  35.0  40.0  0.1   4.71   
    4     40122047   0.0   0.0   0.0   0.0   0.0   40   0.0   0.0  1.1   1.50   
    ...        ...   ...   ...   ...   ...   ...  ...   ...   ...  ...    ...   
    1267  40132012   0.0  40.0  40.0  36.0  35.0    0  35.0  22.0  3.9   9.48   
    1268  40132013  25.0  20.0  20.0  37.0  40.0   40  40.0   0.0  0.0   8.52   
    1269  40132021  40.0  34.0  40.0  40.0  40.0   40  40.0  40.0  5.6  17.34   
    1270  40132033   0.0   0.0  40.0  38.0  35.0   40  40.0   0.0  2.3  10.03   
    1271  40132048  37.0  39.0  38.0  38.0  35.0   40  40.0  40.0  0.0  11.57   

          prof  
    0        5  
    1        5  
    2        5  
    3        5  
    4        5  
    ...    ...  
    1267    11  
    1268    11  
    1269    11  
    1270    11  
    1271    11  

    [1272 rows x 12 columns]

</div>

</div>

<div class="cell markdown">

<a name="csvout"></a>

### 2.2 Data Output to CSV

</div>

<div class="cell code" execution_count="16">

``` python
cleaned_df.to_csv('data_sets/grades.csv', index=False)
encoded_dict.to_csv('data_sets/prof_dict.csv', index=False)
```

</div>

<div class="cell markdown" jp-MarkdownHeadingCollapsed="true" tags="[]">

<a name="visual"></a>

## 3- Data Visualisation

</div>

<div class="cell markdown">

<a name="Overview"></a>

### 3.1 Data Overview

An overview of the distribution of grades for students in General
Mathematics 1 in comparison between midterm and final exam grades.

</div>

<div class="cell code" execution_count="17">

``` python
df = cleaned_df
```

</div>

<div class="cell code" execution_count="18">

``` python
df[["mid","final"]].describe()
```

<div class="output execute_result" execution_count="18">

                   mid        final
    count  1272.000000  1272.000000
    mean      3.557390     9.860483
    std       2.188107     4.952926
    min       0.000000     0.000000
    25%       1.850000     6.107500
    50%       3.700000    10.010000
    75%       5.400000    13.802500
    max       7.000000    19.140000

</div>

</div>

<div class="cell code" execution_count="19">

``` python
import matplotlib.pyplot as plt
```

</div>

<div class="cell code" execution_count="20">

``` python
max_final = df['final'].max()
cmap = plt.colormaps.get_cmap('RdYlGn')
normalized_final = df['final'] / max_final
plt.figure(figsize=(10, 8))
plt.scatter(df['mid'], df['final'], c=normalized_final, cmap=cmap, marker='o', s=50)
plt.xlabel('mid')
plt.ylabel('Final grades')
plt.title('Mid-Final grades Graph')
plt.colorbar(label='Normalized Final Grade')

plt.show()
```

<div class="output display_data">

![](a53766b6e868b8e48118bdc8a97472edae711ca0.png)

</div>

</div>

<div class="cell markdown">

<a name="gradbyp"></a>

### 3.2 Grades by Professors

An overview of the distribution of grades for students in General
Mathematics 1 in comparison between midterm and final exam grades.

</div>

<div class="cell markdown">

#### Mean Grades by Professors

</div>

<div class="cell code" execution_count="21">

``` python
average_final_grade = df.groupby('prof')['final'].mean()

print(average_final_grade)
```

<div class="output stream stdout">

    prof
    0      9.154219
    1      8.990282
    2      8.043429
    3     10.676857
    4      9.294724
    5      9.924054
    6     12.252857
    7      9.070423
    8     10.750563
    9      8.762000
    10     9.897465
    11    11.624077
    12     9.744924
    13     8.502246
    Name: final, dtype: float64

</div>

</div>

<div class="cell code" execution_count="22">

``` python
average_final_grade = df.groupby('prof')['final'].mean()
average_final_grade_dict = average_final_grade.to_dict()
grades = average_final_grade.tolist()

normalized_grades = [(g - min(grades)) / (max(grades) - min(grades)) for g in grades]

cmap = plt.get_cmap('RdYlGn')

plt.figure(figsize=(10, 6))

for professor, norm_grade in zip(average_final_grade.keys(), normalized_grades):
    color = cmap(norm_grade)
    plt.bar(professor, average_final_grade[professor], color=color)

plt.xlabel('Professor')
plt.ylabel('Average Final Grade')
plt.title('Average Final Grade by Professor')
plt.xticks(rotation=90)

sm = plt.cm.ScalarMappable(cmap=cmap, norm=plt.Normalize(vmin=0, vmax=1))
sm.set_array([])

plt.show()
```

<div class="output display_data">

![](883b2b715649e14265ebf43ad03bc5e3517e3217.png)

</div>

</div>

<div class="cell markdown">

#### 3D vectorization

</div>

<div class="cell code" execution_count="23">

``` python
from matplotlib.colors import ListedColormap
```

</div>

<div class="cell code" execution_count="24">

``` python
df_prof_named = df

df_prof_named["prof"] = label_encoder.inverse_transform(merged_df["prof"])
```

</div>

<div class="cell code" execution_count="25">

``` python
df_prof_named['prof'] = pd.Categorical(df_prof_named['prof'])
num_professors = len(df_prof_named['prof'].cat.categories)
cmap = ListedColormap(plt.cm.tab20.colors[:num_professors])
fig = plt.figure(figsize=(10, 8))
ax = fig.add_subplot(111, projection='3d')
x, y , z = df_prof_named['mid'], df_prof_named['prof'].cat.codes, df_prof_named['final']
sc = ax.scatter(x, y, z, c=df_prof_named['prof'].cat.codes, cmap=cmap, marker='o', s=50)
ax.set_xlabel('mid')
ax.set_ylabel('prof')
ax.set_zlabel('final')
ax.set_title('Grades based on profs')
cbar = plt.colorbar(sc, ticks=range(num_professors))
cbar.set_label('Professors')
cbar.set_ticklabels(df_prof_named['prof'].cat.categories)

plt.show()
```

<div class="output display_data">

![](358050d7c5ed1215eb7a5fdb56a09b3870fa384c.png)

</div>

</div>

<div class="cell markdown" jp-MarkdownHeadingCollapsed="true" tags="[]">

<a name="stu"></a>

## 4- Correlation of Clusters with Grades

</div>

<div class="cell markdown">

<a name="major"></a>

### 4.1 Correlation between majors and grades

By student ID, we have categorized grades into majors to find out if
there is any correlation between students' majors and their math grades.

</div>

<div class="cell code" execution_count="26">

``` python
major_df = df[["ID","mid","final"]]
```

</div>

<div class="cell code" execution_count="27">

``` python
pd.options.mode.chained_assignment = None
major_df['ID'] = major_df['ID'].astype(str).apply(lambda x: x[3:5])
```

</div>

<div class="cell code" execution_count="28">

``` python
majors = {
    23: "Electrical Engineering",    26: "Mechanical Engineering",
    22: "Chemical Engineering",    33: "Biomedical Engineering",
    34: "Petroleum Engineering",    27: "Mining Engineering",
    39: "Materials Engineering",    24: "Civil Engineering",
    29: "Aerospace Engineering",    11: "Physics and Energy",
    25: "Industrial Engineering",    31: "Computer Engineering",
    13: "Computer Science",    12: "Applied Mathematics",
    30: "Marine Engineering",    32: "Polymer Engineering",
    28: "Textile Engineering"
}

majors = {str(k): v for k, v in majors.items()}
major_df['ID'] = major_df['ID'].astype(str).replace(majors)
```

</div>

<div class="cell code" execution_count="29">

``` python
major_ranked = major_df.groupby('ID')['final'].mean().reset_index().sort_values(by='final', ascending=False).reset_index(drop=True)
```

</div>

<div class="cell markdown" tags="[]">

<a name="mean"></a>

### 4.2 Mean math grades for majors

</div>

<div class="cell code" execution_count="30">

``` python
import numpy as np

plt.figure(figsize=(12, 6))
colors = plt.cm.coolwarm(np.linspace(0, 1, len(major_ranked)))
bars = plt.bar(major_ranked['ID'], major_ranked['final'], color=colors)
plt.xticks(rotation=90, fontsize=10)
plt.xlabel('Majors')
plt.ylabel('Final Ranking Score')
plt.title('Majors Ranking')
for bar, value in zip(bars, major_ranked['final']):
    plt.annotate(f'{value:.2f}', xy=(bar.get_x() + bar.get_width() / 2, bar.get_height()), xytext=(0, 3),
                 textcoords="offset points", ha='center', va='bottom', fontsize=8)
sm = plt.cm.ScalarMappable(cmap='coolwarm', norm=plt.Normalize(vmin=major_ranked['final'].min(), vmax=major_ranked['final'].max()))
sm.set_array([])
plt.tight_layout()
plt.show()
```

<div class="output display_data">

![](06cfb1541c401c02f472e72875f9767cc219b2dd.png)

</div>

</div>

<div class="cell markdown" tags="[]">

<a name="mmf"></a>

### 4.3 Majors on Mid-Final Plot

</div>

<div class="cell code" execution_count="31">

``` python
major_df
```

<div class="output execute_result" execution_count="31">

                            ID  mid  final
    0       Mining Engineering  2.2   4.93
    1         Computer Science  3.1   8.78
    2     Chemical Engineering  4.3   7.54
    3     Chemical Engineering  0.1   4.71
    4     Chemical Engineering  1.1   1.50
    ...                    ...  ...    ...
    1267   Polymer Engineering  3.9   9.48
    1268   Polymer Engineering  0.0   8.52
    1269   Polymer Engineering  5.6  17.34
    1270   Polymer Engineering  2.3  10.03
    1271   Polymer Engineering  0.0  11.57

    [1272 rows x 3 columns]

</div>

</div>

<div class="cell code" execution_count="32">

``` python
import warnings
warnings.filterwarnings('ignore')
```

</div>

<div class="cell code" execution_count="33">

``` python
cmap = plt.cm.get_cmap('viridis', len(major_df['ID'].unique()))
plt.figure(figsize=(10, 6))
for i, (ID, group) in enumerate(major_df.groupby('ID')):
    plt.scatter(group['mid'], group['final'], color=cmap(i), label=ID)

plt.xlabel('mid')
plt.ylabel('final')
plt.title('Scatter Plot of mid vs final')
plt.legend(loc='upper left', bbox_to_anchor=(1, 1))
plt.grid(True)
plt.show()
```

<div class="output display_data">

![](8c7d23649b341dc3bcbf0cfb826278973dbb0a64.png)

</div>

</div>

<div class="cell markdown" jp-MarkdownHeadingCollapsed="true" tags="[]">

<a name="ml"></a>

## 5- Machine Learning Model

</div>

<div class="cell markdown">

<a name="mldp"></a>

### 5.1 Data Processing

</div>

<div class="cell markdown">

import processed data

</div>

<div class="cell code" execution_count="34">

``` python
df = pd.read_csv("data_sets/grades.csv")
```

</div>

<div class="cell code" execution_count="35">

``` python
df.head()
```

<div class="output execute_result" execution_count="35">

             ID   HW1   HW2   HW3   HW4   HW5  HW6   HW7   HW8  mid  final  prof
    0  40027008  40.0  33.0   0.0  35.0  40.0   40  35.0   0.0  2.2   4.93     5
    1  40113901  37.0  33.0  38.0   0.0  40.0   40  40.0  40.0  3.1   8.78     5
    2  40122045  24.0  32.0  40.0  20.0  15.0   40  35.0  18.0  4.3   7.54     5
    3  40122046   0.0  36.0  40.0  40.0  40.0   40  35.0  40.0  0.1   4.71     5
    4  40122047   0.0   0.0   0.0   0.0   0.0   40   0.0   0.0  1.1   1.50     5

</div>

</div>

<div class="cell markdown">

Split data into train and test set

</div>

<div class="cell code" execution_count="36">

``` python
from sklearn.model_selection import train_test_split
```

</div>

<div class="cell markdown">

for slrm

</div>

<div class="cell code" execution_count="37">

``` python
slrm_X = df[['mid']]
slrm_y = df['final']

slrm_X_train, slrm_X_test, slrm_y_train, slrm_y_test = train_test_split(slrm_X, slrm_y, test_size=0.2, random_state=42)
```

</div>

<div class="cell markdown">

for mlrm

</div>

<div class="cell code" execution_count="38">

``` python
mlrm_X = df[['HW1', 'HW2', 'HW3', 'HW4', 'HW5', 'HW6', 'HW7', 'HW8', 'mid', 'prof']]
mlrm_y = df['final']

mlrm_X_train, mlrm_X_test, mlrm_y_train, mlrm_y_test = train_test_split(mlrm_X, mlrm_y, test_size=0.2, random_state=42)
```

</div>

<div class="cell markdown">

<a name="slrm"></a>

### 5.2 Simple Linear Regression Model

</div>

<div class="cell markdown">

Simple Linear Regression is a statistical technique to model the linear
relationship between a dependent variable (*Y*) and an independent
variable (*X*) as: *Y* = *β*0 + *β*1 \* *X* + *ε*. It assumes linearity,
independence, homoscedasticity, and normality of residuals.

Scikit-learn, a popular Python library, offers an efficient
implementation of Simple Linear Regression. It simplifies model
training, prediction, and evaluation. By using scikit-learn, you can
preprocess data, split it into training and testing sets, and assess the
model's accuracy with metrics like Mean Squared Error or R-squared.

</div>

<div class="cell markdown">

Create a linear regression object and Fit the model to the training data

</div>

<div class="cell code" execution_count="39">

``` python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_absolute_error, mean_squared_error, r2_score
```

</div>

<div class="cell code" execution_count="40">

``` python
model = LinearRegression()
model.fit(slrm_X_train, slrm_y_train)
```

<div class="output execute_result" execution_count="40">

    LinearRegression()

</div>

</div>

<div class="cell markdown">

Predict using the model on the testing set

</div>

<div class="cell code" execution_count="41">

``` python
slrm_y_test_pred = model.predict(slrm_X_test)
```

</div>

<div class="cell markdown">

Calculate error metrics on the testing set

</div>

<div class="cell code" execution_count="42">

``` python
mae_test = mean_absolute_error(slrm_y_test, slrm_y_test_pred)
mse_test = mean_squared_error(slrm_y_test, slrm_y_test_pred)
r2_test = r2_score(slrm_y_test, slrm_y_test_pred)
```

</div>

<div class="cell markdown">

What we are looking for are the values of *w* (Weight) and *b* (Bias) to
place in our simple linear regression model:
*f*<sub>*w*, *b*</sub>(*x*) = *w**x* + *b*

Scikit-learn will present this values after calculatoin as coefficient
for *w* and intercept for *b* by $(w,b) =
$`(model.coef_ , model.intercept_)`

</div>

<div class="cell code" execution_count="73">

``` python
print(f"f(x) = {float(model.coef_):.3f}X + {model.intercept_:.3f}")
```

<div class="output stream stdout">

    f(x) = 2.014X + 2.723

</div>

</div>

<div class="cell markdown">

*f*<sub>*w*, *b*</sub>(*x*) = 2.014*x* + 2.723

</div>

<div class="cell markdown">

Plot the data and the regression line for the testing set

</div>

<div class="cell code" execution_count="43">

``` python
plt.scatter(slrm_X_train, slrm_y_train, label="Training Data")
plt.plot(slrm_X_test, slrm_y_test_pred, color='green', label="Regression Line")
plt.xlabel('mid')
plt.ylabel('final')
plt.legend()
plt.title('Simple Linear Regression - Training Data')
plt.show()
```

<div class="output display_data">

![](b8ff17536a32b80bac673edcdccc9b878c8386c5.png)

</div>

</div>

<div class="cell markdown">

Plot the data and the regression line for the testing set

</div>

<div class="cell code" execution_count="44">

``` python
plt.scatter(slrm_X_test, slrm_y_test, label="Testing Data")
plt.plot(slrm_X_test, slrm_y_test_pred, color='green', label="Regression Line")
plt.xlabel('mid')
plt.ylabel('final')
plt.legend()
plt.title('Simple Linear Regression - Testing Data')
plt.show()
```

<div class="output display_data">

![](02495fb75565441ffd1580d76b78fcc629398546.png)

</div>

</div>

<div class="cell markdown">

Display error metrics

</div>

<div class="cell markdown">

**Mean Absolute Error** (MAE) is the mean of the absolute value of the
errors:

$$\\frac 1n\\sum\_{i=1}^n\|y_i-\\hat{y}\_i\|$$

</div>

<div class="cell code" execution_count="62">

``` python
print("Testing Set - Mean Absolute Error (MAE): {:.2f}".format(mae_test))
```

<div class="output stream stdout">

    Testing Set - Mean Absolute Error (MAE): 1.75

</div>

</div>

<div class="cell markdown">

**Mean Squared Error** (MSE) is the mean of the squared errors:

$$\\frac 1n\\sum\_{i=1}^n(y_i-\\hat{y}\_i)^2$$

</div>

<div class="cell code" execution_count="63">

``` python
print("Testing Set - Mean Squared Error (MSE): {:.2f}".format(mse_test))
```

<div class="output stream stdout">

    Testing Set - Mean Squared Error (MSE): 4.66

</div>

</div>

<div class="cell markdown">

**R-squared** represents the proportion of the variance in the dependent
variable

$$1 - \\frac{\\sum (y_i - \\bar{y})^2}{\\sum (y_i - \\hat{y}\_i)^2}$$

</div>

<div class="cell code" execution_count="64">

``` python
print("Testing Set - R-squared (coefficient of determination): {:.2f}".format(r2_test))
```

<div class="output stream stdout">

    Testing Set - R-squared (coefficient of determination): 0.82

</div>

</div>

<div class="cell markdown">

1 - ∑(y_i - ŷ_i)^2 / ∑(y_i - ȳ)^2

</div>

<div class="cell markdown" tags="[]">

<a name="mlrm"></a>

### 5.3 Multi Linear Regression Model

</div>

<div class="cell markdown">

MLRM (Multiple Linear Regression Model) is a statistical technique used
to model the relationship between a dependent variable and two or more
independent variables. The model assumes a linear relationship, and it
can be represented as:

*y* = *β*<sub>0</sub> + *β*<sub>1</sub> ⋅ *x*<sub>1</sub> + *β*<sub>2</sub> ⋅ *x*<sub>2</sub> + … + *β*<sub>*n*</sub> ⋅ *x*<sub>*n*</sub> + *ε*

Where:

-   *y* is the dependent variable.
-   (*x*<sub>1</sub>,*x*<sub>2</sub>,…,*x*<sub>*n*</sub>) are the
    independent variables.
-   (*β*<sub>0</sub>,*β*<sub>1</sub>,*β*<sub>2</sub>,…,*β*<sub>*n*</sub>)
    are the coefficients.
-   (*ε*) is the error term.

Scikit-learn, a Python library, provides an easy-to-use implementation
of MLRM through the `LinearRegression` class. You can create and train a
model, estimate coefficients, and make predictions using this class.

</div>

<div class="cell markdown">

Train the Multiple Linear Regression Model:

</div>

<div class="cell code" execution_count="77">

``` python
mlrm = LinearRegression()
mlrm.fit(mlrm_X_train, mlrm_y_train)
train_score = mlrm.score(mlrm_X_train, mlrm_y_train)
test_score = mlrm.score(mlrm_X_test, mlrm_y_test)
```

</div>

<div class="cell markdown">

Final Function which is in form:
$$f\_{w,b}(x^{(i)}) = \\sum\_{n=1}^i(w^{(i)} x^{(i)}) + b $$

</div>

<div class="cell markdown">

Scikit-learn represents coefitients as `mlrm.coef_` and intercept as
`mlrm.intercept_` so we can extract *f*<sub>*w*, *b*</sub> as:

</div>

<div class="cell code" execution_count="86">

``` python
coefficients = mlrm.coef_
feature_names = mlrm_X.columns

formula = "Final Grade = "
for i, (coefficient, feature_name) in enumerate(zip(coefficients, feature_names)):
    if i == 0:
        formula += f"{coefficient:.2f} * {feature_name}"
    else:
        formula += f" + {coefficient:.2f} * {feature_name}"

# Print the clean formula
print(f"{formula} + {mlrm.intercept_:.2f}")
```

<div class="output stream stdout">

    Final Grade = 0.02 * HW1 + 0.01 * HW2 + 0.01 * HW3 + 0.02 * HW4 + 0.02 * HW5 + 0.02 * HW6 + 0.02 * HW7 + 0.02 * HW8 + 1.79 * mid + -0.02 * prof + -0.27

</div>

</div>

<div class="cell markdown">

*f*<sub>*w*<sup>(*i*)</sup>, *b*</sub>(*x*<sup>(*i*)</sup>) = 0.02*H**W*<sup>(1)</sup> + 0.01*H**W*<sup>(2)</sup> + 0.01*H**W*<sup>(3)</sup> + 0.02*H**W*<sup>(4)</sup> + 0.02*H**W*<sup>(5)</sup> + 0.02*H**W*<sup>(6)</sup> + 0.02*H**W*<sup>(7)</sup> + 0.02*H**W*<sup>(8)</sup> + 1.79*m**i**d* − 0.27

</div>

<div class="cell markdown">

Score the model

</div>

<div class="cell markdown">

**R-squared** represents the proportion of the variance in the dependent
variable

$$1 - \\frac{\\sum (y_i - \\bar{y})^2}{\\sum (y_i - \\hat{y}\_i)^2}$$

</div>

<div class="cell code" execution_count="87">

``` python
print("Testing R-squared score:", test_score)
```

<div class="output stream stdout">

    Testing R-squared score: 0.8826555536699574

</div>

</div>

<div class="cell markdown">

Plotting the predicted values against the actual values in the test set

</div>

<div class="cell code" execution_count="50">

``` python
y_pred = mlrm.predict(mlrm_X_test)

plt.scatter(mlrm_y_test, y_pred)
plt.xlabel("Actual Final Grade")
plt.ylabel("Predicted Final Grade")
plt.title("Actual vs. Predicted Final Grade")
plt.show()
```

<div class="output display_data">

![](80579c5dff20a51105f310d9f4586a77f9d1e1b4.png)

</div>

</div>

<div class="cell code" execution_count="88">

``` python
plt.scatter(mlrm_X_test['mid'], mlrm_y_test, label='Actual', color='blue', alpha=0.5)

# Sort the mid values to create a smooth curve
sorted_mid = mlrm_X_test['mid'].sort_values()

# Predict the final grades using the sorted mid values and plot the curve
plt.plot(sorted_mid, model.predict(pd.DataFrame(sorted_mid, columns=['mid'])), label='MLRM', color='red')

plt.xlabel('mid')
plt.ylabel('final')
plt.title('MLRM Function')
plt.legend()
plt.grid(True)
plt.show()
```

<div class="output display_data">

![](fdcc6cddcaf325ebcba5137ca090698695adb138.png)

</div>

</div>
