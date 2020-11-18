Lambda Funtion
--------------

```python
f = lambda x : x+5
f(10) # will return 15

#Two input 
f = lambda first,last: first + " " + last
#If else combine
f = lambda x: x*2 if x%2==0 else x 
```

Apply Lambda Funtion with Apply Funtion 
----------------------------------------

```python
df_mtcars["num_in_name"] = df_mtcars.car_name.apply\
                           (lambda x: 1 if x.replace(" ", "").\
                           isalpha() else 0)

df_mtcars.head(15)
#如果全是字母则返回1，有非字母则返回0
```

```python
df_mtcars["env_friendly"] =\
                           df_mtcars.apply(lambda row: 1 if (row["cyl"] in [4,6]
                           and row["mpg"]>=20)\
                           or (row["cyl"]==8 and row["mpg"]>=16) else 0,axis = 1)
#4-6 cyl and mpg >=20 
#or 8cyl and mpg >=16
#---> 1 else: 0 
```

Filtering
---------

![](resources/599EE70AB6C1455330DC86EFD606E6F6.jpg)

### Baisc Filters

```python
fast_car = df.loc[df.hp>150, :]
boolean_fast = df.hp>150
fast_car = df.loc[boolean_fast, :]
fast_car_mpg = df.loc[df.hp>150,['mpg']]# columns should be in a list
```

### Advanced Filters

```python
df.loc[(df.cyl==6)&(df.gear==4), :]
#use () and & or | to add multiple conditions 
df.cyl.isin([4,6])# return the boolean
df.loc[df.cyl.isin([4,6]),]
```

Duplicate Function
------------------

