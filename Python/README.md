# work in progress

[Variables and condition](#Variables-and-condition)  <br />
[Lists](#Lists)  <br />
[Dictionaries](#Dictionaries)  <br />


## Python Basics

### Variables and conditions

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

### Lists

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

### Dictionaries

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

**Calculate the average of columns** *(axis = 0 will give you the average per column and axis = 1 per row)*

```python
df[["A", "B"]].mean(axis=0)
```

