```python
from pandasql import sqldf
name_year = sqldf("SELECT Name, Year, FROM df WHERE Year = 2000 AND name = 'Jake'")
#This will return a data frame
name_year2 = sqldf("SELECT Gender, COUNT(count) AS Total_Count FROM df \
                    WHERE Year > 500 GROUP BY Gender")
```

String Formatting 
------------------

```python
num_cookies = 10 
sentence = "I ate %d cookies", %num_cookies
# %d %f %f 
num_cookies = 10.3333
sentence = "I ate %0.3f cookies", %num_cookies
#"I ate 10.333 cookies"
num_1 = 10
num_2 = 20
sentence = "I ate %d cookies, he ate %d cookies", %(num_1,num_2)
```

Genral SQL Queries 
-------------------

```python
year = 2000
query = "SELECT Name, Year, FROM df WHERE Year = %d AND name = 'Jake'" %year
sqldf(query)
```

SQL with Join
-------------

```python
query = "SELECT * from df_A  AS a JOIN df_B AS b ON a.city = b.city"
```

