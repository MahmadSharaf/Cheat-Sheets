# Data Structures

- [Data Structures](#data-structures)
  - [NumPy](#numpy)
    - [NumPy Modules](#numpy-modules)
  - [Pandas](#pandas)
    - [Input/Output](#inputoutput)
      - [Read and Write from CSV](#read-and-write-from-csv)
      - [Read and write from Excel](#read-and-write-from-excel)
      - [Read and Write to SQL Query or Database Table](#read-and-write-to-sql-query-or-database-table)
    - [Retrieving Information](#retrieving-information)
      - [Basic Information](#basic-information)
      - [Summary](#summary)
    - [Data Wrangling](#data-wrangling)
      - [Creating Data Frame](#creating-data-frame)
      - [Non-aggregating methods](#non-aggregating-methods)
      - [Reshaping Data](#reshaping-data)
      - [Subset Observations (rows)](#subset-observations-rows)
      - [Subset Variables (Columns)](#subset-variables-columns)
      - [Subset row and column](#subset-row-and-column)
    - [Handling Missing Data](#handling-missing-data)
    - [Group Data](#group-data)
    - [Sort and Rank](#sort-and-rank)
    - [Applying functions](#applying-functions)
    - [Plotting](#plotting)
    - [Pandas Tips and Tricks](#pandas-tips-and-tricks)
    - [Styling DataFrames](#styling-dataframes)
    - [Logic in Python](#logic-in-python)
    - [String manipulation using Regular Expressions](#string-manipulation-using-regular-expressions)
  - [Matplotlib](#matplotlib)
    - [Create Plot](#create-plot)
    - [Plotting Routines](#plotting-routines)
    - [Customize Plot](#customize-plot)
    - [Save Plot](#save-plot)
    - [Show Plot](#show-plot)
    - [Close & Clear](#close--clear)
    - [Matplotlib references](#matplotlib-references)
  - [Seaborn](#seaborn)
    - [Import seaborn library](#import-seaborn-library)
    - [Basic Steps for creating plots with Seaborn](#basic-steps-for-creating-plots-with-seaborn)
      - [Step 1: Prepare the data](#step-1-prepare-the-data)
      - [Step 2: Figure Aesthetics](#step-2-figure-aesthetics)
      - [Step 3: Plotting](#step-3-plotting)
      - [Step 4: Further Customizations](#step-4-further-customizations)
      - [Step 5: Show, Save, Close](#step-5-show-save-close)
    - [Seaborn References](#seaborn-references)
  - [Resources](#resources)

## NumPy

- It gives Arrays that a great data structure objects, that makes working with numerical data easy and simple more than what it can be done in pure python.
- It is the foundation for the python data stack, and it is what makes python great for data analysis.

### NumPy Modules

1. Random: it helps to simulate random events like coin flips.

   1. [randint(low = 0, high, size)](https://numpy.org/doc/stable/reference/random/generated/numpy.random.randint.html?highlight=randint#numpy.random.randint): it generates a list of [size] numbers and each element value can be any value between [low] and [high-1].
   2. [choice(a, size, replace=True, p=None)](https://numpy.org/doc/stable/reference/random/generated/numpy.random.choice.html?highlight=choice#numpy.random.choice): generates a random sample of size [size] from given 1-D array [a] and [p] is the probability of each value in [a]. [replace] is for bootstrapping, as whether values could be chosen more than once or not.
   3. [binomial(n,p,size=None)](https://numpy.org/doc/stable/reference/random/generated/numpy.random.binomial.html?highlight=binomial#numpy.random.binomial): Draw samples from a binomial distribution, Samples are drawn from a binomial distribution with specified parameters, n trials and p probability of success where n an integer >= 0 and p is in the interval [0,1]. (n may be input as a float, but it is truncated to an integer in use)
   4. seed
   5. gamma
   6. [normal(loc=0.0, scale=1.0, size=None)](https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.random.normal.html): Draw random samples from a normal (Gaussian) distribution. [loc] is the center point, [scale] is the standard deviation, [size] is the number of sampling points.

   ```py
   import numpy as py
   
   np.random.randint(2, size=10)
   # [1,0,0,1,1,0,1,1,0,0]
   
   np.random.choice([0,1], size=10000, p=[0.8, 0.2]).mean()
   # 0.203199999999 which shows that the probability of 1 is 20%
   
   np.random.binomial(n=10, p=.5)
   # 5
   # the above is the same as the below
   (np.random.randint(2,size=10)==0).sum()
   # 5
   # The below will give the results of the above test 1000 times
   np.random.binomial(n=10, p=.5, size=1000)
   # result of flipping a coin 10 times, tested 1000 times.
   
   np.random.normal(70,std,10000)
   # returns a normal distribution of 10000 sample with center at 70 and has 2.5 wide spread.
   ```

[Python For Data Science NumPy Cheat Sheet](files/Python%20For%20Data%20Science%20NumPy%20Cheat%20Sheet.pdf)

## Pandas

- It gives Data Frames that are great data structures objects, that can manipulate and analyze data. It also includes some convenient methods for visualizing data that hook into matplotlib.
- [Compared to SQL](https://pandas.pydata.org/pandas-docs/stable/getting_started/comparison/comparison_with_sql.html) and [Medium Article](https://medium.com/jbennetcodes/how-to-rewrite-your-sql-queries-in-pandas-and-more-149d341fc53e#e009)

### Input/Output

#### Read and Write from CSV

- [read_csv](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_csv.htm)
- [to_csv](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.to_csv.html)

```py
# Read and write from CSV
pd.read_csv('file_name.csv',header=None,nrows=5,na_values='?')

# Convert DataFrame to CSV file
df.to_csv('file_name.csv')
# `to_csv()` will store our index unless we tell it not to. To make it ignore the index, we have to provide the parameter `index=False`
df.to_csv('file_name_edited.csv', index=False)
```

#### Read and write from Excel

- read_excel
- to_excel

```py
# Read and write from Excel
pd.read_excel('file_name.xlsx')
df.to_excel('file_name.xlsx')

# Write to excel sheet with multiple sheets
with pd.ExcelWriter(path='file_name.xlsx') as writer:
        df1.to_excel(writer,sheet_name='df1')
        df2.to_excel(writer,sheet_name='df2')
        df3.to_excel(writer,sheet_name='df3')

# Read multiple sheets from excel file
xlsx = pd.ExcelFile('file_name.xlsx')
df = pd.read_excel(xlsx, 'Sheet1')
```

#### Read and Write to SQL Query or Database Table

```py
from sqlalchemy import create_engine
engine = create_engine('sqlite:///:memory:')

pd.read_sql("SELECT * FROM my_table;", engine)
pd.read_sql("my_table;", engine)

# read_sql() is a convenience wrapper around read_sql_table() and read_sql_query()
pd.read_sql_table('my_table',engine)
pd.read_sql_query("SELECT * FROM my_table;", engine)


pd.to_sql('my_DF', engine)
```

### Retrieving Information

#### Basic Information

```py
# Get rows and columns counts
df.shape

# Describe index
df.index

# Describe Columns
df.columns

# This displays a concise summary of the DataFrame,
# including the number of non-null values in each column
df.info()

# Number of non-NA values
df.count()

# This returns the data types of the columns
df.dtypes
```

#### Summary

- [idxmax](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.idxmax.html)

```py
# Sum of values
df.sum()

# Cumulative sum of values
df.cumsum()

# Min values
df.min()

# Max values
df.max()

# Min index value
df.idmin()

# Max index value
df.idmax()

# Finds the index of the row containing a column's maximum value!
df.colum_name.idxmax()

# Summary Statistics
df.describe()

# Mean of values
df.mean()

# Median of values
df.median()

# Variance of each object
df.var()

# Standard Deviation of each object
df.std()

# Count of Null values in each column
df.isna().sum()

# Count of Null values in each row
df.isna().sum(axis=1)

# List unique values in the df['name'] column
df.column_name.unique()

# This returns the number of unique values in each column
df.column_name.nunique()

# Return values at the given quantile over requested axis.
df.quantile(0.5)
```

### Data Wrangling

#### Creating Data Frame

```py
# Specify values for each column
df = pd.DataFrame(
   {
      "a": [4,5,6],
      "b": [7,8,9],
      "c": [10,11,12]
   },
   index= [1,2,3])

# Specify values for each row
df = pd.DataFrame(
   [[4,7,10],
    [5,8,11],
    [6,9,12]],
   index = [1,2,3],
   column = ['a','b','c'])

# Specify DataFrame with a MultiIndex
df = pd.DataFrame(
   {
      "a": [4,5,6],
      "b": [7,8,9],
      "c": [10,11,12]
   },
   index= pd.MultiIndex.from_tuples(
      [('d',1),('d',2),('e',2)],
      names = ['n','v']))
```

#### Non-aggregating methods

```py
# the `round` method rounds each number to a given decimal place. `round(3)` rounds to the nearest 3 decimal points while `round(-3)` rounds to the nearest thousand
df.round(decimals=0)
```

#### Reshaping Data

- [df_new = df.copy() vs df_new = df](https://www.geeksforgeeks.org/python-difference-between-pandas-copy-and-copying-through-variables/)
- [to_datetime](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.to_datetime.html) converts string to DateTime type
- [Merges()](https://pandas.pydata.org/pandas-docs/stable/user_guide/merging.html)
- [cut()](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.cut.html)

```py
# The `melt` method stacks columns one on top of the other.
pd.melt(df)

df_new = df.melt(id_vars = ['id','a_column'],
                  value_vars = ['col_1', 'col_2'],
                  var_name = 'var_col_name', value_name = 'val_col_name')

# Spread rows into columns
pd.pivot(columns='vars', values='val')

# Append rows of DataFrames
pd.concat([df1,df2])

# Append columns of DataFrames
pd.concat([df1,df2],axis=1)

# Combine dataframes
df3 = df1.append(df2, ignore_index=True)

# Merge dataframes
df_combined = df1.merge(df2, left_on='column_name_df1', right_on='column_name_df2', how='inner')

# Order rows by values of a column (low to high).
df.sort_values('col_name')

# Order rows by values of a column (low to high).
df.sort_values('col_name', ascending=False)

# Rename the columns of DataFrame
df.rename(columns = {'old_col_name':'new_col_name'})

# Rename all column labels to replace spaces with underscores and convert everything to lowercase. (Underscores can be much easier to work with in Python than spaces. For example, having spaces wouldn't allow you to use df.column_name instead of df['column_name'] to select columns or use query(). Being consistent with lowercase and underscores also helps make column names easy to remember.)
df.rename(columns=lambda x: x.strip().lower().replace(' ','_'), inplace=True)

# copying a DataFrame or Series
# Pandas .copy() method is used to create a copy of a Pandas object. Variables are also used to generate copy of an object but variables are just pointer to an object and any change in new data will also change the previous data.
df2 = df.copy()

# Converts string to datetime object. But CSV will read this column as strings next time the file reopened, unless the it parsed into the CSV file. But pandas to_datetime provides more options than that of CSV.
df['date_column'] = pd.to_datetime(df['date_column'])

# Use cut when you need to segment and sort data values into bins. This function is also useful for going from a continuous variable to a categorical variable. For example, cut could convert ages to groups of age ranges. Supports binning into an equal number of bins, or a pre-specified array of bins.
pd.cut(x, bins, right=True, labels=None, retbins=False, precision=3, include_lowest=False, duplicates='raise', ordered=True)
```

#### Subset Observations (rows)

```py
# Extract rows that meet logical criteria
df[df.col_name > 7]

# Returns boolean column, which gives the duplicate TRUE value with escaping the first instance. All rows has to be the same to be identified as duplicate.
df.duplicated()

# Removes the duplicates (only consider columns) in the dataset and inplace parameter applies the change in the dataset.
df.drop_duplicates(inplace=True)

# Select first n rows
df.head(n)

# Select last n rows
df.tail(n)

# Randomly select fraction of rows
df.sample(frac=0.5)

# Randomly select n rows
df.sample(n=10)

# Select rows by position
df.iloc[10:20]

# Select and order top n entries.
df.nlargest(n, 'value')

# Select and order bottom n entries
df.nsmallest(n, 'value')
```

#### Subset Variables (Columns)

- [loc(), iloc()](https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html)

```py
# Select multiple columns with specific names
df[['col1','col2','col3']]

# Select single column with specific name.
df['col']
df.col

# Select columns whose name matches regular expression regex.
df.filter(regex='regex')

# Select all columns between x2 and x4 (inclusive)
df.loc[:,'x2':'x4']

# Select columns in positions 1,2 and 5 (first column is 0)
df.iloc[:,[1,2,5]]
```

#### Subset row and column

- [loc(), iloc()](https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html)

```py
# Select single value by row and column
# By Index/Position
df.iloc[[0],[0]]
df.iat[[0],[0]] # Get scalar/single value. It's a very fast iloc
# By Column/Label
df.loc[[0],['col_name']]
df.at[[0],['col_name']] # Get scalar/single value. It's a very fast loc

# Select rows meeting logical condition, and only in the specific columns
df.loc[df['a'] > 10, ['a','c']]

# Crosstab lets you select multiple columns and then see how many records, there are that overlap for different values of these columns.
pd.crosstab(df.col1,df.col2, aggFunc=sum, margins=True, normalize=True).plot(kind='bar')
```

### Handling Missing Data

```py
# Drop values from rows
s.drop(['a','c'])

# Remove rows or columns by specifying label names and corresponding axis, or by specifying directly index or column names. When using a multi-index, labels on different levels can be removed by specifying the level.
df.drop(labels=None, axis=0, index=None, columns=None, level=None, inplace=False, errors='raise')

# Remove rows with NULL values
df.dropna()

# Remove columns with NULL values
df.dropna(axis=1)

# More dropna rules
df.dropna(how='all')
# specify the threshold equals 4, means that dropping the column if it has 4 missing values or more.
df.dropna(thresh=4, axis=1)
df.dropna(subset=['Fruits'])

# Fills the missing values with value and if inplace is true it will replace the column with new data.
df['column_name'].fillna(value, inplace=True)

# Replace all null data with value
df.fillna(value)
# Method 'Pad' uses the previous record and use to impute the value. `limit` parameter limits the number of consecutive imputations
df.fillna(method = 'pad', limit=1)
# Method 'bfill' is the backfill technique, it fills the missing value with the value of the next one.
df.fillna(method = 'bfill')
# Method 'ffill' is the forward technique, it fills the missing value with the value of the previous one.
df.fillna(method = 'ffill')

# Substitute missing values using the existing one using interpolation technique
df.interpolate()
```

### Group Data

- All of summary functions can be applied to a group
- [groupby](https://www.shanelynn.ie/summarising-aggregation-and-grouping-data-in-python-pandas/)

```py
# Returns the frequency of occurrence of all the unique values within a single column
df.column_name.value_counts()

# Return a GroupBy object, grouped by values in column 'col'
df.groupby(by='col')

# Return a GroupBy object, grouped by values in index level named 'ind'
df.groupby(level='ind')

# Aggregate group using function
agg(function)

# Single aggregation, single column
df.groupby('column_name').agg(new_column_name=('column_name', 'mean'))

# Multiple aggregation, single column
df.groupby('column_name').agg(new_column_name1=('column_name', 'mean'),
                       new_column_name2=('column_name', 'max'),
                       new_column_name3=('column_name', 'count'))

# Multiple grouping columns, multiple aggregations
df.groupby(['column_name1','column_name2']).agg(
    new_column_name1=('column_name', 'count'),
    new_column_name2 = ('column_name',lambda x: len(x)/df2  .shape[0]),
    )

# Pivot tables groups and aggregates the same way as `groupby`, but places the unique values of one of the grouping columns as the new columns in the resulting DataFrame.
# Notice that pivot tables make for easier comparisons across groups.
df.pivot_table(index='column_name1', columns='column_name2', 
                     values='column_name', aggfunc='mean')
```

### Sort and Rank

- [CategoricalDtype](https://pandas.pydata.org/pandas-docs/version/0.23.4/generated/pandas.api.types.CategoricalDtype.html): to convert the data into an ordered type, the order of categories becomes innate to the feature, and we won't need to specify an "order" parameter each time it's required in a plot.

```py
# Sort by row or column index
df.sort_index(by='col_name')

# Sorts by the values along an axis
df.sort_values(by='Column label')

# Sorts values by column1 in ascending order
df.sort_values(column1, ascending=True)

# Sort a series by its values
s.order()

# Assign ranks to entries
df.rank()

# CategoricalDtypes
# this method requires pandas v0.21 or later
level_order = ['Alpha', 'Beta', 'Gamma', 'Delta']
ordered_cat = pd.api.types.CategoricalDtype(ordered = True, categories = level_order)
df['cat_var'] = df['cat_var'].astype(ordered_cat)
# # use this method if you have pandas v0.20.3 or earlier
# df['cat_var'] = df['cat_var'].astype('category', ordered = True,
#                                      categories = level_order)
```

### Applying functions

- [apply()](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.apply.html)
- [applymap](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.applymap.html?highlight=applymap#pandas.DataFrame.applymap)

```py
f = lambda x: x*2
# Apply function
df.apply(f)

# Apply function element-wise
df.applymap(f)
```

### Plotting

```py
# Plot Histogram for each column
df.plot.hist()

# hist() can be called on a Pandas series object as well
df.column_name.hist();

# plot() is a more general plotting function
df.column_name.plot(kind='hist');
df.plot(x='x-axis column_name', y='y-axis column_name', kind='scatter');
df.column_name.plot(kind='box');
df.column_name.plot(kind='pie');
# Scatter chart using pairs of points
df.plot.scatter(x='w', y='h')
# scatter_matrix() shows the relationships among numerical variables with scatter plots. It also returns a histogram for each variable.
pd.plotting.scatter_matrix(df, figsize=(15,15));
```

### Pandas Tips and Tricks

```py
# Get information about a function
help(pd.Series.loc)

# convert to string and extract the integer using regular expressions
df['column_name'].str.extract('(\d+)').astype(int)

# get all rows that column_name has values contains (/)
df[df['column_name'].str.contains('/')]

# View the index number and label for each column
for i, v in enumerate(df.columns):
    print(i, v)

# remove "_mean" from column names
new_labels = []
for col in df.columns:
    if '_mean' in col:
        new_labels.append(col[:-5])  # exclude last 6 characters
    else:
        new_labels.append(col)
# datatypes of columns
for i, v in enumerate(df.iloc[0,:]):
    print(df.columns[i],':', type(v))

# make sure they're all identical like this
(df_08.columns == df_18.columns).all()

# Get dummy columns with 1,0 encoding for Linear Regression Model, it will return
pd.get_dummies(df['column_name'])
```

### Styling DataFrames

- pandas enables you to style DataFrames in various ways to provide emphasis on particular cells.

```py
# Below, the maximum value of each column is highlighted, a comma is added to separate the digits, and decimals are removed.
df.style.highlight_max().format(r'{:,.0f}')
```

### Logic in Python

- `<` : Less than
- `>` : Greater than
- `==`: Equals
- `<=`: Less than or equals
- `>=`: Greater than or equals
- `!=`: Not equal to
- `df.column.isna(values)` : Group membership
- `pd.isnull(obj)` : Is NaN
- `pd.notnull(obj)`: Is not Nan
- `&,|,~,^,df.any(),df.all()` : Logical and, or, not, xor, any, all

### String manipulation using Regular Expressions

- `'\.'` : Matches strings containing a period '.'
- `'Length$'` : Matches string ending with word 'Length'
- `'^Sepal'` : Matches string beginning with word 'Sepal'
- `'^x[1-5]$` : Matches strings beginning with 'x' and ending with 1,2,3,4,5
- `'^(?!Species$).*'` : Matches strings except the string 'Species'

```py
# (passengers:1 crew:1)
df.column_name.str.extract(r'(\d+)?\D*(\d+)?\D*(\d+)?').head()
# 1 1
```

## Matplotlib

- Matplotlib is a package for building visualizations from your data. It can make many kinds of simple plots with tiny amounts of codes, but it can take some code effort to  create a professional looking figures.
- Matplotlib is a Python 2D plotting library which produces publication-quality figures in a variety of hard copy formats and interactive environments across platforms.
- [Magic words](https://ipython.readthedocs.io/en/stable/interactive/magics.html)

### Create Plot

- Import the library
  
  ```py
  import matplotlib.pyplot as plt
  
  # view the plots in the notebook
  %matplotlib inline
  ```

- Create figure
  
  ```py
  fig = plt.figure()
  fig2 = plt.figure(figsize=plt.figaspect(2.0))
  ```

- Axes: All plotting is done with respect to an Axes. In most cases, a subplot will fit your needs. A subplot is an axes on a grid system.
  
  ```py
  fig.add_axes()
  ax1 = fig.add_subplot(221) # row-col-num
  ax3 = fig.add_subplot(212)
  fig3, axes = plt.subplots(nrows=2,ncols=2)
  fig4, axes2 = plt.subplots(ncols=3)
  ```

### Plotting Routines

- 1D Data
  
  ```py
  # Draw points with lines or markers connecting them
  lines = ax.plot(x,y
  
  # Draw unconnected points, scaled or colored
  ax.scatter(x,y)
  
  # Plot vertical rectangles (constant width)
  axes[0,0].bar([1,2,3],[3,4,5]
  
  # Plot horizontal rectangles (constant height)
  axes[1,0].barh([0.5,1,2.5],[0,1,2]
  
  # Draw a horizontal line across axes
  axes[1,1].axhline(0.45)
  
  # Draw a vertical line across axes
  axes[0,1].axvline(0.65)
  
  # Draw filled polygons
  ax.fill(x,y,color='blue')
  
  # Fill between y-values and 0
  ax.fill_between(x,y,color='yellow')
  ```

- Vector Fields
  
  ```py
  # Add an arrow to the axes
  axes[0,1].arrow(0,0,0.5,0.5)
  
  # Plot a 2D field of arrows
  axes[1,1].quiver(y,z)
  
  # Plot 2D vector fields
  axes[0,1].streamplot(X,Y,U,V)
  ```

- Data Distributions
  
  - [errorbar()](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.errorbar.html)
  
  ```py
  # Plot a histogram
  ax1.hist(y)
  
  # Plot a Heat Map
  plt.hist2d(data = df, x = 'disc_var1', y = 'disc_var2', bins = [bins_x, bins_y])
  
  # Make a box-and-whisker plot
  ax3.boxplot(y)
  
  # Make a violin plot
  ax3.violinplot(z)
  
  # Make Line Plots. Plot y versus x as lines and/or markers with attached errorbars.
  plt.errorbar(data = df, x = 'num_var1', y = 'num_var2')
  ```

- 2D Data
  
  ```py
  # Colormapped or RGB arrays
  fig, ax = plt.subplots()
  im = ax.imshow(img, cmap='gist_earth', interpolation='nearest', vmin=-2,vmax=2)
  
  # Pseudocolor plot of 2D array
  axes2[0].pcolor(data2)
  
  # Pseudocolor plot of 2D array
  axes2[0].pcolormesh(data
  
  # Plot contours
  CS = plt.contour(Y,X,U
  
  # Plot filled contours
  axes2[2].contourf(data1)
  
  # Label a contour plot
  axes2[2]= ax.clabel(CS)
  ```

### Customize Plot

- Colors, Color Bars & Color Maps
  
  ```py
  plt.plot(x, x, x, x**2, x, x**3)
  ax.plot(x, y, alpha = 0.4)
  ax.plot(x, y, c='k')
  fig.colorbar(im, orientation='horizontal')
  im = ax.imshow(img, cmap='seismic')
  ```

- Markers
  
  ```py
  fig, ax = plt.subplots()
  ax.scatter(x,y,marker=".")
  ax.plot(x,y,marker="o")
  ```

- Linestyles
  
  ```py
  plt.plot(x,y,linewidth=4.0)
  plt.plot(x,y,ls='solid')
  plt.plot(x,y,ls='--')
  plt.plot(x,y,'--',x**2,y**2,'-.')
  plt.setp(lines,color='r',linewidth=4.0)
  ```

- Text & Annotations
  
  ```py
  ax.text(1, -2.1, 'Example Graph', style='italic')
  ax.annotate("Sine",
              xy=(8, 0),
              xycoords='data',
              xytext=(10.5, 0),
              textcoords='data',
              arrowprops=dict(arrowstyle="->", connectionstyle="arc3"),)
  ```

- Mathtext
  
  ```py
  plt.title(r'$sigma_i=15$', fontsize=20)
  ```

- Limits, Legends & Layouts
  
  - Limits & Autoscaling

    ```py
    # Add padding to a plot
    ax.margins(x=0.0,y=0.1)
    
    # Set the aspect ratio of the plot to 1
    ax.axis('equal')
    
    # Set limits for x-and y-axis
    ax.set(xlim=[0,10.5],ylim=[-1.5,1.5])
    
    # Set limits for x-axis
    ax.set_xlim(0,10.5)
    
    # Scale the plot axis to one of Transformation {"linear", "log", "symlog", "logit", ...}
    ax.xscale('log')
    ```

  - Legends

    ```py
    # Set a title and x-and y-axis labels
    ax.set(title='An Example Axes', ylabel='Y-Axis', xlabel='X-Axis')
    
    # No overlapping plot elements
    ax.legend(loc='best')
    ```

  - Ticks

    ```py
    # Manually set x-ticks
    ax.xaxis.set(ticks=range(1,5),ticklabels=[3,100,-12,"foo"])
    
    # Make y-ticks longer and go in and out
    ax.tick_params(axis='y', direction='inout', length=10)
    
    # Rotate x-axis ticks
    plt.xticks(rotation = 45)
    ```

  - Subplot Spacing

    ```py
    # Adjust the spacing between subplots
    fig3.subplots_adjust(wspace=0.5, hspace=0.3, left=0.125, right=0.9, top=0.9, bottom=0.1)
    
    # Fit subplot(s) in to the figure area
    fig.tight_layout()
    ```

  - Axis Spines

    ```py
    # Make the top axis line for a plot invisible
    ax1.spines['top'].set_visible(False)
    
    # Move the bottom axis line outward
    ax1.spines['bottom'].set_position(('outward',10))
    ```

### Save Plot

```py
#Save figures
plt.savefig('foo.png')

# Save transparent figures
plt.savefig('foo.png', transparent=True)
```

### Show Plot

```py
plt.show()
```

### Close & Clear

```py
# Clear an axis
plt.cla()

# Clear an entire figure
plt.clf()

# Close a window
plt.close()
```

### Matplotlib references

- [Python For Data Science MatPlotLib Cheat Sheet](https://s3.amazonaws.com/assets.datacamp.com/blog_assets/Python_Matplotlib_Cheat_Sheet.pdf)
- [How to rotate axis lables in seaborn and matplotlib](https://www.drawingfromdata.com/how-to-rotate-axis-labels-in-seaborn-and-matplotlib)

## Seaborn

- It is built on top of matplotlib, adds a number of functions to make common statistical visualizations easier to generate.
- [ScatterPlot Matrix](https://seaborn.pydata.org/examples/scatterplot_matrix.html)
- [countplot](https://seaborn.pydata.org/generated/seaborn.countplot.html): Draws a basic bar chart of frequencies for categorical variables. By default, each category is given a different color.
- [color_palette](https://seaborn.pydata.org/generated/seaborn.color_palette.html): returns a list of RGB tuples. Each tuple consists of three digits specifying the red, green, and blue channel values to specify a color. Calling this function without any parameters returns the current / default palette.

### Import seaborn library

```py
import matplotlib.pyplot as plt
import seaborn as sb

# countplot Draws a bar chart for categorical variables. By default, each category is given a different color. we take the first color to be the color for all bars.
base_color = sb.color_palette()[0]
cat_order = df['col_name'].value_counts().index
sb.countplot(data = df, x = 'col_name', color = base_color, order = cat_order)
```

### Basic Steps for creating plots with Seaborn

#### Step 1: Prepare the data

```py
# Seaborn offers built-in data sets
titanic = sb.load_dataset("titanic")
iris = sb.load_dataset("iris")
```

#### Step 2: Figure Aesthetics

- [subplot()](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.subplot.html)
- [figure()](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.figure.html): The method requires one list as argument specifying the dimensions of the Axes, the first two elements of the list indicate the position of the lower-left hand corner of the Axes and the last two elements specifying the Axes width and height.

Python first creates a Figure object. And since the Figure doesn't start with any Axes to draw the plot onto, an Axes object is created inside the Figure. Finally, the plot is drawn within that Axes.

```py
# Create a figure object
fig = plt.figure()

# Create Axes object
ax = fig.add_axes([.125, .125, .775, .755])

# OR
# Create a figure and one subplot
fig, ax = plt.subplots(figsize=(5,6))

# Plot the chart
ax.hist(data = df, x = 'cat_var')
# OR
sb.countplot(data = df, x = 'cat_var', color = base_color, ax = ax)
```

- Seaborn styles:

   ```py
   # (Re)set the seaborn default
   sb.set()

   # Set the matplotlib parameters
   sb.set_style("whitegrid")

   # Set the matplotlib parameters
   sb.set_style("ticks", {"xtick.major.size":8,"ytick.major.size":8})

   # Return a dict of params or use `with` to temporarily set the style
   sb.axes_style("whitegrid")
   ```

- Context Functions

   ```py
   # Set context to "talk"
   sb.set_context("talk")

   # Set context to "notebook", scale font elements and override param mapping
   sb.set_context("notebook", t_scale=1.5, rc={"lines.linewidth":2.5})
   ```

- Color Palette

   ```py
   # Define the color palette
   sb.set_palette("husl",3)

   # Use with `with` to temporarily set palette
   sb.color_palette("husl")

   # Set your own color palette
   flatui = ["#9b59b6","#3498db","#95a5a6","#e74c3c","#34495e","#2ecc71"]
   sb.set_palette(flatui)
   ```

#### Step 3: Plotting

- Axis Grids
- [FacetGrid](https://seaborn.pydata.org/generated/seaborn.FacetGrid.html)

   ```py
   # Subplot grid for plotting conditional relationships
   g = sb.FacetGrid(titanic, col="survived", row="gender")
   g = g.map(plt.hist,"age")

   # Draw a categorical plot onto a Facetgrid
   sb.factorplot(x="pclass", y="survived", hue="gender", data=titanic)

   # Plot data and regression model fits across a FacetGrid
   sb.lmplot(x="sepal_width", y="sepal_length", hue="species", data=iris)

   # Subplot grid for plotting pairwise relationships
   h = sb.PairGrid(iris)
   h = h.map(plt.scatter)

   # Plot pairwise bivariate distributions
   sb.pairplot(iris)

   # Grid for bivariate plot with marginal univariate plots
   i = sb.JointGrid(x="x", y="y", data=data)
   i = i.plot(sb.regplot, sb.distplot)

   # Plot bivariate distribution
   sb.jointplot("sepal_length", "sepal_width", data=iris, kind='kde')
   ```

- Categorical Plots

1. Scatterplot

   ```py
   # Scatterplot
   # Scatterplot with one categorical variable
   sb.stripplot(x="species", y="petal_length", data=iris)
   
   # Categorical scatterplot with non-overlapping points
   sb.swarmplot(x="species", y="petal_length", data=iris)
   ```

2. Bar Chart

   ```py
   # Show point estimates and confidence intervals with scatterplot glyphs
   sb.barplot(x="gender", y="survived", hue="class", data=titanic)
   ```

3. Count Plot

   ```py
   # Show count of observations
   sb.countplot(x="deck", data=titanic, palette="Greens_d")
   
   # Convert the column into an ordered categorical data type.
   # By default, pandas reads in string data as object types, and will plot the bars in the order in which the unique values were seen. By converting the data into an ordered type, the order of categories becomes innate to the feature, and we won't need to specify an "order" parameter each time it's required in a plot.
   level_order = ['Alpha', 'Beta', 'Gamma', 'Delta']
   ordered_cat = pd.api.types.CategoricalDtype(ordered = True,categories = level_order)
   # this method requires pandas v0.21 or later
   df['cat_var'] = df['cat_var'].astype(ordered_cat)
   
   # # use this method if you have pandas v0.20.3 or earlier
   # df['cat_var'] = df['cat_var'].astype('category', ordered = True,
   #                                      categories = level_order)
   
    base_color = sb.color_palette()[0]
    sb.countplot(data = df, x = 'cat_var', color = base_color)
   ```

4. Point Plot

   ```py
   # Show point estimates and confidence intervals as rectangular bars
   sb.pointplot(x="class", y="survived", hue="gender", data=titanic, palette={"male":"g", "female":"m"}, markers=["^","o"], linestyles=["-","--"])
   ```

5. Boxplot

   ```py
   # Boxplot
   sb.boxplot(x="alive", y="age", hue="adult_male", data=titanic)
   
   # Boxplot with wide-form data
   sb.boxplot(data=iris,orient="h")
   ```

6. Violinplot

   ```py
   # Violin plot
   sb.violinplot(x="age", y="gender", hue="survived", data=titanic)
   ```

- Regression Plots

   ```py
   # Plot data and a linear regression model fit
   sb.regplot(x="sepal_width", y="sepal_length", data=iris, ax=ax)
   ```

- Distribution Plots

   ```py
   # Plot univariate distribution
   plot = sb.distplot(df['col_name'], kde=False, color="b")
   ```

- Matrix Plots

   ```py
   # Heatmap
   sb.heatmap(uniform_data,vmin=0,vmax=1)
   ```

#### Step 4: Further Customizations

- Axisgrid Objects

   ```py
   # Remove left spine
   g.despine(left=True)

   # Set the labels of the y-axis
   g.set_ylabels("Survived")

   # Set the tick labels for x
   g.set_xticklabels(rotation=45)

   # Set the axis labels
   g.set_axis_labels("Survived", "gender")

   # Set the limit and ticks of the x-and y-axis
   h.set(xlim=(0,5), ylim=(0,5), xticks=[0,2.5,5], yticks=[0,2.5,5])
   ```

- Plot

   ```py
   # Add plot title
   plt.title("A Title")

   # Adjust the label of the y-axis
   plt.ylabel("Survived")

   # Adjust the label of the x-axis
   plt.xlabel("gender")

   # Adjust the limits of the y-axis
   plt.ylim(0,100)

   # Adjust the limits of the x-axis
   plt.xlim(0,10)

   # Adjust a plot property
   plt.setp(ax,yticks=[0,5])

   # Adjust subplot params
   plt.tight_layout()
   ```

#### Step 5: Show, Save, Close

- Show or Save Plot

   ```py
   # Show the plot
   plt.show()

   # Save the plot as a figure
   plt.savefig("foo.png")

   # Save transparent figure
   plt.savefig("foo.png", transparent=True)
   ```

- Close & Clear

   ```py
   # Clear an axis
   plt.cla()

   # Clear an entire figure
   plt.clf()

   # Close a window
   plt.close()
   ```

### Seaborn References

- [DataCamp Cheat Sheet](https://www.datacamp.com/community/blog/seaborn-cheat-sheet-python)

## Resources

- [Python For Data Science Cheat Sheet](https://pandas.pydata.org/Pandas_Cheat_Sheet.pdf)
- [Python for data analysis](http://www.ruxizhang.com/uploads/4/4/0/2/44023465/python_for_data_analysis.pdf)
- [NumPy and Pandas by Udacity](https://classroom.udacity.com/courses/ud170)
- [How to rotate x-lables](https://kite.com/python/answers/how-to-rotate-date-ticks-using-matplotlib-in-python#:~:text=Use%20matplotlib.,specified%20amount%20of%20degrees%20degrees%20) and [here](https://www.drawingfromdata.com/how-to-rotate-axis-labels-in-seaborn-and-matplotlib)
