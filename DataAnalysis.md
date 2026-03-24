```python
pip install pandas numpy matplotlib seaborn openpyxl
```

    Requirement already satisfied: pandas in c:\users\gr0001\anaconda3\lib\site-packages (2.3.3)
    Requirement already satisfied: numpy in c:\users\gr0001\anaconda3\lib\site-packages (2.3.5)
    Requirement already satisfied: matplotlib in c:\users\gr0001\anaconda3\lib\site-packages (3.10.6)
    Requirement already satisfied: seaborn in c:\users\gr0001\anaconda3\lib\site-packages (0.13.2)
    Requirement already satisfied: openpyxl in c:\users\gr0001\anaconda3\lib\site-packages (3.1.5)
    Requirement already satisfied: python-dateutil>=2.8.2 in c:\users\gr0001\anaconda3\lib\site-packages (from pandas) (2.9.0.post0)
    Requirement already satisfied: pytz>=2020.1 in c:\users\gr0001\anaconda3\lib\site-packages (from pandas) (2025.2)
    Requirement already satisfied: tzdata>=2022.7 in c:\users\gr0001\anaconda3\lib\site-packages (from pandas) (2025.2)
    Requirement already satisfied: contourpy>=1.0.1 in c:\users\gr0001\anaconda3\lib\site-packages (from matplotlib) (1.3.3)
    Requirement already satisfied: cycler>=0.10 in c:\users\gr0001\anaconda3\lib\site-packages (from matplotlib) (0.11.0)
    Requirement already satisfied: fonttools>=4.22.0 in c:\users\gr0001\anaconda3\lib\site-packages (from matplotlib) (4.60.1)
    Requirement already satisfied: kiwisolver>=1.3.1 in c:\users\gr0001\anaconda3\lib\site-packages (from matplotlib) (1.4.9)
    Requirement already satisfied: packaging>=20.0 in c:\users\gr0001\anaconda3\lib\site-packages (from matplotlib) (25.0)
    Requirement already satisfied: pillow>=8 in c:\users\gr0001\anaconda3\lib\site-packages (from matplotlib) (12.0.0)
    Requirement already satisfied: pyparsing>=2.3.1 in c:\users\gr0001\anaconda3\lib\site-packages (from matplotlib) (3.2.5)
    Requirement already satisfied: et-xmlfile in c:\users\gr0001\anaconda3\lib\site-packages (from openpyxl) (2.0.0)
    Requirement already satisfied: six>=1.5 in c:\users\gr0001\anaconda3\lib\site-packages (from python-dateutil>=2.8.2->pandas) (1.17.0)
    Note: you may need to restart the kernel to use updated packages.
    


```python

```


```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

```


```python
#load Datasets
import pandas as pd
df = pd.read_csv(r"C:\\Users\\GR0001\\Documents\\customer_churn_dataset.csv")
```


```python
#Display Basic Info
print(df.head())
print(df.info())
```

      Customer_ID  Gender  Age Region  Tenure_Months Subscription_Type  \
    0   CUST00001  Female   19   East             36          Standard   
    1   CUST00002  Female   20  North             59             Basic   
    2   CUST00003  Female   65   East             41             Basic   
    3   CUST00004    Male   24   East             12          Standard   
    4   CUST00005  Female   60   East             35          Standard   
    
       Monthly_Charges  Total_Charges Payment_Method Contract_Type  Support_Calls  \
    0          1868.92       67281.12            UPI       Monthly             10   
    1          1474.22       86978.98            UPI        Yearly              3   
    2          1252.85       51366.85           Cash        Yearly              8   
    3          1376.04       16512.48           Card        Yearly             10   
    4           846.62       29631.70           Card     Quarterly              5   
    
       Last_Activity_Days  Churn  
    0                   1      1  
    1                   7      0  
    2                  59      1  
    3                  40      1  
    4                   9      0  
    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 15000 entries, 0 to 14999
    Data columns (total 13 columns):
     #   Column              Non-Null Count  Dtype  
    ---  ------              --------------  -----  
     0   Customer_ID         15000 non-null  object 
     1   Gender              15000 non-null  object 
     2   Age                 15000 non-null  int64  
     3   Region              15000 non-null  object 
     4   Tenure_Months       15000 non-null  int64  
     5   Subscription_Type   15000 non-null  object 
     6   Monthly_Charges     15000 non-null  float64
     7   Total_Charges       15000 non-null  float64
     8   Payment_Method      15000 non-null  object 
     9   Contract_Type       15000 non-null  object 
     10  Support_Calls       15000 non-null  int64  
     11  Last_Activity_Days  15000 non-null  int64  
     12  Churn               15000 non-null  int64  
    dtypes: float64(2), int64(5), object(6)
    memory usage: 1.5+ MB
    None
    


