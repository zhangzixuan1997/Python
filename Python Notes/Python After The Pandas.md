```python
import pandas as pd
a = pd.read_csv("a")
a.head(3) # return rows
a.tail()
a.shape
a.dtypes
#There are no parenthese for shape and 
#dtypes beacuse they are attributes of the original data.
#The keywords with parenthese are methods wihch needs computation.
a.columns
a.index
```

![](resources/3C32F9093BF646147A0A12DB01E0A575.jpg)

Slicing Data Using Pandas
-------------------------

```python
a['Name'] # return a series
a.Name # return the same 
a.Grade.head()
a['Grade'].head()
#Here is how we write a dataframe
name_column.to_csv("Name_Grade.csv")
#Pick out a single entry
#Loc Method
df.loc[3,"Name"] #Pick up the 3rd value in the name column
df.loc[1:3, "Mini_Exam3":"Grade"]
df.loc[[0,2,4], ["Previous_Part","Grade"]]
#Compute mean of Final column
avg_final = df["Final"].mean()
list(df.columns) #get column names. 
#The unique() method returns an array (think of it as a list) of the unique values in the column
list_grades = df["Grade"].unique()
list_grades
#The value_counts() method returns the counts of each unique value in the column as a series
grade_breakdown = df["Grade"].value_counts()
#applying function to multiple rows
df[["Final", "Mini_Exam3"]].mean()

```

![](resources/FC4E7A726004F527797C98F16F163EE3.jpg)

1. `header=None` pandas automatically assign the first row of `df` (which is the actual column names) to the first row, hence your columns no longer have names
2. `header=0`, pandas first deletes column names(header) and then assign new column names to them (only if you pass names = [........] while loading your file).

  read\_csv( filepath, header = 0 , names = ['....' , '....' ...])

```python
summary = df.describe()
#slicing summary dataframe
summary.loc[["min", "max"], ["Final", "Previous_Part"]]
#Create New Columns
df["Final_Perc"] = df["Final"]/35
#Drop a column
df.drop(["Final_Perc"], inplace = True, axis=1)
#inplace means we are sure the change the data. Axis = 0 means column 
df.head()
#Sort the data frame according tothe Final Column
#By setting inplace= False will just return the sorted dataframe and not change df 
df.sort_values(by = ["Final"], inplace =False, ascending=False).head()
#Read in parking and specify column that will serve as index
df_parking = pd.read_csv("Data/Parking.csv", index_col=0)
```

Datetime Type
-------------

```python
#Reset the column Issue Date to be a datetime
df_parking["Issue_Date"] = pd.to_datetime(df_parking["Issue_Date"]) 
#Now its a datetime object
first_entry = df_parking.loc[0,"Issue_Date"]
first_entry
first_entry.day
first_entry.month
first_entry.weekday_name
first_entry.is_leap_year
#Get the day of the week for the entire column
all_dow = df_parking["Issue_Date"].dt.weekday_name
all_dow.head()
#Add the time into columns
df_parking["DOW"] = df_parking["Issue_Date"].dt.weekday_name
df_parking["Month"] = df_parking["Issue_Date"].dt.month
df_parking["Week"] = df_parking["Issue_Date"].dt.week
df_parking["Weekday"] = df_parking["Issue_Date"].dt.weekday
#Let's see the most frequent days for parking tickets
df_parking["DOW"].value_counts()
#We can even do time arithmetic.  We get a TimeDelta object
delta = parking.Issue_Date.max() - parking.Issue_Date.min()
delta
#Timedelta('753 days 09:21:00')
delta.seconds, delta.days
```

Other Pandas Methods
--------------------

```python
#Change the names of columns 
df.rename(columns={"1":"one", "2":"two"}, inplace=True)
#Setting the column Name to be the index
df.set_index("Name", inplace = True)

#Access Sol's info
df.loc["Sol",:]

```

![](resources/2DFD700FC6416C809090DD5755573F97.jpg)

```python
#Access Sol's info
df.loc["Sol",:]
#Resetting the index
df.reset_index(drop=False, inplace=True)
#Combine data frames with concat function
head = df.head()
tail = df.tail()
#axis=0 says stack them top to bottom. axis =1 stacks side to side 
dfConcat = pd.concat([head,tail], axis =0)
```

Handling Missing Data
---------------------

![](resources/5187AA8807B317690DF8F0F130B187CC.jpg)

