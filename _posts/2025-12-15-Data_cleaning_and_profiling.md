---
layout: post
title: Data Cleaning and Profiling
---


Data Cleaning and Profiling (D599 Task1)

The objective of this project is to profile and clean the dataset of a large multinational tech company to optimize it for future analysis. In today’s highly competitive tech industry, attracting and retaining top talent is a critical business priority. This will enable the tech business to design more effective employee retention strategies.
Part I: Data Profiling
· Initial rows/records: 10,199
· Initial columns/variables: 16
Variables Data Type
1 Employee number Quantitative/Discrete
2 Age Quantitative/Discrete
3 Tenure Quantitative/Discrete
4 Turnover Qualitative/Nominal
5 HourlyRate Quantitative/Continuous
6 HoursWeekly Quantitative/Continuous
7 CompensationType Qualitative/Nominal
8 AnnualSalary Quantitative/Continuous
9 DrivingCommute Quantitative/Discrete
10 JobRole Qualitative/Nominal
11 Gender Qualitative/Nominal
12 MaritalStatus Qualitative/Nominal
13 NumCompaniesPreviouslyWorked Quantitative/Discrete
14 AnnualProfessionalDevHrs Quantitative/Discrete
15 PayCheckMethod Qualitative/Nominal
16 TextMessageOptin Qualitative/Nominal
print(df.head())
EmployeeNumber  Age  Tenure Turnover HourlyRate   HoursWeekly  \
0               1   28       6      Yes     $24.37            40   
1               2   33       2      Yes     $24.37            40   
2               3   22       1       No     $22.52            40   
3               4   23       1       No     $22.52            40   
4               5   40       6       No     $88.77            40   

  CompensationType  AnnualSalary  DrivingCommuterDistance  \
0           Salary       50689.6                       89   
1           Salary       50689.6                       89   
2           Salary       46841.6                       35   
3           Salary       46841.6                       35   
4           Salary      284641.6                       12   

              JobRoleArea                Gender MaritalStatus  \
0                Research                Female       Married   
1                Research                Female       Married   
2  Information_Technology                Female        Single   
3  Information_Technology                Female        Single   
4                   Sales  Prefer Not to Answer        Single   

   NumCompaniesPreviouslyWorked  AnnualProfessionalDevHrs PaycheckMethod  \
0                           3.0                       7.0     Mail Check   
1                           6.0                       7.0     Mail Check   
2                           1.0                       8.0   Mailed Check   
3                           3.0                       NaN   Mailed Check   
4                           7.0                       NaN     Mail Check   

  TextMessageOptIn  
0              Yes  
1              Yes  
2              Yes  
3              Yes  
4              Yes
Part II: Data Cleaning and Plan
B. Data Cleaning with Python
Data Quality Inspection and Findings
Find Duplicate Rows
In [138]:
df2=df.copy()

# Duplicates
print("\nDuplicate rows:", df.duplicated().sum()) #99 rows x 16 columns
print("\nDuplicate rows preview:")
print(df2[df2.duplicated()].head())

df2=df2.drop_duplicates()
print(df2) #10100, 16
To check for duplicates:
o df.duplicated returns a boolean series for each row to determine how many duplicate rows exist
o df.drop_duplicates() removes the duplicates to a new dataframe
Duplicate Entries Findings:
o Found and deleted 99 duplicate rows
Duplicate rows: 99

Duplicate rows preview:
       EmployeeNumber  Age  Tenure Turnover HourlyRate   HoursWeekly  \
10100               1   28       6      Yes     $24.37            40   
10101               2   33       2      Yes     $24.37            40   
10102               3   22       1       No     $22.52            40   
10103               4   23       1       No     $22.52            40   
10104               5   40       6       No     $88.77            40   

      CompensationType  AnnualSalary  DrivingCommuterDistance  \
10100           Salary       50689.6                       89   
10101           Salary       50689.6                       89   
10102           Salary       46841.6                       35   
10103           Salary       46841.6                       35   
10104           Salary      284641.6                       12   

                  JobRoleArea                Gender MaritalStatus  \