```python
print(df.info())
print(df.describe())

```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 15000 entries, 0 to 14999
    Data columns (total 13 columns):
     #   Column              Non-Null Count  Dtype  
    ---  ------              --------------  -----  
     0   Customer_ID         15000 non-null  object 
     1   Gender              15000 non-null  object 
     2   Age                 15000 non-null  int64  
     3   Region              15000 non-null  object 
     4   Tenure_Months       15000 non-null  int64  
     5   Subscription_Type   15000 non-null  object 
     6   Monthly_Charges     15000 non-null  float64
     7   Total_Charges       15000 non-null  float64
     8   Payment_Method      15000 non-null  object 
     9   Contract_Type       15000 non-null  object 
     10  Support_Calls       15000 non-null  int64  
     11  Last_Activity_Days  15000 non-null  int64  
     12  Churn               15000 non-null  int64  
    dtypes: float64(2), int64(5), object(6)
    memory usage: 1.5+ MB
    None
                    Age  Tenure_Months  Monthly_Charges  Total_Charges  \
    count  15000.000000   15000.000000     15000.000000   15000.000000   
    mean      41.484200      36.287200      1104.574543   40246.726282   
    std       13.794764      20.810129       522.996570   31942.896536   
    min       18.000000       1.000000       200.110000     201.910000   
    25%       30.000000      18.000000       648.182500   14382.855000   
    50%       42.000000      36.000000      1108.150000   31476.905000   
    75%       53.000000      54.000000      1554.295000   59838.585000   
    max       65.000000      72.000000      1999.800000  143832.960000   
    
           Support_Calls  Last_Activity_Days         Churn  
    count   15000.000000        15000.000000  15000.000000  
    mean        5.004133           30.440000      0.813600  
    std         3.165752           17.346886      0.389442  
    min         0.000000            1.000000      0.000000  
    25%         2.000000           16.000000      1.000000  
    50%         5.000000           30.000000      1.000000  
    75%         8.000000           45.000000      1.000000  
    max        10.000000           60.000000      1.000000  
    


```python
print(df.isnull().sum())
```

    Customer_ID           0
    Gender                0
    Age                   0
    Region                0
    Tenure_Months         0
    Subscription_Type     0
    Monthly_Charges       0
    Total_Charges         0
    Payment_Method        0
    Contract_Type         0
    Support_Calls         0
    Last_Activity_Days    0
    Churn                 0
    dtype: int64
    


```python
df.drop_duplicates(inplace=True)
```


```python
print("First 5 rows:")
print(df.head())
```

    First 5 rows:
      Customer_ID  Gender  Age Region  Tenure_Months Subscription_Type  \
    0   CUST00001  Female   19   East             36          Standard   
    1   CUST00002  Female   20  North             59             Basic   
    2   CUST00003  Female   65   East             41             Basic   
    3   CUST00004    Male   24   East             12          Standard   
    4   CUST00005  Female   60   East             35          Standard   
    
       Monthly_Charges  Total_Charges Payment_Method Contract_Type  Support_Calls  \
    0          1868.92       67281.12            UPI       Monthly             10   
    1          1474.22       86978.98            UPI        Yearly              3   
    2          1252.85       51366.85           Cash        Yearly              8   
    3          1376.04       16512.48           Card        Yearly             10   
    4           846.62       29631.70           Card     Quarterly              5   
    
       Last_Activity_Days  Churn  
    0                   1      1  
    1                   7      0  
    2                  59      1  
    3                  40      1  
    4                   9      0  
    


