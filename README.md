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

```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
data = pd.read_csv("/content/SAMPLEIDS.csv")
data.head()
```
![image](https://github.com/varshxnx/exno1ds/assets/122253525/39fcfa9a-3784-46db-ae7f-568d33f3a4aa)

```
data = pd.get_dummies(data)
data.isnull().sum()
```
![image](https://github.com/varshxnx/exno1ds/assets/122253525/9f8dbfe6-e3c0-4fab-aee3-954ad5fa137f)

```
columns_with_null = data.columns[data.isnull().any()]
import seaborn as sns
plt.figure(figsize=(10,10))
sns.barplot(columns_with_null)
plt.title("NULL VALUES")
plt.show()
```
![image](https://github.com/varshxnx/exno1ds/assets/122253525/f0b728a1-b026-4e94-9f58-30892c8b1c74)

```
for column in columns_with_null:
    median = data[column].median()  
    data[column].fillna(median, inplace=True)
data.isnull().sum().sum()
```
![image](https://github.com/varshxnx/exno1ds/assets/122253525/1b350042-cc6f-4a02-96f6-c3f9aae27625)


## IQR
```
import pandas as pd
import seaborn as sns
ir = pd.read_csv("/content/iris (1).csv")
ir.head()
```
![image](https://github.com/varshxnx/exno1ds/assets/122253525/69f8e9cf-dee9-4624-be38-2125a8141a41)

```
ir.describe()
```
![image](https://github.com/varshxnx/exno1ds/assets/122253525/3108e919-7d6f-4c24-ad8d-6a119fe7f69b)

```
sns.boxplot(x='sepal_width',data=ir)
```
![image](https://github.com/varshxnx/exno1ds/assets/122253525/7319774f-ee57-41a0-a5d6-d61252b9f48d)

```
c1=ir.sepal_width.quantile(0.25)
c3=ir.sepal_width.quantile(0.75)
iq=c3-c1
print(c3)
```
![image](https://github.com/varshxnx/exno1ds/assets/122253525/bcec41dd-05e5-4a22-8c0c-bb851b5c94f2)

```
rid=ir[((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
rid['sepal_width']
```
![image](https://github.com/varshxnx/exno1ds/assets/122253525/95f00e8a-51af-46de-9b0e-f9286b7fd965)

```
delid=ir[~((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
delid
```
![image](https://github.com/varshxnx/exno1ds/assets/122253525/fa860947-8c62-4f58-8bf1-c4ee3e02b3cd)

```
sns.boxplot(x='sepal_width',data=delid)
```
![image](https://github.com/varshxnx/exno1ds/assets/122253525/7ed64f50-d259-4d1c-955e-207e7cdb0b36)


## Z SCORE
```
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import scipy.stats as stats
dataset=pd.read_csv("/content/heights.csv")
dataset
```
![image](https://github.com/varshxnx/exno1ds/assets/122253525/5cfe76e4-395f-4cad-b8ac-8cd5192db7d4)

```
df = pd.read_csv("heights.csv")
q1 = df['height'].quantile(0.25)
q2 = df['height'].quantile(0.5)
q3 = df['height'].quantile(0.75)
```
```
iqr = q3-q1
iqr
```
![image](https://github.com/varshxnx/exno1ds/assets/122253525/29084c47-bfbe-425d-bc93-245eb1eed4ab)

low = q1 - 1.5*iqr
low
```
![image](https://github.com/varshxnx/exno1ds/assets/122253525/19e6066d-ef27-4049-a93f-7bd1df06633f)

```
high = q3 + 1.5*iqr
high
```
![image](https://github.com/varshxnx/exno1ds/assets/122253525/c7625ca0-6739-48dd-a59d-c38889a01580)

```
df1 = df[((df['height'] >=low)& (df['height'] <=high))]
df1
```
![image](https://github.com/varshxnx/exno1ds/assets/122253525/78cc2be6-bc3e-40e9-8291-5032adaad95e)

```
z = np.abs(stats.zscore(df['height']))
z
```
![image](https://github.com/varshxnx/exno1ds/assets/122253525/3bec7e24-556d-4e84-a59f-3073116dd2fb)


# Result
Thus the outliers are detected and removed in the given file and the final data set is saved into the file.