10100                Research                Female       Married   
10101                Research                Female       Married   
10102  Information_Technology                Female        Single   
10103  Information_Technology                Female        Single   
10104                   Sales  Prefer Not to Answer        Single   

       NumCompaniesPreviouslyWorked  AnnualProfessionalDevHrs PaycheckMethod  \
10100                           3.0                       7.0     Mail Check   
10101                           6.0                       7.0     Mail Check   
10102                           1.0                       8.0   Mailed Check   
10103                           3.0                       NaN   Mailed Check   
10104                           7.0                       NaN     Mail Check   

      TextMessageOptIn  
10100              Yes  
10101              Yes  
10102              Yes  
10103              Yes  
10104              Yes  
       EmployeeNumber  Age  Tenure Turnover HourlyRate   HoursWeekly  \
0                   1   28       6      Yes     $24.37            40   
1                   2   33       2      Yes     $24.37            40   
2                   3   22       1       No     $22.52            40   
3                   4   23       1       No     $22.52            40   
4                   5   40       6       No     $88.77            40   
...               ...  ...     ...      ...         ...          ...   
10095           10096   50      15      Yes     $61.78            40   
10096           10097   33       9      Yes     $23.28            40   
10097           10098   31       9      Yes     $28.25            40   
10098           10099   50      12       No     $32.22            40   
10099           10100   59      14       No     $44.59            40   

      CompensationType  AnnualSalary  DrivingCommuterDistance  \
0               Salary       50689.6                       89   
1               Salary       50689.6                       89   
2               Salary       46841.6                       35   
3               Salary       46841.6                       35   
4               Salary      284641.6                       12   
...                ...           ...                      ...   
10095           Salary      128502.4                        6   
10096           Salary       48422.4                      -10   
10097           Salary       37960.0                       68   
10098           Salary       67017.6                      -13   
10099           Salary       92747.2                       94   

                  JobRoleArea                Gender MaritalStatus  \
0                    Research                Female       Married   
1                    Research                Female       Married   
2      Information_Technology                Female        Single   
3      Information_Technology                Female        Single   
4                       Sales  Prefer Not to Answer        Single   
...                       ...                   ...           ...   
10095              Laboratory                  Male      Divorced   
10096               Marketing                  Male        Single   
10097              Laboratory                  Male       Married   
10098                Research                Female       Married   
10099                Research                  Male       Married   

       NumCompaniesPreviouslyWorked  AnnualProfessionalDevHrs  PaycheckMethod  \
0                               3.0                       7.0      Mail Check   
1                               6.0                       7.0      Mail Check   
2                               1.0                       8.0    Mailed Check   
3                               3.0                       NaN    Mailed Check   
4                               7.0                       NaN      Mail Check   
...                             ...                       ...             ...   
10095                           1.0                       8.0      Mail Check   
10096                           1.0                      20.0  Direct_Deposit   
10097                           2.0                      21.0   DirectDeposit   
10098                           5.0                      20.0  Direct_Deposit   
10099                           NaN                      10.0   DirectDeposit   

      TextMessageOptIn  
0                  Yes  
1                  Yes  
2                  Yes  
3                  Yes  
4                  Yes  
...                ...  
10095              Yes  
10096              Yes  
10097              NaN  
10098              Yes  
10099              NaN  

[10100 rows x 16 columns]
Inconsistent Entries
# Unique values per column
for col in df2.columns:
    unique_vals = df2[col].nunique()
    print(f"{col}: {unique_vals} unique values")
