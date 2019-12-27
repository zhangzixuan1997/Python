![](resources/AF6AD414D2D6012C5D6EC81998F7FD5E.jpg)

```python
#Inner Merge
df_teams.merge(df_city,how='inner',left_on = 'Home_City',right_on='Num_Fans')
df_players.merge(df_teams,how='inner', on = "Team")
```

![](resources/7AD5DC17241F7A3554C6AEC651589452.jpg)

```python
#Left Join # Chelsea is not in the second table 
df_players.merge(df_teams,how='left', on = "Team")
```

![](resources/54581DD2C2FA19678236F6A3DDCA97D7.jpg)

```python
df_outer = df_rush.merge(df_rec,how="outer",on="Week")
df_outer.fillna(0,inplace=True)
```

