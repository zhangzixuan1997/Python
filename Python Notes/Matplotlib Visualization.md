Main Methods 
-------------

```python
import pandas as pd
import matplotlib.pyplot as plt
#Read in data frame - Note the new style "bmh"
plt.style.use("ggplot")
#matplotlib.use("nbagg")
df_cars = pd.read_csv("Data/mtcars.csv")
#I am sorting so I can slice out the automatic and manual calls.
df_cars_sorted = df_cars.sort_values(by="am").reset_index(drop = True)
df_cars_sorted
#Get automatic (am=0) versus manual (am=1) cars.  We will see a faster way to do this using SQL.
df_cars_auto = df_cars_sorted.loc[0:18,:]
df_cars_man = df_cars_sorted.loc[19:,:]

```

### \#Create figure and get the axes

```python
#Create figure and get the axes
fig , (ax0,ax1,ax2) = plt.subplots(nrows=1,ncols=3, figsize = (15,5))

#Add title for entire figure
fig.suptitle("Understanding the Effect of Horspower on other Features")
#Plot hp versus mpg for auto
df_cars_auto.plot(kind="scatter", x = "hp", y = "mpg", color = 'b', label = "auto",  ax = ax0 )

#Plot hp versus mpg for manual
df_cars_man.plot(kind="scatter", x = "hp", y = "mpg", color = 'r', marker = "x", label = "manual", ax = ax0 )

#Change axis labels and title
ax0.set(title = "hp vs. mpg", xlabel="horspower", ylabel="miles per gallon")

#Get rid of grid lines
ax0.grid(False)

#Change the background color
ax0.set_facecolor("white")
#Plot hp versus displacement for auto
df_cars_auto.plot(kind="scatter", x = "hp", y = "disp", color = 'b', label = "auto",  ax = ax1 )

#Plot hp versus mpg for manual
df_cars_man.plot(kind="scatter", x = "hp", y = "disp", color = 'r', marker = "x", label = "manual", ax = ax1)

#Change axis labels and title
ax1.set(title = "hp vs. disp", xlabel="horspower", ylabel="dispersion (cu. in.)")

#Plot hp versus quater mile time for auto
df_cars_auto.plot(kind="scatter", x = "hp", y = "qsec", color = 'b', label = "auto",  ax = ax2, )

#Plot hp versus mpg for manual
df_cars_man.plot(kind="scatter", x = "hp", y = "qsec", color = 'r', marker = "x", label = "manual", ax = ax2)

#Change axis labels and title
ax2.set(title = "hp vs. qsec", xlabel="horspower", ylabel="1/4 mile time (sec)")
#Compute the two means
mean_mpg_auto = df_cars_auto.mpg.mean()
mean_mpg_man = df_cars_man.mpg.mean()

#Draw the two lines
ax0.axhline(mean_mpg_auto, color = "b", linestyle = "--")
ax0.axhline(mean_mpg_man, color = "r", linestyle = "--")

fig
```

![](resources/D8098EF48F39926AFD3F758C491338F2.jpg)

```python
#Saving the figure to png
fig.savefig("carplots.png", bbox_inches = "tight")
#Formatting the axes labels 
from matplotlib.ticker import FuncFormatter
def currency(x,pos):
#where the input x is axis label and pos is the position 
  in_thousand = int(x/1000)
  new_label = '$%dK'%in_thousand
  return new_label
currency(100000,1)
#Will give you $100K
```

### Share Y label

```python
fig,(ax0,ax1) = plt.subplots(nrows=1,ncols=2,sharey = True,figsize=(10.6))
```

![](resources/778B2ADEB92BC62B75A224C1E1733CA8.jpg)



Other Methods
-------------

![](resources/5DBAA00B6DD1B34A15393D7644A86C4D.jpg)

![](resources/70CA1C660A3ADC152957807F6F444E92.jpg)

![](resources/60EFA4110238857A1C530603078441F8.jpg)