To check for inconsistent entries for qualitative variables:
EmployeeNumber: 10100 unique values
Age: 41 unique values
Tenure: 20 unique values
Turnover: 2 unique values
HourlyRate : 5244 unique values
HoursWeekly: 1 unique values
CompensationType: 1 unique values
AnnualSalary: 5538 unique values
DrivingCommuterDistance: 120 unique values
JobRoleArea: 12 unique values
Gender: 3 unique values
MaritalStatus: 3 unique values
NumCompaniesPreviouslyWorked: 9 unique values
AnnualProfessionalDevHrs: 21 unique values
PaycheckMethod: 7 unique values
TextMessageOptIn: 2 unique values
# Inconsistent categories
for col in df.select_dtypes(include='object').columns:
    print(f"\nColumn: {col}")
    print(df[col].value_counts(dropna=False).head(10))  # top 10 categories
Inconsistent Entries Findings:

Column: PaycheckMethod
PaycheckMethod
Mail Check        4986
Mailed Check      2441
DirectDeposit      992
Direct_Deposit     958
Mail_Check         547
Direct Deposit     226
MailedCheck         49
Name: count, dtype: int64
#Qualitative
# Normalize JobRoleArea
df3=df2.copy()
df3['JobRoleArea'] = df3['JobRoleArea'].astype(str).str.strip().str.title()

# Define mapping dictionary
mapping = {
    'Information Technology': 'Info_Tech',
    'Information_technology': 'Info_Tech',
    'Informationtechnology': 'Info_Tech',
    'Human Resources': 'Human_Resources',
    'HumanResources': 'Human_Resources'
}

# Apply mapping to a new column
df3['JobRole'] = df3['JobRoleArea'].map(mapping).fillna(df3['JobRoleArea'])
df3['JobRole'].value_counts(dropna=False)

#Quantitative
# Normalize PaycheckMethod
df3['PaycheckMethod'] = df3['PaycheckMethod'].astype(str).str.strip().str.title()

# Define mapping dictionary
mapping = {
    'Mail Check': 'Mailed_Check',
    'Mailed Check': 'Mailed_Check',
    'Mail_Check': 'Mailed_Check',
    'Mailedcheck': 'Mailed_Check',
    'Directdeposit': 'Direct_Deposit',
    'Direct Deposit': 'Direct_Deposit'
}

# Apply mapping to a new column
df3['PayMethod'] = df3['PaycheckMethod'].map(mapping).fillna(df3['PaycheckMethod'])
df3['PayMethod'].value_counts(dropna=False)

#drop old columns
df3.drop(['PaycheckMethod', 'JobRoleArea'], axis=1, inplace=True)
df3.info #10100x16
 
       AnnualProfessionalDevHrs TextMessageOptIn                 JobRole  \
0                           7.0              Yes                Research   
1                           7.0              Yes                Research   
2                           8.0              Yes  Information_Technology   
3                           NaN              Yes  Information_Technology   
4                           NaN              Yes                   Sales   
...                         ...              ...                     ...   
10095                       8.0              Yes              Laboratory   
10096                      20.0              Yes               Marketing   
10097                      21.0              NaN              Laboratory   
10098                      20.0              Yes                Research   
10099                      10.0              NaN                Research   

            PayMethod  
0        Mailed_Check  
1        Mailed_Check  
2        Mailed_Check  
3        Mailed_Check  
4        Mailed_Check  
...               ...  
10095    Mailed_Check  
10096  Direct_Deposit  
10097  Direct_Deposit  
10098  Direct_Deposit  
10099  Direct_Deposit  

[10100 rows x 16 columns]>
Quality Issue Findings
Inconsistent Entries• 
The column ‘JobRoleArea’ had multiple variations for entries ‘information technology’ and ‘human resources’
The column ‘PayCheckMethod’ had multiple variations for ‘Mailed_Check’ and ‘Direct Deposit’Do the same steps for ‘PayCheckMethod’ as ‘JobRoleArea’ to correct inconsistent entries
• Create a mapping dictionary to correct spacing, white space, and capitalization inconsistencies• Rename column and drop old column
﻿
Formatting Errors
To check for formatting errors:
o Df.describe returns negative ‘AnnualSalary’ and ‘DrivingCommuterDistance’
o Check for numeric columns stored as text, currency format, code consistency, and length checks
Formatting Errors Findings:
· Negative values were found for ‘Annual Salary’ and ‘DrivingCommuterDistance’
· ‘AnnualSalary’ was not formatted as currency
# Strip whitespace from column names
df3.columns = df3.columns.str.strip()

