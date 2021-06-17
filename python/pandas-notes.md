# Learning Pandas

Here's some quick notes for data munging using Pandas, Python, and Katt.

Note: Jupyter notebook probably wasn't necessary for this, but it's good practice to get used to the keyboard shortcuts again.

### A review of Lambda

To get through data munging faster, ```lambda``` functions define a function in a single line of code.  Some functions need more room, but as a rule of thumb, if it looks like something you could do in Excel, use a lambda.  The code is much easier to read.

Below is an example of basic Lambda syntax:


```python
mylambda = lambda x: (x * 2) + 3
print(mylambda(5))
```

    13


Lambdas can also work through basic ```if``` gates.  (For the love of documentation, don't make this too complicated without expanding it into a larger function.)

The following two code segments work the same way:


```python
def myfunction(x):
    if x > 40:
        return 40 + (x - 40) * 1.50
    else:
        return x
    
print(myfunction(50))
```

    55.0



```python
myfunction = lambda x: 40 + (x - 40) * 1.50 \
    if x > 40 else x
    # See that slash above?  Use it when the lambda is more than one line.

print(myfunction(50))
```

    55.0


Pretty cool.  For reference, here's a list of some of the most common data munging tasks.

```python
# Split a name in half and take the last name.
get_last_name = lambda x: x.split(' ')[-1]
df['last_name'] = df.name.apply(get_last_name)

# Find an email provider, or anything else.  Note the different syntax:
df['Email Provider'] = df.Email.apply(lambda x: x.split('@')[-1])

# Change names of columns in a dataframe
df.columns = ['ID', 'Title', 'Category', 'Year Released', 'Rating']

# Rename columns of data -- better because of specificity
df.rename(columns={
  'id': 'ID',
  'name': 'movie_title'},
  inplace=True
)

# Using a lambda on a row, because more than one column value is needed behind an if statement
total_earned = lambda row: (row.hourly_wage * 40) + ((row.hourly_wage * 1.5) * (row.hours_worked - 40)) \
    if row.hours_worked > 40 \
    else row.hourly_wage * row.hours_worked
df['total_earned'] = df.apply(total_earned, axis = 1)

# Make a new row that finds whether another row is NULL
ad_clicks['is_click'] = ad_clicks.ad_click_timestamp.isnull()
```

As well, here's some common aggregation functions to use on dataframe columns:

| Command | Description |
|---------|-------------|
 mean | Average of all values in column |
std | Standard deviation
median | Median
max | Maximum value in column
min | Minimum value in column
count | Number of values in column
nunique | Number of unique values in column
unique | List of unique values in column

If slicing and dicing is needed, aggregate by sub-type using syntax like:
```df.groupby('column1').column2.measurement()```

To make the output a proper dataframe instead of a series, add an ```reset_index()``` to the end, with both sets of parenthesis.

This can definitely start getting more complex, for example:

```python
import numpy as np
import pandas as pd

orders = pd.read_csv('orders.csv')
cheap_shoes = orders.groupby('shoe_color').price.apply(lambda x: np.percentile(x, 25)).reset_index()
```

The above finds what the 25th percentile is for the uploaded dataframe of shoes, grouping by the shoe color, then assigning the result to a dataframe named ```cheap_shoes```.

However, the above output is a tibble, which is hated by managers and UI folk everywhere.  Pandas thankfully can make a pivot table:

```python
shoe_counts_pivot = shoe_counts.pivot(
	columns='shoe_color',
	index='shoe_type',
	values='id').reset_index()
        ```

For merging, instead of using VLOOKUP a couple thousand times, you can use ```pd.merge(df1, df2)```.  The basic use of merge will merge together two dataframes using a column by the same name in each dataframe.  *Note: this is an Inner Join ONLY unless using ```how```*

If the dataframes don't have a column named the same to link them together, the easiest way to deal with it is by using ```df1.rename()``` (see above), as the dictionary-based process can be sturdier and easier to troubleshoot.

The process can be made even more explicit with the following:

```python
pd.merge(
    orders,
    customers,
    left_on='customer_id',
    right_on='id',
    suffixes=['_order', '_customer'])
    how='outer'
```

- ```left_on``` and ```right_on``` are the two columns the datasets are spliced together, or how to distinguish your foreign keys.  
- ```suffixes``` are for when two columns in each df have the same column name.  By default, the one on the left will be "x" and on the right will be "y".
- ```how``` is for the join type, and can be 'outer', 'left', or 'right' -- this defaults to inner, so be careful to not drop things
- When playing with dataframes, use nice spacing.  It's a lot easier to work through nice spacing, and more logical to use spacing similar to SQL.  That way when a DBA gets pissed off, they won't also start swearing at your code, and everyone can read it.

To merge together two dataframes with identical columns (such as for data from two rounds of the same experiment, or two sign-up sheets), use ```pd.concat([df1, df2])```.
