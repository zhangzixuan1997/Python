![](resources/123A273C2DDB93856655D45F56F39097.jpg)

Group By Function
-----------------

```python
 a = a.groupby(by=['Month','Shot_Type'],as_index = False).count()
```

![](resources/52904418F5A2DD7F3C7A216716800FCB.jpg)

If we dont set the as\_index to False, month will be the index.

pivot\_table funtion. 
----------------------

```python
FG_perc_by_month = pd.pivot_table(c, values='FGM', index='Month',columns=['Shot_Type'],aggfunc='mean')
```

![](resources/7A5BE92AF054662363F653AE69B87A9E.jpg)

Group By With Transfrom
-----------------------

### fill na based on groupby means

![](resources/A62D38B368774E255AC3806EF89B654C.jpg)

```python
# transform the original data for the groupby  series -> series
df['mpg'] = df.groupby(by = ['cyl']).mpg.transform(lambda x : x.fillna(x.mean())) 
# Standadize the hp 
df['hp_new'] = (df['hp'] - hp_mean) / hp_std
# Want to normalize based on groups:
df['mpg'] = df.groupby(by = ['cyl']).mpg.transform(lambda x : (x-x.mean())/x.std()) 

# We can use apply as well, but more difficult
def: stand(group): 
  return pd.Dataframe({"hp_new":(group['hp']-group['hp'].mean())/group['hp'].std()})
df['hp_new'] = df['mpg'] = df.groupby(by = ['cyl']).apply(stand)
# Can only return a df, becasue series will change the dataset 
```

Filtering
---------

```python
df.groupby(by = ['cyl']).filter(lambda x : len(x)>=3)
#check only cylinders groups with more than 3 variables 
df.groupby(by = ['am']).filter(lambda x : x.mpg.mean()>=df.mpg.mean())
#The mpg of this group is larger than the average mpg of the entire dataset 
```

$x^2$