# Convert all numeric values to absolute (positive) values
df3[df3.select_dtypes(include='number').columns] = df3.select_dtypes(include='number').abs()

# Clean string columns: strip and title-case
for col in df3.select_dtypes(include='object').columns:
    df3[col] = df3[col].str.strip().str.title()

# inspect value counts across all columns
print(df3.value_counts(dropna=False))

# Clean and convert to float
df3['AnnualSalary'] = (df3['AnnualSalary'].astype(float)
)

# Format for display
df3['AnnualSalary'] = df3['AnnualSalary'].apply(lambda x: "${:,.2f}".format(x))
Out [143]:
EmployeeNumber  Age  Tenure  Turnover  HourlyRate  HoursWeekly  CompensationType  AnnualSalary  DrivingCommuterDistance  Gender  MaritalStatus  NumCompaniesPreviouslyWorked  AnnualProfessionalDevHrs  TextMessageOptIn  JobRole        PayMethod     
1               28   6       Yes       $24.37      40           Salary            50689.6       89                       Female  Married        3.0                           7.0                       Yes               Research       Mailed_Check      1
6738            37   7       No        $32.09      40           Salary            66747.2       52                       Male    Married        1.0                           21.0                      Yes               Info_Tech      Mailed_Check      1
6731            28   5       No        $23.33      40           Salary            48526.4       11                       Female  Divorced       1.0                           24.0                      NaN               Info_Tech      Mailed_Check      1
6732            52   15      Yes       $93.22      40           Salary            333897.6      53                       Female  Divorced       NaN                           NaN                       Yes               Manufacturing  Mailed_Check      1
6733            58   7       Yes       $94.53      40           Salary            336622.4      92                       Male    Married        6.0                           18.0                      Yes               Manufacturing  Mailed_Check      1
                                                                                                                                                                                                                                                          ..
3367            48   19      No        $92.51      40           Salary            332420.8      12                       Female  Single         7.0                           12.0                      NaN               Research       Mailed_Check      1
3368            28   4       Yes       $23.80      40           Salary            49504.0       71                       Female  Married        3.0                           10.0                      NaN               Sales          Mailed_Check      1
3369            55   17      Yes       $43.84      40           Salary            91287.2       44                       Male    Single         7.0                           17.0                      NaN               Marketing      Mailed_Check      1
3370            45   15      Yes       $71.11      40           Salary            147908.8      12                       Male    Single         4.0                           18.0                      No                Manufacturing  Direct_Deposit    1
10100           59   14      No        $44.59      40           Salary            92747.2       94                       Male    Married        NaN                           10.0                      NaN               Research       Direct_Deposit    1
Name: count, Length: 10100, dtype: int64
# Length checks
for col in df3.select_dtypes(include='object').columns:
    lengths = df3[col].str.len()
    print(f"{col} min length: {lengths.min()}, max length: {lengths.max()}")
Out [145]:
Turnover min length: 2, max length: 3
HourlyRate min length: 6, max length: 6
CompensationType min length: 6, max length: 6
AnnualSalary min length: 9, max length: 11
Gender min length: 4, max length: 20
MaritalStatus min length: 6, max length: 8
TextMessageOptIn min length: 2.0, max length: 3.0
JobRole min length: 5, max length: 22
PayMethod min length: 12, max length: 14
Formatting Errors Inspection:
# Strip whitespace from column names
df3.columns = df3.columns.str.strip()
# Convert all numeric values to absolute (positive) values
df3[df.select_dtypes(include=’number’).columns] = df.select_dtypes(include=’number’).abs()
# Clean string columns: strip and title-case
for col in df3.select_dtypes(include=’object’).columns:
df3[col] = df3[col].str.strip().str.title()
# inspect value counts across all columns
print(df3.value_counts(dropna=False))
B1 Missing Values
In [146]:
import numpy as np

