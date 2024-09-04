# Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output
## Reading the given data
```
import pandas as pd
import numpy as np
df = pd.read_csv('SAMPLEIDS.csv')
df
```
![Screenshot 2024-09-04 182308](https://github.com/user-attachments/assets/b1c1107f-03b5-4d13-9a91-a6ff00cb096f)

## Getting information of data
```
df.describe()
```
![Screenshot 2024-09-04 182430](https://github.com/user-attachments/assets/3d3a8b1c-aa79-4c52-b587-2ec1873de3e2)

```
df.info()
```
![Screenshot 2024-09-04 182526](https://github.com/user-attachments/assets/80c8e4c5-e10e-4a57-baf7-8035a60d73b7)

```
df.head()
```
![Screenshot 2024-09-04 182624](https://github.com/user-attachments/assets/1dbf0747-5623-49ba-b142-4cae38c4f748)

```
df.tail()
```
![Screenshot 2024-09-04 182701](https://github.com/user-attachments/assets/e6755c1d-71b0-485c-927e-130c13c93235)

## Removing NULL values from the data
```
df.isnull()
```
![Screenshot 2024-09-04 182937](https://github.com/user-attachments/assets/7272fff1-b1f9-4451-a97e-4611eeced4b8)

```
df.isnull().sum()
```
![Screenshot 2024-09-04 183026](https://github.com/user-attachments/assets/e57c06dc-d802-44be-9378-6a2142cca52c)

```
df.isnull().any()
```
![Screenshot 2024-09-04 183114](https://github.com/user-attachments/assets/a83e802c-b3c7-4ce9-a147-8b268353f83a)

```
df.dropna(axis=0)
```
![Screenshot 2024-09-04 183152](https://github.com/user-attachments/assets/a2c03ef9-4e7f-472c-aea7-6f0c832de76b)

## Removing outlier using IQR
```
import sea as sns
pf=pd.read_csv("height.csv")
pf
```
![Screenshot 2024-09-04 183404](https://github.com/user-attachments/assets/9cd7a08f-3cce-40ea-b1bd-79c1bd588aa5)

```
sns.boxplot(data=pf)
```
![Screenshot 2024-09-04 183521](https://github.com/user-attachments/assets/cd9e95b1-8a88-4a63-aaa4-7739371b8972)

```
sns.scatterplot(data=pf)
```
![Screenshot 2024-09-04 183521](https://github.com/user-attachments/assets/4d57999b-7693-4f67-8c92-a9a35300382e)

```
Q1 = pf['height'].quantile(0.25)
Q3 = pf['height'].quantile(0.75)
IQR = Q3 - Q1
LB = Q1 - 1.5 * IQR
UB = Q3 + 1.5 * IQR

outliers = pf[(pf['height'] < LB) | (pf['height'] > UB)]

print("Lower Bound:", LB)
print("Upper Bound:", UB)
print("Outliers:\n", outliers)
```
![Screenshot 2024-09-04 183645](https://github.com/user-attachments/assets/6e729b28-143e-4791-86ce-1190d66bd5b8)

```
no_outliers = pf[~((pf['height'] < LB) | (pf['height'] > UB))]
print(no_outliers)
```
![Screenshot 2024-09-04 183730](https://github.com/user-attachments/assets/e26c228b-b5d2-40ac-8b34-74bdb38be0ca)

```
sns.boxplot(data=no_outliers)
```
![Screenshot 2024-09-04 183803](https://github.com/user-attachments/assets/b91636fe-d1cf-4d88-816a-12d032b9a220)

```
sns.scatterplot(data=no_outliers)
```
![Screenshot 2024-09-04 183832](https://github.com/user-attachments/assets/c1cbc4e5-119f-4273-a7f8-dd1ba0d22f45)

## REMOVING OUTLIERS OF THE SAME DATA USING Z SCORE
```
import matplotlib.pyplot as plt
import scipy.stats as stats
pf
```
![Screenshot 2024-09-04 183911](https://github.com/user-attachments/assets/53ab5ebf-6220-49b3-b2d9-1b365287c429)

```
q1=pf['height'].quantile(0.25)
q2=pf['height'].quantile(0.5)
q3=pf['height'].quantile(0.75)

iqr=q3-q1
low= q1-1.5*iqr
high=q3+1.5*iqr

pf1=pf[((pf['height'] >= low) & (pf['height'] <= high))]
pf1
```
![Screenshot 2024-09-04 184004](https://github.com/user-attachments/assets/329f461c-3cdf-429c-89a5-737a50ece417)

```
z=np.abs(stats.zscore(pf['height']))
z
```
![Screenshot 2024-09-04 184004](https://github.com/user-attachments/assets/e7894b70-e34e-4322-b401-b15e022e83e1)

```
pf1 = pf[z<3]
pf1
```
![Screenshot 2024-09-04 184004](https://github.com/user-attachments/assets/3b4c5132-7f72-414a-a568-066395c56279)

# Result
Thus we have cleaned the data and removed the outliers by detection using IQR and Z-score method