```python
print("\nDataset Info:")
print(df.info())
```

    
    Dataset Info:
    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 15000 entries, 0 to 14999
    Data columns (total 13 columns):
     #   Column              Non-Null Count  Dtype  
    ---  ------              --------------  -----  
     0   Customer_ID         15000 non-null  object 
     1   Gender              15000 non-null  object 
     2   Age                 15000 non-null  int64  
     3   Region              15000 non-null  object 
     4   Tenure_Months       15000 non-null  int64  
     5   Subscription_Type   15000 non-null  object 
     6   Monthly_Charges     15000 non-null  float64
     7   Total_Charges       15000 non-null  float64
     8   Payment_Method      15000 non-null  object 
     9   Contract_Type       15000 non-null  object 
     10  Support_Calls       15000 non-null  int64  
     11  Last_Activity_Days  15000 non-null  int64  
     12  Churn               15000 non-null  int64  
    dtypes: float64(2), int64(5), object(6)
    memory usage: 1.5+ MB
    None
    


```python
duplicates = df.duplicated().sum()
print(f"\nDuplicate rows: {duplicates}")
```

    
    Duplicate rows: 0
    


```python
#WHAT IS OVERALL CHURN RATE
churn_rate = df['Churn'].mean() * 100
print("Churn Rate:", churn_rate)
```

    Churn Rate: 81.36
    


```python
#How many Customer churned vs retained
print(df['Churn'].value_counts())
```

    Churn
    1    12204
    0     2796
    Name: count, dtype: int64
    


```python
#Churn rate by Contract type
df.groupby('Contract_Type')['Churn'].mean()*100
```




    Contract_Type
    monthly      100.000000
    quarterly     72.407083
    yearly        71.773863
    Name: Churn, dtype: float64




```python
#Does Support Calls Affect Churn
df.groupby('Support_Calls')['Churn'].mean()
```




    Support_Calls
    0     0.669361
    1     0.676790
    2     0.656297
    3     0.669297
    4     0.643594
    5     0.640860
    6     1.000000
    7     1.000000
    8     1.000000
    9     1.000000
    10    1.000000
    Name: Churn, dtype: float64




```python
#High Risk Customer (Important)
high_risk = df[(df['Support_Calls'] > 5) & (df['Last_Activity_Days'] > 30)]
print(high_risk.head())
```

       Customer_ID  Gender  Age Region  Tenure_Months Subscription_Type  \
    2    CUST00003  Female   65   East             41             Basic   
    3    CUST00004    Male   24   East             12          Standard   
    5    CUST00006  Female   18   West             36             Basic   
    10   CUST00011    Male   18  North             30             Basic   
    19   CUST00020    Male   25  South             12           Premium   
    
        Monthly_Charges  Total_Charges Payment_Method Contract_Type  \
    2           1252.85       51366.85           cash        yearly   
    3           1376.04       16512.48           card        yearly   
    5           1723.06       62030.16           cash     quarterly   
    10          1832.17       54965.10            upi        yearly   
    19           646.64        7759.68           cash       monthly   
    
        Support_Calls  Last_Activity_Days  Churn  
    2               8                  59      1  
    3              10                  40      1  
    5               8                  51      1  
    10              9                  43      1  
    19              7                  35      1  
    


```python
#Revenue Lost Due To Churn
revenue_loss = df[df['Churn'] == 1]['Total_Charges'].sum()
print("Revenue Loss:", revenue_loss)
```

    Revenue Loss: 491711568.37
    


```python
#Churn by Region
df.groupby('Region',observed=False)['Churn'].mean() * 100
```




    Region
    East     81.856990
    North    81.406080
    South    79.707057
    West     82.454760
    Name: Churn, dtype: float64




```python
#Average monthly charges
df.groupby('Churn')['Monthly_Charges'].mean()
```




    Churn
    0    1103.646170
    1    1104.787239
    Name: Monthly_Charges, dtype: float64




```python
#Churn by Region
df.groupby('Region',observed=True)['Churn'].mean() * 100
```




    Region
    East     81.856990
    North    81.406080
    South    79.707057
    West     82.454760
    Name: Churn, dtype: float64