# Step 1: Check total missing values
print("Total missing values:", df3.isna().sum().sum())

# Step 2: Check missing values per column
print("Missing values per column:\n", df3.isna().sum())

# Step 3: Compute integer means for numeric columns
numeric_means = df3.select_dtypes(include=[np.number]).mean().round().astype(int)

# Step 4: Fill NaN in numeric columns with their integer mean
df3.fillna(value=numeric_means, inplace=True)

# Step 5: Convert all numeric columns to integer dtype
for col in df3.select_dtypes(include=[np.number]).columns:
    df3[col] = df3[col].astype(int)

# Step 6: Verify results
print("Missing values after fill:\n", df3.isna().sum())
print("Data types after conversion:\n", df3.dtypes)

# Percentage missing
missing_pct = df3.isna().mean().round(4) * 100
print("\nMissing value percentage per column:")
print(missing_pct)
Out [146]:
Total missing values: 4868
Missing values per column:
 EmployeeNumber                     0
Age                                0
Tenure                             0
Turnover                           0
HourlyRate                         0
HoursWeekly                        0
CompensationType                   0
AnnualSalary                       0
DrivingCommuterDistance            0
Gender                             0
MaritalStatus                      0
NumCompaniesPreviouslyWorked     663
AnnualProfessionalDevHrs        1947
TextMessageOptIn                2258
JobRole                            0
PayMethod                          0
dtype: int64
Missing values after fill:
 EmployeeNumber                     0
Age                                0
Tenure                             0
Turnover                           0
HourlyRate                         0
HoursWeekly                        0
CompensationType                   0
AnnualSalary                       0
DrivingCommuterDistance            0
Gender                             0
MaritalStatus                      0
NumCompaniesPreviouslyWorked       0
AnnualProfessionalDevHrs           0
TextMessageOptIn                2258
JobRole                            0
PayMethod                          0
dtype: int64
Data types after conversion:
 EmployeeNumber                   int64
Age                              int64
Tenure                           int64
Turnover                        object
HourlyRate                      object
HoursWeekly                      int64
CompensationType                object
AnnualSalary                    object
DrivingCommuterDistance          int64
Gender                          object
MaritalStatus                   object
NumCompaniesPreviouslyWorked     int64
AnnualProfessionalDevHrs         int64
TextMessageOptIn                object
JobRole                         object
PayMethod                       object
dtype: object

Missing value percentage per column:
EmployeeNumber                   0.00
Age                              0.00
Tenure                           0.00
Turnover                         0.00
HourlyRate                       0.00
HoursWeekly                      0.00
CompensationType                 0.00
AnnualSalary                     0.00
DrivingCommuterDistance          0.00
Gender                           0.00
MaritalStatus                    0.00
NumCompaniesPreviouslyWorked     0.00
AnnualProfessionalDevHrs         0.00
TextMessageOptIn                22.36
JobRole                          0.00
PayMethod                        0.00
dtype: float64
In [147]:
df3.replace("", np.nan, inplace=True)   # turn empty strings into NaN
df3.fillna('NS', inplace=True)             # then replace NaN with 0 (or another value)
Outliers
To check for outliers:
o Assign a variable to numeric columns
o Calculate Q1, Q3 and IQR
o Define upper and lower bounds
o Flag outliers
o Combine both outliers
In [148]:
numeric_cols = df3.select_dtypes(include='number').columns
q1 = df3[numeric_cols].quantile(0.25)
q3 = df3[numeric_cols].quantile(0.75)
iqr = q3 - q1
lower_limit = q1 - 1.5 * iqr
upper_limit = q3 + 1.5 * iqr

# Flag outliers
low_outliers = (df3[numeric_cols] < lower_limit).any(axis=1)
high_outliers = (df3[numeric_cols] > upper_limit).any(axis=1)
outliers = df3[low_outliers | high_outliers]

