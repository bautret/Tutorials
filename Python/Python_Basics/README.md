# Python Basics

[Python](#Python-Basics) <br />
[Pandas](#Pandas)  <br />
[Plotly](#Plotly)  <br />

## Python Basics

**Initialize a variable**

```python
a = 5
```

**Display a value**

```python
print(a)
```

**Modify the value of a variable**

```python
a = 5
a = 7
```

**Know the type of a variable**

```python
print(type(a))
```

**Switch values (e.g.: a and b)**

```python
c = a
a = b
b = c
```

**Create conditions with if**

```python
e = 20
if (e > 5):
	print("strictly greater than 5")
elif (e==5):
    print("equal to 5")
else:
    print("strictly lower than 5")
```

**Create a list**

```python
l = [3, 5, 12, 7, 4, 36]
```

**Display its length**

```python
print(len(l))
```

**Display its elements**

```python
print(l[0])
print(l[2])
```

**Modify an element**

```python
l[2] = 17
```

**Add an element**

```python
l.append(296)
```

**Initialize a dictionary**

```python
d = {
    "A": "car",
    "B": 2,
    "C": "bike"
}
```

**Display dictionary's keys**
```python
print(d.keys())
```

**Display the value of a key**

```python
print(d["C"])
```

**Add a new key and its value**

```python
d["D"] = 8
```

**Print the data type of a key value**

```python
print(type(paris_city["location"]))
```

**Get the value of a subkey**

```python
paris_city["area"]["prefecture_level"]
```

**Get a specific element of a key**

```python
paris_city["location"][1]
```

## Pandas

**To import the library**

```python
import pandas as pd
```

**Create a dataframe from a dataframe**

```python
df_E_B = df[["E","B"]]
print(df_E_B)
```

**Only keep specific rows and columns**

```python
df_1_3_B_C_D = df.loc[1:3,["B","C","D"]]
print(df_1_3_B_C_D)
```

**Filter a dataframe** *(here only the rows that have a value greater than 8 in the column B)*

```python
df[df["B"] >= 8]
```

**Filter a dataframe with multiple conditions**

```python
df[(df["B"]>=8) & (df["D"]=="a")]
```

**Only display several rows**

```python
df_nba.head()
```
*include the number of rows you want to display like this: head(6). Don't forget you start to count by 0. By default it will display the first 5.*

**Calculate the average of columns** *(axis = 0 will give you the average per column and axis = 1 per row)*

```python
df[["A", "B"]].mean(axis=0)
```

**Upload a csv file** *(make sure the file is located in the same directory than you notebook online or locally)*

```python
import pandas as pd
df_facebook = pd.read_csv("acquisition_facebook_adds.csv")
```

*sometimes you'll get issue with the file, one reason could be how the column are separated*

**Convert a dataframe to a csv file**

```python
df_facebook_instagram_20190113.to_csv("acquisition_facebook_instagram_20190113.csv")
```

*sometimes you'll want to modify the separator*

```python
df_orders.to_csv("gwz_orders_samples_other_format.csv", sep=",")
```

**Open a json file**

```python
import json

with open("actors.json", "w") as f:
   json.dump(d, f)
```

The "w" indicates the write mode. As f: means we assign the json opening to the variable f. 
json.dum(d, f) will save the contents of the dictionary d to a JSON file f.

**Add new values to the json file**

```python
with open("actors.json", "r") as f:
   leonardo = json.load(f)

leonardo["nationality"] = "US"

with open("actors.json", "w") as f:
   json.dump(leonardo, f)
```

**Open an Excel file**

```python
df_sales_restaurant_1 = pd.read_excel("restaurants_accountability.xlsx")
```
*It will automatically open the first sheet of the file.*

To open all sheets

```python
df_sales_restaurant_1 = pd.read_excel("restaurants_accountability.xlsx", None)
```

*Top open a specific sheet*

```python
sheet_index = 1
df_sales_restaurant_1 = pd.read_excel("restaurants_accountability.xlsx", sheet_name = sheet_index)
```

or alternatively you can use the name of your sheet instead of the sheet_index

**Knows the number of columns and rows**

```python
df_facebook.shape
```

**Getting the name of your columns**

```python
print(list(df_order))
```

**Convert a column to datetime**

```python
df_facebook["date"] = pd.to_datetime(df_facebook["date"], format="%Y-%m-%d")
```

**Getting the min and max value**

```python
print(df_facebook["date"].min())
print(df_facebook["date"].max())
```

**Getting the sum value**

```python
print(df_facebook["spend"].sum())
```

**Getting the mean value**

```python
print(df_order.groupby("id_store")["m_cached_price"].mean())
```

**Getting unique values of a column**

```python
print(df_order["dim_status"].unique())
```

**Count the number of unique values in a column**

```python
print(len(df_order["id_store"].unique()))
```

**Group by in addition to aggregation function (e.g.: sum, count etc.)**

```python
df_facebook_daily = df_facebook.groupby("date")["spend"].sum()
print(df_facebook_daily)
```

**Group by several criteria**

```python
df_facebook_daily_2 = df_facebook.groupby(["date","channel"])["spend"].sum()
print(df_facebook_daily_2)
```

*an alternative way would be the following*

```python
cols_to_group_on = ["date", "channel"]
df_facebook_channel_daily = df_facebook.groupby(cols_to_group_on, as_index=False)["spend"].sum()
df_facebook_channel_daily
```

**Getting the proportion of a value**

```python
df_order["dim_status"].value_counts(normalize=True)
```

**Getting results in the ascending order**

```python
print(df_order.groupby("id_store")["id_order"].count().sort_values(ascending=False))
```

**Add a new column in your dataframe**

```python
df_order["price_per_customer"] = df_order["m_cached_payed"] / df_order["m_nb_customer"]
```

**Join two DataFrames together**

```python
df_facebook = pd.merge(df_facebook, df_taxes, on="channel", how="left")
df_facebook
```

**Create a pivot table**

```python
data = df_facebook
values = "real_spend"
index = ["date"]
columns = ["channel"]
aggfunc = "sum"
df_facebook_pivot = pd.pivot_table(data, values, index, columns, aggfunc).reset_index()
df_facebook_pivot
```

**Replace a value in a column by another one**

```python
df_order.loc[df_order.m_nb_customer == 0, "m_nb_customer"] = 1
```

**Delete rows that don't meet a certain condition**

```python
df_order = df_order[df_order["m_cached_payed"] > 0]
```

**To get basic info about a dataset**

```python
df.info()
```

*You could find this one useful too*

```python
df.describe()
```

**Convert to date and set it as an index**

```python
df["Date"] = pd.to_datetime(df["Date"], format='%Y-%m-%d')
df = df.set_index("Date")
```

**To get the number of appearanc of a certain value**

```python
df.index.dayofweek.value_counts()
```

**To display the data within a timeframe**

```python
mask = df.index.month.isin([1, 12])
df[mask]
```

## Plotly

Good website to get to know the different type of graphs :
[data-to-viz](https://www.data-to-viz.com/#area)

**The libraries you need**

```python
import numpy as np
from collections import Counter

import pandas as pd
import plotly.express as px
import plotly.graph_objects as go
from plotly.subplots import make_subplots
```

**To create a new figure**

```python
fig = go.Figure()
```

**Create a graphical object of type Scatter**

```python
first_line_object = go.Scatter(x=[2, 3], y=[7, 8], mode="lines")
```

**Show your graph**

```python
fig.add_trace(first_line_object)
fig.show()
```

**Another way to do all the above**

```python
fig = px.line(x=[2, 3], y=[7, 8], markers=True)
fig.show()
```

**For a bar graph**

```python
fig = px.bar(df[df.country == "France"],
             x="year",
             y="lifeExp",
             title="LifeExpectancy over time in France")
fig.show()
```

**To modify it to a line graph**

```python
fig = px.line(df[df.country == "France"],
             x="year",
             y="lifeExp",
             title="LifeExpectancy over time in France")
fig.show()
```

**Another example of graph**

```python
fig = px.scatter(df[df.year==2007],
                 x="gdpPercap",
                 y="lifeExp",
                 color="continent",
                 size="pop",
                 size_max=60,
                 title="lifeExp vs gdpPercap")
fig.show()
```

**Adding information when you pass your mouse on the date**
```python
hover_data=["country"]
```
