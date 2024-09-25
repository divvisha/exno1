# Exno:1 Data Cleaning Process

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

   ~~~
   import pandas as pd
   df=pd.read_csv("/content/SAMPLEIDS.csv")
   df
   ~~~
   ![Screenshot 2024-09-25 101714](https://github.com/user-attachments/assets/514e7e0b-34c0-44e6-805c-c140dfcceb93)
   ~~~
   df.shape
~~~
   ![Screenshot 2024-09-25 101806](https://github.com/user-attachments/assets/af5098d4-b7f8-4d52-ad9e-83aae485dd1c)
   ~~~
   df.describe()
~~~
   ![Screenshot 2024-09-25 101842](https://github.com/user-attachments/assets/1eeb3999-4e42-430c-8310-2acf6a0c6ba3)
   ~~~
   df.info()
~~~
   ![Screenshot 2024-09-25 101911](https://github.com/user-attachments/assets/e5f3b23f-de92-4f89-aa8f-a52e34000e9a)
~~~
   df.head(3)
   df.tail(3)
~~~
   ![Screenshot 2024-09-25 101946](https://github.com/user-attachments/assets/a0fce84f-5c78-4bdd-8aa4-aa12d59c67c5)
   ~~~
   df.isnull().sum()
   ~~~
   ![Screenshot 2024-09-25 102021](https://github.com/user-attachments/assets/345a0c64-e125-4996-b289-35d4ddbea226)
   ~~~
   df.dropna(how='any').shape
~~~
   ![Screenshot 2024-09-25 102427](https://github.com/user-attachments/assets/00fbc1ec-99cd-4f5a-ba37-956ce9db1ffb)
~~~
   df.shape
~~~
   ![Screenshot 2024-09-25 102502](https://github.com/user-attachments/assets/59ab9325-ac1b-40e7-a009-b8dc88aa0e7f)
   ~~~
   x=df.dropna(how='any')
   x
   ~~~
   ![Screenshot 2024-09-25 102705](https://github.com/user-attachments/assets/6f39f743-b400-425c-9b2a-7321339dfba1)
   ~~~
   x2=df.dropna(how='all').shape
   mn=df.TOTAL.mean()
   mn
~~~
   ![Screenshot 2024-09-25 102756](https://github.com/user-attachments/assets/aa5a00b2-c03c-4e39-b1c7-0e1ebd454a9b)
   ~~~
   df.TOTAL.fillna(mn,inplace=True)
   df
~~~
   ![Screenshot 2024-09-25 102843](https://github.com/user-attachments/assets/97dccd07-fb31-419c-b7ad-e1c014833a64)
   ~~~
   df['M1']
~~~
   ![Screenshot 2024-09-25 102925](https://github.com/user-attachments/assets/851aabcc-1d34-4da5-b1c6-76ad0d5ee914)
   ~~~
   l=df.M1.interpolate()
   l
~~~
   ![Screenshot 2024-09-25 103005](https://github.com/user-attachments/assets/fe8d32da-65d4-4840-ba08-4759b4645081)
   ~~~
   df.M1.fillna(method='FFill',inplace=True)
~~~
   ![Screenshot 2024-09-25 103042](https://github.com/user-attachments/assets/0969e621-90f8-4eac-99c0-a986b033a988)
   ~~~
   df.isna().sum()
~~~
   ![Screenshot 2024-09-25 103117](https://github.com/user-attachments/assets/a723760a-2687-4d0a-8a4f-6dbc54c83065)
   ~~~
   df.duplicated()
~~~
   ![Screenshot 2024-09-25 103156](https://github.com/user-attachments/assets/cdc5f6c5-6ac3-425e-a5d0-7ea0cced5085)
   ~~~
   df.drop_duplicates(inplace=True)
   df.duplicated()
~~~
   ![Screenshot 2024-09-25 103250](https://github.com/user-attachments/assets/ea9affc3-f18b-4e96-991a-87fad6b39552)
   ~~~
   import seaborn as sns
   sns.heatmap(df.isnull(),yticklabels=False, annot=True)
~~~
   ![Screenshot 2024-09-25 103458](https://github.com/user-attachments/assets/4e337176-fd19-4bf1-97ca-0b947c004d7c)
   ~~~
   df.dropna(inplace=True)
   sns.heatmap(df.isnull(),yticklabels=False, annot=True)
~~~
   ![Screenshot 2024-09-25 103600](https://github.com/user-attachments/assets/e748141e-3d20-4a18-8c65-42f0a6b48acc)
   ~~~
   df['DOB']
~~~
   ![Screenshot 2024-09-25 103651](https://github.com/user-attachments/assets/7700627c-cd9d-4099-8260-c1b2552eb01a)
   ~~~
   import numpy as np
   age=[1,3,28,27,25,92,30,39,40,50,26,24,29,94]
   af=pd.DataFrame(age)
   af
~~~
   ![Screenshot 2024-09-25 104003](https://github.com/user-attachments/assets/ac85063c-012d-4ce3-ba80-ce8714a0c324)
   ~~~
   sns.boxplot(data=af)
~~~
   ![image](https://github.com/user-attachments/assets/3a7614a7-0894-4403-9ba2-8505c07d7466)
   ~~~
   sns.scatterplot(data=af)
~~~
   ![image](https://github.com/user-attachments/assets/e64670b5-7959-4a1e-a4ea-03b0065865b1)
   ~~~
   q1=af.quantile(0.25)
   q2=af.quantile(0.5)
   q3=af.quantile(0.75)
   iqr=q3-q1
   iqr
~~~
   ![image](https://github.com/user-attachments/assets/dd21765d-035d-478e-a48a-656cc2daa9fb)
   ~~~
   lower_bound=Q1-1.5*IQR
   upper_bound=Q3+1.5*IQR
   lower_bound
   upper_bound
~~~
   ![image](https://github.com/user-attachments/assets/9b8605f8-75e4-4a2c-83ac-4a763f01f3e3)
   ![image](https://github.com/user-attachments/assets/3d101ca5-286b-4271-a526-832b1a4ac8c1)
   ~~~
   outliers=[x for x in age if x<lower_bound or x>upper_bound]
   print("Q1:", Q1)
   print("Q3:", Q3)
   print("IQR:", IQR)
   print("Lower bound:", lower_bound)
   print("Upper bound:", upper_bound)
   print("Outliers:", outliers)
~~~
   ![image](https://github.com/user-attachments/assets/b2ae0b45-492f-453e-8d9d-518d8c4efce1)
   ~~~
   sns.boxplot(data=af)
~~~
   ![image](https://github.com/user-attachments/assets/32f85f7a-8d0d-46c8-8be7-a588e3bebfd6)
   ~~~
   data=[1,2,2,2,3,1,1,15,2,2,2,3,1,1,2]
   mean=np.mean(data)
   std=np.std(data)
   print("Mean of the Dataset is", mean)
   print("Std. Deviation is", std)
~~~
   ![image](https://github.com/user-attachments/assets/1f020114-11fc-4b63-85ad-47502082d997)
   ~~~
   threshold=3
   outlier=[]
   for i in data:
     z=(i-mean)/std
     if z>threshold:
       outlier.append(i)
   print("Outlier in dataset is", outlier)
~~~
   ![image](https://github.com/user-attachments/assets/ac8509d2-2750-4325-842b-24a7f558b4c6)
   ~~~
   from scipy import stats
   data={'weight':[12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,66,69,202,72,75,78,81,84,232,87,90,93,96,99,258]}
   df=pd.DataFrame(data)
   df
~~~
   ![image](https://github.com/user-attachments/assets/b6d3851f-b5e4-4a73-b4c3-acfc618acf46)
   ~~~
   z=np.abs(stats.zscore(df))
   print(df[z['weight']>3])
~~~
   ![image](https://github.com/user-attachments/assets/916889c8-5dc1-432a-ad2a-622bafaf8d0b)
   ~~~
   out=[]
   def d_o(val):
     ts=3
     m=np.mean(val)
    sd=np.std(val)
    for i in val:
      z=(i-m)/sd
      if np.abs(z)>ts:
        out.append(i)
    return out

   op=d_o(val)
   op
~~~
   ![image](https://github.com/user-attachments/assets/a26af9ce-8bdf-4122-8205-2b996c96cb76)


# Result
Thus the program to read the given data and perform data cleaning and save the cleaned data to a file has been successfully executed.