# Totals
total_rows = df3.shape[0]
num_outliers = outliers.shape[0]
percent_outliers = (num_outliers / total_rows) * 100

# Column-level counts
outlier_counts = ((df3[numeric_cols] < lower_limit) | (df3[numeric_cols] > upper_limit)).sum()

# Build one summary table
summary_df = pd.DataFrame({
    "Q1": q1.abs(),
    "Q3": q3.abs(),
    "IQR": iqr.abs(),
    "Lower Limit": lower_limit.abs(),
    "Upper Limit": upper_limit.abs(),
    "Outlier Count": outlier_counts.abs()
})

# Print condensed summary
print(f"\n--- Outlier Summary ---")
print(f"Total rows: {total_rows} | Outlier rows: {num_outliers} ({percent_outliers:.2f}%)\n")
print(summary_df.sort_values("Outlier Count", ascending=False))
Out [148]:
--- Outlier Summary ---
Total rows: 10100 | Outlier rows: 222 (2.20%)

                                   Q1       Q3     IQR  Lower Limit  \
DrivingCommuterDistance         15.00    71.00    56.0         69.0   
EmployeeNumber                2525.75  7575.25  5049.5       5048.5   
Age                             37.00    53.00    16.0         13.0   
Tenure                           5.00    13.00     8.0          7.0   
HoursWeekly                     40.00    40.00     0.0         40.0   
NumCompaniesPreviouslyWorked     2.00     6.00     4.0          4.0   
AnnualProfessionalDevHrs        11.00    19.00     8.0          1.0   

                              Upper Limit  Outlier Count  
DrivingCommuterDistance             155.0            222  
EmployeeNumber                    15149.5              0  
Age                                  77.0              0  
Tenure                               25.0              0  
HoursWeekly                          40.0              0  
NumCompaniesPreviouslyWorked         12.0              0  
AnnualProfessionalDevHrs             31.0              0
Out [149]:
In [150]:
import seaborn as sns
import matplotlib.pyplot as plt
commuter = df3

column_name = df3['DrivingCommuterDistance']
df_commuter=pd.DataFrame(commuter,columns=column_name)

sns.boxplot(data=df3, x= column_name)
plt.show()
This image has an empty alt attribute; its file name is image.png
out [150]:
In [151]:
import numpy as np
import matplotlib.pyplot as plt

outlier_indices = np.where((df3['DrivingCommuterDistance'] >= 155) & (df3['DrivingCommuterDistance'] <= 69))

no_outliers = df3.drop(outlier_indices[0])

fig, ax_no_outliers = plt.subplots(figsize=(6, 4))
ax_no_outliers.scatter(no_outliers['DrivingCommuterDistance'], no_outliers['DrivingCommuterDistance'])
ax_no_outliers.set_xlabel('(Lower_Distance)')
ax_no_outliers.set_ylabel('(Higher_Distance) )')
plt.show()
This image has an empty alt attribute; its file name is 1*UvvldSPG90bYRC9D-9JK3Q.png
Outliers Findings:
· Q1 — First Quartile/25th Percentile:
o 25% of employees are younger than 37 years, earn less than $63,440, and commute less than 13 miles.
· Q3 — Third Quartile/75th Percentile:
o 75% of employees are younger than 53 years, earn less than $153,717, and commute less than 71 miles.
· IQR — Interquartile Range:
o The central salary range spans $90,277.20
· Lower Limit:
o Salaries below $71,975.80 are potential outliers
· Upper Limit:
o Salaries above $289,133.00 are potential outliers
Save new cleaned csv file
In [152]:
df3.to_csv('Employee_Turnover_Cleaned10.csv', index=False)
import os
print(os.getcwd())
Out [152]:
/Users/meredithsmith/PycharmProjects/PythonProject/PythonProject/PythonProject44
In [153]:print(df3.head)
Out [153]:
<bound method NDFrame.head of        EmployeeNumber  Age  Tenure Turnover HourlyRate  HoursWeekly  \
0                   1   28       6      Yes     $24.37           40   
1                   2   33       2      Yes     $24.37           40   
2                   3   22       1       No     $22.52           40   
3                   4   23       1       No     $22.52           40   
4                   5   40       6       No     $88.77           40   
...               ...  ...     ...      ...        ...          ...   
10095           10096   50      15      Yes     $61.78           40   
10096           10097   33       9      Yes     $23.28           40   
10097           10098   31       9      Yes     $28.25           40   
10098           10099   50      12       No     $32.22           40   
10099           10100   59      14       No     $44.59           40   

      CompensationType AnnualSalary  DrivingCommuterDistance  \