```python
#isnull method for a data frame
df_missing.isnull()
#Notice that here the not available is turned into an NaN value
df_missing_NA = pd.read_csv("Data/Missing_Data.csv", na_values=["NaN", "not available"])
#Note that the temp column is unaffected
df_missing_NA2 = pd.read_csv("Data/Missing_Data.csv",\
                na_values={"Previous_Part":"NA", "Participation1":-1,"Mini_Exam2":"not available"})
df_missing_NA2
#Get rid of all rows with an NA
df_missing_NA2.dropna(axis=0)
#Passing how='all' will only drop rows that are all NA (doesn't change anything)
df_missing_NA2.dropna(how='all')
#Dropping column is just a matter of passing axis=1 (doesn't change anything)
df_missing_NA2.dropna(axis=1,how='all')
#Change the null value into 0
df_missing_NA2.fillna(0)
#You can pass fillna a dict which gives the replacement value for each column
df_missing_NA2.fillna({"Previous_Part":5,"Mini_Exam2":0.5})
#Replace with mean
df_missing_NA2.fillna(df_missing_NA2.mean())
```

Excel File with Pandas
----------------------

```python
df1 = pd.read_excel("Data/Excel_Reading.xlsx", "Sheet1")
#Get NA values
df1 = pd.read_excel("Data/Excel_Reading.xlsx", "Sheet1", na_values = ["NA", "Not avail"])
#Fill with mean
df1.fillna(df1.mean())
#Write the file with to_excel. We can specify a start row and column
df1.to_excel("NewFile.xlsx", "Sheet1", startrow=5, startcol=5)
```

Map Function 
-------------

```python
#Use map to create new column
df_titanic["Binary_Male"] = df_titanic.Sex.map({"male":1, "female":0})
df_titanic.head()
#Compute fraction of male passengers
df_titanic.Binary_Male.mean()
```

Apply Function
--------------

```python
#Using apply - axis =0
import numpy as np
df_titanic[["Age", "Fare"]].apply(np.mean,axis=0)
#Get round Numbers 
rounded_cols = df_titanic[["Age", "Fare"]].apply(np.round).head()
rounded_cols.head() 
```

![](resources/08D5ABB35B4A3C7FBAC60E4D040EFF21.jpg)![](resources/2C30AFA1E57857E58E869C5D77C94311.jpg)



Rename the column name 
-----------------------

```python
df.rename(columns = {"a":"b"}, inplace = False)
#concatenating dataframes 
df = pd.concat([df_a,df_b],axis = 0,ignore_index = True)
#axis 0 : concat by stacking on top of each other 
#axis 1 : concat by rows in a side by side way 
#Assign new indices by ignore = True 
```

Using The Index 
----------------

```python
#Reset index to the name 
df.set_index("Name",inplace = True)
#inplace = False will return a new df. 
df.loc["Joe","Grade"] #row name and column name
#if you reset again, the name will disappear
df["Name"] = df.index
df.set_index("ID",inplace = True)
#back to indices 
df.reset_index(inplace = True,drop = False)
#drop original. drop = true means orginial index is gone. 
```

Missing Data Theories 
----------------------

1\. 删除。一般情况下：missing value的样本量很小时，可以删除样本；有的时候也会删除整个feature，由于feature里面缺失的数据太多。缺点：信息丢失

2\. 补充。均值，中位数，固定值，最小值，最大值，插值等等，或者建立一个模型来“预测”缺失的数据，例如KNN。缺点：人为引入了noise

3\. 升维。把当前feature的value投射到更高维的空间，例如，是否参加考试，是/否/缺失？完整保留了原始数据的全部信息、不用考虑缺失值、不用考虑线性不可分之类的问题。缺点：feature一下增加了许多，计算量会很大。

4\. 忽略。例如，Random forest，自身能够handle数据缺失的情况，在这种情况下可以对确实数据进行忽略处理，即不需要对缺失数据做任何的处理。缺点：在模型的选择上有局限。

Apply function
--------------

```python
df.apply(max,asix = 0)  # apply each column the max values 
df.apply(max,asix = 0)  # apply each row the max values 
#The input here are entries. 
df['Ceil_Fare'] = df.Fare.apply(np.ceil) # ceiling version 7.8->8 
#Will give you a warining , you can copy the dataframe first to get rid of warning 
#apply also works for self built funtion 
def Get_gender_bool(gender):
  if gender =='mail': 
    return 1 
  else :
    return 0
df['gender_bool'] = df.sex.apply(Get_gender_bool)
```

Other Apply Funtions 
---------------------

```python
df2 = df_titanic [['age','sex']].copy
#Input is the series for a row
def old_man(row):
  age = row['age']
  sex = row['sex']
  
  if age >= 60 and sex == 'male':
    return 1 
  else: 
    return 0 
df2['old_man'] = df2.apply(old_man,axis = 1) # Apply to each row 
```

Iterrows 
---------

![](resources/13ACEEA78B83AA056DFA14A0AEC90136.jpg)

```python
df = df_titanic [['name','sex','age']].copy
#We can a 
for index, row in df.iterrows():
  # in this way you can get the index and the contents in that row, this is kind of slow 
  name = row['name']
  age = row['age']
  last_name = name.replace(',',"").split(" ")[0]
  D[last_name] = age
```







