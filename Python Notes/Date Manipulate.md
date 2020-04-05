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

```python
#Define a datetime to get a time period

```