0               Salary   $50,689.60                       89   
1               Salary   $50,689.60                       89   
2               Salary   $46,841.60                       35   
3               Salary   $46,841.60                       35   
4               Salary  $284,641.60                       12   
...                ...          ...                      ...   
10095           Salary  $128,502.40                        6   
10096           Salary   $48,422.40                       10   
10097           Salary   $37,960.00                       68   
10098           Salary   $67,017.60                       13   
10099           Salary   $92,747.20                       94   

                     Gender MaritalStatus  NumCompaniesPreviouslyWorked  \
0                    Female       Married                             3   
1                    Female       Married                             6   
2                    Female        Single                             1   
3                    Female        Single                             3   
4      Prefer Not To Answer        Single                             7   
...                     ...           ...                           ...   
10095                  Male      Divorced                             1   
10096                  Male        Single                             1   
10097                  Male       Married                             2   
10098                Female       Married                             5   
10099                  Male       Married                             4   

       AnnualProfessionalDevHrs TextMessageOptIn                 JobRole  \
0                             7              Yes                Research   
1                             7              Yes                Research   
2                             8              Yes  Information_Technology   
3                            15              Yes  Information_Technology   
4                            15              Yes                   Sales   
...                         ...              ...                     ...   
10095                         8              Yes              Laboratory   
10096                        20              Yes               Marketing   
10097                        21               NS              Laboratory   
10098                        20              Yes                Research   
10099                        10               NS                Research   

            PayMethod  
0        Mailed_Check  
1        Mailed_Check  
2        Mailed_Check  
3        Mailed_Check  
4        Mailed_Check  
...               ...  
10095    Mailed_Check  
10096  Direct_Deposit  
10097  Direct_Deposit  
10098  Direct_Deposit  
10099  Direct_Deposit  

[10100 rows x 16 columns]>
C. Data Cleaning Techniques Used to Correct Data Quality Issues
1. Dataset Modification Description and Explanation with Python
Duplicates Modification: Identified and dropped 99 unnecessary rows
Why This Data Cleaning Technique for Duplicates?
o Duplicates can skew the outcome and lead to data inaccuracy. Identifying and removing duplicates ensures that each record is unique and accurate.
Missing Values Modification:
o Replaced missing numerical data with the mean
o Replaced missing categorical data with ‘NS’
Why This Data Cleaning Technique for Missing Values?
o Minimizes data skew across numerical variables by providing the mean for missing data
o Creates consistency for missing categorical data
Inconsistent Entries Modification:
o Reduced variations in PayCheckMethod and JobRoleAreas columns
o Normalized categorical values
o Create a mapping dictionary to correct spacing, white space, and capitalization inconsistencies
o Rename column and drop old column
o Assign variables to allowed and unallowed values for each variable
o Replace inconsistent values by creating a dictionary with reverse mapping
o Filter to return only the consistent entries
o Df3[‘JobRoleArea’].astype(str).str.strip().str.title() converts all values in JobRoleArea to strings, removes leading and trailing whitespace from each string, and converts the string to title case
Why This Data Cleaning Technique for Inconsistent Entries?
o Increases consistency and uniformity in data representation
Formatting Errors Modification:
o Changed data type, eliminated white spaces, fixed capitalization
o Converted monetary columns to currency for consistency
Why This Data Cleaning Technique for Formatting Errors?
o Formatting errors maintain data consistency in order to avoid breaking analysis, distorting results, or code failure
Outliers Modification:
o Identified values that could negatively influence data, whether they are erroneous, extenuating, or exceptional circumstances
o Used IQR and left the outliers as is after converting to absolute value
Why This Data Cleaning Technique for Outliers?
o IQR is a robust measure of spread that isnt distorted by extreme values, defines clear boundaries, and is simple and visual
2. Choosing Specific Data Cleaning
These data cleaning techniques were chosen through data profiling. After making a data structure assessment, data quality assessment, and relationship discovery, it was clear how the data needed to be cleaned (Western Governors University, 2025). The pre-analysis helps in understanding the dataset and determining which data cleaning techniques to execute.
This consists of looking at:
· Source of the dataset for bias that could affect data quality or reliability,
· Context of the data
· How many different variables exist
· How many different categories are within each variable
· Summary statistics for each column
· Plotting variables
· Looking closely at the relationships if the dataset is relational
· Possible using the profiling feature of the pandas library
(DataCamp, 2024)
3. Describe two advantages of your data cleaning approach specified in part C1.
Duplicate Removal: One advantage is that the removal of 99 duplicate rows increases data accuracy and reduces redundancy. By eliminating duplicate records, the dataset more accurately reflects the underlying information, thereby preventing skewed results caused by repetitive values. This ensures that statistical summaries, such as averages or counts, are not artificially inflated. In practice, removing duplicates strengthens the reliability of insights, supports cleaner reporting, and reduces the risk of misleading conclusions in decision-making processes.
Consistency and Standardization: Another advantage is that reducing inconsistent entries and formatting errors streamlines data analysis, allowing for better accessibility. When formats are standardized — such as consistent date structures, uniform text casing, or aligned categorical labels — analysts can more easily query, filter, and merge data without additional cleaning steps. This not only saves time but also enhances the usability of the dataset across different teams and tools. For organizations, standardized data improves collaboration, supports accurate reporting, and lays the foundation for scalable analytics and automation.
4. Discuss two limitations to your data cleaning approach specified in part C1.
Imputation: A limitation of my data cleaning method is that replacing missing numerical values with the mean assumes normal distribution. If the column is skewed, the mean may distort the distribution. Additionally, replacing empty values with the same mean reduces variance. In columns ‘AnnualProfessionalDevHrs’ and ‘NumCompaniesPreviouslyWorked’, it is possible that these missing values could be 0. If these values were indeed 0, this would result in the loss of original data context, skewed data, and the introduction of bias. To ensure transparency, this data imputation process must be well-documented.
Uncapped Outliers: Another limitation of my data cleaning approach is that I did not cap or remove the outliers for ‘DrivingCommuterDistance’, which accounted for 2% of the values. These extreme values may disproportionately influence statistical measures such as the mean and standard deviation, potentially skewing the results of any analysis that relies on them. By leaving the outliers unaddressed, the model may misrepresent typical commuting behavior, reduce the accuracy of predictive insights, and introduce bias in downstream calculations. A more robust approach would involve applying techniques such as winsorization, z‑score filtering, or interquartile range (IQR) trimming to mitigate the impact of these anomalies while preserving the integrity of the dataset.
This image has an empty alt attribute; its file name is 1*2FvIbT307CQnvoqexFiUXQ.png
This image has an empty alt attribute; its file name is 1*z103Nz6SkHHA3ToLBhA87g.png
D599_Task_1Download
https://gitlab.com/wgu-gitlab-environment/student-repos/msmit256/d598-analytics-programming/-/blob/PA3Viz/D598_Data_Set.xlsx?ref_type=heads
Employee_Turnover_Cleaned10.csv
https://wgu.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=c62e58ae-8745-4d06-b6bd-b39f0130c611
