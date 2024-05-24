[[Training Schedule]]

## Session 1
### Data structures
1. Data structures are used to organize and store data in python to make the task of data processing easier ([[Vasiliev2022]]).
2. Although there are many different types of data structures, python ships with four types of structure: lists, tuples, dictionaries, and sets ([[Vasiliev2022]]).
#### Lists
2. Lists are ordered collections of items that are mutable ([[Vasiliev2022]]).
3. By ordered it means that the sequence in which the items are entered into the list is considered relevant to python and it retains that order.
4. Mutable means that the list can be altered after it was created (using either a method or a function). This includes adding items to a list.
5. Lists are created using square brackets `[]`.
6. Lists can contain either contain items of the same data type or can contain a mixture of different data types ([[Vasiliev2022]]). Lists can even contain other lists.
7. This property is very useful since it allows for variables to be created that contain different types of data, for example rock lithology, aspect, surface temperature, and hardness readings.
8. It is also possible to retrieve a value within a list using an index value (in python these values start at 0, meaning that the first item in a list as an index of 0). List are indexed using the square brackets (`[]`). If a range of values are required, the list can be sliced using a colon as part of the index (i.e. `[:]`) where the starting index is to the left of the colon and the desired end index (+1) is to the right of the colon.
9. List comprehension is a technique that is similar to a loop (just more compact) and allows for a new list to be created from an existing list based on some criteria ([[Vaughan2023]]).
10. The table below contains some useful methods that can be applied to lists (adapted from [[Vasiliev2022]], [[McGrath2018]])

| Method                       | Description                                                  |
| ---------------------------- | ------------------------------------------------------------ |
| `my_list.append(x)`          | Add element x to the list named `my_list`.                   |
| `my_list.clear()`            | Removes all the items from `my_list`.                        |
| `my_list.count(x)`           | Counts the number of times element x appears in `my_list`.   |
| `my_list.extend(other list)` | Add all the elements of other list to the end of `my_list`.  |
| `my_list.index(x)`           | Find the index of element x in list `my_list`.               |
| `my_list.insert(i, x)`       | Insert element x into `my_list` at index i.                  |
| `my_list.pop(i)`             | Removes element from `my_list` at position i and returns it. |
| `my_list.remove(x)`          | Remove element x from list `my_list`.                        |
| `my_list.reverse()`          | Reverses all the items in list `my_list`.                    |
| `my_list.sort()`             | Sorts all the items in list `my_list`.                       |

---
**Example**
```
# the list below contain data on barchan dimensions published by Hamdan (2016)
>>> barchan_widths = [156.78, 176.6, 233.48, 157.37, 150.82, 231.11, 211.04, 171.17, 199.1, 383.75]

# The first value in this list is
>>> barchan_widths[0]
156.78

# Creating a slice of the data to retrieve the first 4 items
# remember the index of the fourth entry is 3
>>> barchan_widths[0:4]
[150.82, 156.78, 157.37, 171.17]

# Since it is mutable, we can rearrange it from low to high
>>> barchan_widths.sort()
>>> barchan_widths
[150.82, 156.78, 157.37, 171.17, 176.6, 199.1, 211.04, 231.11, 233.48, 383.75]

# create a new list that contain only values larger than 200
>>> barchan_widths_larger_200 = [i for i in barchan_widths if i >= 200]
>>> barchan_widths_larger_200
[211.04, 231.11, 233.48, 383.75]

# We can store data of different types
# The data contains name, Koppen classification, elevation and temperature
>>> site_data = ["Pretoria", ["C", "w", "a"], 1339, 18.7]

# We can index a list that is located within another list
>>> site_data[1][0]
'C'

# Adding rainfall data to site_data list
>>> site_data.append(732)
>>> site_data
['Pretoria', ['C', 'w', 'a'], 1339, 18.7, 732]
```
---
#### Tuples
1. Similar to lists, tuples are organized collections of items ([[Vasiliev2022]]). However, they differ from lists in that they are immutable ([[Vasiliev2022]]).
2. Immutable means that once a tuple is created, it cannot be changed afterwards.
3. Tuples are created using round brackets `()`.
4. Tuples can also contain a variety of different data types and can be indexed in the same way as lists.
5. The only methods that can be used on tuples are the ones that do not modify the tuple: `index()` and `count()`
---
**Example**
```
# creating a tuple containing the dimensions (l,w,h) of a cut rock
>>> sample = (57,49.5,21.6)

# retrieve the width (index = 1)
>>> sample[1]
49.5

# add the colour to the list
>>> sample.append("brown")
Traceback (most recent call last):
  File "<pyshell#22>", line 1, in <module>
    sample.append("brown")
AttributeError: 'tuple' object has no attribute 'append'
```
---
#### Dictionaries
1. Dictionaries are mutable, unordered collections of key-value pairs ([[Vasiliev2022]]).
2. Since they are mutable, it means that dictionaries can be altered after they have been created.
3. Since they are unordered, it means that they are not typically used when ordering is important (although the order in which the data was entered is maintained).
4. This is because dictionaries rely on key-value pairs to store and retrieve the data.
5. To retrieve the data, the key must be placed inside square brackets `[]`. This is similar to retrieving items from a list, except that you do not need to remember the index value, you just need to remember the key.
6. The key is a unique identifier that is used to identify a specific value ([[Vasiliev2022]]).
7. Dictionaries are created using curly brackets `{}`.
---
**Example**
```
# recreate the site data variable from earlier using a dictionary
>>> site_data_dict = {"name": "Pretoria", "koppen": ["C", "w", "a"], "elevation": 1339, "temp": 18.7, "rainfall": 732}

# retrieve the site's elevation
>>> site_data_dict["elevation"]
1339
```
---
### Sets
1. Set are collections of unordered unique items ([[Vaughan2023]]).
2. The unique criterion means that duplicate items are not stored (even though they may be included when the set is created).
3. Sets allow set operations (such as intersection and union) to be carried out ([[Vaughan2023]]).
4. Some additional methods that can be used on sets are given below:

| Method                                            | Description                                                                                                                                                                       |
| ------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `my_set.add(x)`                                   | Add item x to `my_set`                                                                                                                                                            |
| `my_set.clear()`                                  | Removes all items from `my_set` (i.e. change it to an empty set).                                                                                                                 |
| `my_set.difference(another_set)`                  | Returns the items in `my_set` that are not present in `another_set`                                                                                                               |
| `my_set.difference_update(another_set)`           | Replaces the value of `my_set` with the results of the `difference()` method.                                                                                                     |
| `my_set.discard(x)`                               | Removes the item x from `my_set`.                                                                                                                                                 |
| `my_set.intersection(another_set)`                | Returns the items that occur in both `my_set` and `another_set`.                                                                                                                  |
| `my_set.isdisjoint(another_set)`                  | Returns `False` if `my_set` and `another_set` have common items. Returns `True` if they do not have common items.                                                                 |
| `my_subset.issubset(another_set)`                 | Returns `True` if `my_set` is a subset of `another_set`. It returns `False` otherwise.                                                                                            |
| `my_subset.issuperset(another_set)`               | Returns `True` if `my_set` is a superset of `another_set`. It returns `False` otherwise.                                                                                          |
| `my_set.pop()`                                    | Removes the item at index = 0 from `my_set`.                                                                                                                                      |
| `my_set.remove(x)`                                | Removes item x from `my_set`.                                                                                                                                                     |
| `my_set.symmetric_difference(another_set)`        | Returns the symmetric difference between `my_set` and `another_set` (i.e. items that are in both sets but which are not common to both sets). It is the opposite of intersection. |
| `my_set.symmetric_difference_update(another_set)` | Replaces the current value of `my_set` with the symmetric difference between `my_set` and `another_set`.                                                                          |
| `my_set.union(another_set)`                       | Returns a new set that represents the union between `my_set` and `another_set`.                                                                                                   |
| `my_set.update(another_set)`                      | Replaces the value of `my_set` with the union between `my_set` and `another_set`.                                                                                                 |

---
**Example**
```
# create a set of the lithologies considered in a study
# Note that slate has been added twice but only appears once
>>> lithologies = {"sandstone", "slate", "marble", "gabbro", "slate"}
>>> lithologies
{'marble', 'sandstone', 'gabbro', 'slate'}

# create two sets that contain the tombstone lithologies
# of two different cemetaries
>>> cemetery_1 = {"sandstone", "marble", "limestone"}
>>> cemetery_2 = {"limestone", "gabbro", "granite"}

# check which items are in cemetery_1 but not in cemetery_2
>>> cemetery_1.difference(cemetery_2)
{'sandstone', 'marble'}

# check which lithology occurs in both cemetery_1 and cemetery_2
>>> cemetery_1.intersection(cemetery_2)
{'limestone'}

# test if there are common lithologies between cemetery_1 and cemetery_2
>>> cemetery_1.isdisjoint(cemetery_2)
False # Yes, there are lithologies that occur in both cemeteries

# check which lithologies are not shared between cemetery_1 and cemetery_2
>>> cemetery_1.symmetric_difference(cemetery_2)
{'marble', 'gabbro', 'granite', 'sandstone'}

# check which litholgies were observed for both cemeteries combined
>>> cemetery_1.union(cemetery_2)
{'limestone', 'granite', 'sandstone', 'marble', 'gabbro'}
```
---
## Session 2
### Importing packages
1. For more specialized functionality, a large number (5,708,479) of python packages have been developed.
2. These packages contain code that was developed by a third party (and therefore caution needs to be exercised when installing them) ([[Matthes2023]]).
3. You can view a package as a collection of functions that you can make use of when writing your code.
4. In order to make use of these functions two steps need to be taken: the package needs to be installed using either conda or pip (see Day 1), and the package (or a function within the package) needs to be imported into your code using the `import` statement.
5. When a package is imported, the name of the package needs to be stated before a function within that package can be executed. For example, `random.randint()` uses the function `randint()` that can be found within the `random` package.
6. To avoid having to write out the package name each time, which can be long in certain instances, the package can be loaded with an alias.
7. Alternatively, you can import a function directly from the package. When you did this, it is not needed to specify the package name when calling the function.
---
**Example**
```
# importing the random module
>>> import random

# using the randint function from the random package
# to return a random integer between 1 and 100
>>> random.randint(1,100)
56

# importing the numpy package and renaming it
>>> import numpy as np

# use the log2() function to calculate the phi sizes 
# of particles in a list
>>> particle_sizes = [0.0625, 0.125, 0.25, 0.5, 1, 1.5, 2]
>>> np.log2(particle_sizes)*-1
array([ 4.       ,  3.       ,  2.       ,  1.       , -0.       ,
       -0.5849625, -1.       ])

# importing the sqrt() function from the math package
>>> from math import sqrt
>>> sqrt(16)
4.0
```
---
### Loading .csv files
1. Comma separated value files (.csv) are a very common file format used in data science.
2. Since csv files are text files, they do not have the risks associated with proprietary file formats such as xlsx.
3. Python does not have built-in support for loading csv files in such a way as to facilitate data analysis.
4. Therefore, we need to make use of another package, Pandas, in order to load the csv files.
5. Pandas introduces two new data structures that we did not look at earlier: Series and DataFrame ([[Vasiliev2022]]) (we will look at those in the next section).
6. To understand these structures, it is best to draw on MS Excel as an example.
7. A series in pandas essentially corresponds to a single column in MS Excel. It is similar to a list but differs in some notable ways.
8. The first difference is that, while it is possible to have different types of data in a Series, this is not usually done in practice ([[Vasiliev2022]]).
9. The second difference is that a Series corresponds to a 1D labelled array ([[Vasiliev2022]]). An array data structure is not included with the standard Python installation. It is a data structure that groups elements of the same data type ([[Vaughan2023]]). The labels used by default are integer values (that corresponds to the index of the value) but they can be changed to any value specified by the user ([[Vasiliev2022]]). Just as with a list, the index values can be used to extract the corresponding entry in the Series.
12. To load a csv file, the `read_csv()` function in the Pandas package is used.
---
**Example**
```
# import pandas package
>>> import pandas as pd

# load the file weatherData.csv
>>> weather_data = pd.read_csv("weatherData.csv")

# check the type of data structure
type(weather_data)
<class 'pandas.core.frame.DataFrame'>

# create a series using pandas
>>> barchan_widths = [156.78, 176.6, 233.48, 157.37, 150.82, 231.11, 211.04, 171.17, 199.1, 383.75]
>>> barchan_widths_series = pd.Series(barchan_widths)
>>> barchan_widths_series
0    156.78
1    176.60
2    233.48
3    157.37
4    150.82
5    231.11
6    211.04
7    171.17
8    199.10
9    383.75
dtype: float64

# change the labels of the Series to correspond to the original data
# entries provided by Hamdan (2016)
>>> dune_labels = [67, 106, 25, 64, 47, 72, 35, 65, 17, 27]
>>> barchan_widths_series = pd.Series(barchan_widths, index = dune_labels)
barchan_widths_series
67     156.78
106    176.60
25     233.48
64     157.37
47     150.82
72     231.11
35     211.04
65     171.17
17     199.10
27     383.75
dtype: float64

# extract the width data of dune 65
>>> barchan_widths_series[65]
171.17
```
---
### Basic data analysis using Pandas
#### Information about the DataFrame
1. The Pandas package is considered the de facto standard when it comes to working with data-centered python applications ([[Vasiliev2022]]).
2. When a csv file is loaded into python (using pandas) it is stored as a DataFrame.
3. A DataFrame is similar to the entire spreadsheet (i.e. it consists of multiple individual Series). Each column within the DataFrame can be of a different data type ([[Vasiliev2022]]). In some ways it is similar to the dictionary discussed earlier where the key corresponds to the label of the column ([[Vasiliev2022]]). This makes it possible to access individual columns by just specifying the name of the column.
4. The WeatherData.csv file we loaded contains the following information:
	1. **temp**: Temperature in $^\circ C$
	3. **dew**: The dew point temperature in $^\circ C$
	4. **hum**: The humidity (%).
	5. **wind**: Wind speed in $km.hr^{−1}$.
	6. **vis**: The visibility at the time of observation in km.
	7. **kpa**: The pressure at the time of observation in kilopascals.
	8. **weather**: The weather at the time of observation
5. The top four rows of the DataFrame can be extracted using the `.head()` method. This is often useful to get an idea of what the data looks like.
6. The `shape` method (no brackets) is used to obtain information on the size of the DataFrame (i.e. how many rows and columns does it have).
7. Another method, `info()` can also be called to get more descriptive information about the DataFrame such as the column index, its heading, how many non-null values it contains, and what data type it contains.
---
**Example**
```
# display the first four rows of the DataFrame weather_data
>>> weather_data.head()
   temp  dew  hum  wind  vis     kpa               weather
0  -1.8 -3.9   86     4  8.0  101.24                   Fog
1  -1.8 -3.7   87     4  8.0  101.24                   Fog
2  -1.8 -3.4   89     7  4.0  101.26  Freezing Drizzle,Fog
3  -1.5 -3.2   88     6  4.0  101.27  Freezing Drizzle,Fog
4  -1.5 -3.3   88     7  4.8  101.23                   Fog

# determine the size of the DataFrame weather_data
>>> weather_data.shape
(8784, 7) # it contains 8784 rows and 7 columns

# get some more detailed information regarding the DaaFrame weather_data.csv
>>> weather_data.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 8784 entries, 0 to 8783
Data columns (total 7 columns):
 #   Column   Non-Null Count  Dtype  
---  ------   --------------  -----  
 0   temp     8784 non-null   float64
 1   dew      8784 non-null   float64
 2   hum      8784 non-null   int64  
 3   wind     8784 non-null   int64  
 4   vis      8784 non-null   float64
 5   kpa      8784 non-null   float64
 6   weather  8784 non-null   object 
dtypes: float64(4), int64(2), object(1)
memory usage: 480.5+ KB
```
---
#### Extracting data from the DataFrame
1. Before we start an analysis, it may be beneficial to either extract data from the DataFrame or to subset the entire DataFrame based on some criteria.
2. For example, we can use the `unique()` method to get the unique entries (i.e. removing all the duplicate entries) of a column within our DataFrame.
3. We can use the `.loc()` method to extract a complete row of our DataFrame.
4. We can extract selected rows by using the index method and specifying the columns as a list.
5. If we want to extract rows that meet a certain criteria, then we can use a combination of index calls to do so.
---
**Example**
```
# what are the unique weather observations in the weather column of
# the dataframe weather_data?
>>> weather_data['weather'].unique()
array(['Fog', 'Freezing Drizzle,Fog', 'Mostly Cloudy', 'Cloudy', 'Rain',
       'Rain Showers', 'Mainly Clear', 'Snow Showers', 'Snow', 'Clear',
       'Freezing Rain,Fog', 'Freezing Rain', 'Freezing Drizzle',
       'Rain,Snow', 'Moderate Snow', 'Freezing Drizzle,Snow',
       'Freezing Rain,Snow Grains', 'Snow,Blowing Snow', 'Freezing Fog',
       'Haze', 'Rain,Fog', 'Drizzle,Fog', 'Drizzle',
       'Freezing Drizzle,Haze', 'Freezing Rain,Haze', 'Snow,Haze',
       'Snow,Fog', 'Snow,Ice Pellets', 'Rain,Haze', 'Thunderstorms,Rain',
       'Thunderstorms,Rain Showers', 'Thunderstorms,Heavy Rain Showers',
       'Thunderstorms,Rain Showers,Fog', 'Thunderstorms',
       'Thunderstorms,Rain,Fog',
       'Thunderstorms,Moderate Rain Showers,Fog', 'Rain Showers,Fog',
       'Rain Showers,Snow Showers', 'Snow Pellets', 'Rain,Snow,Fog',
       'Moderate Rain,Fog', 'Freezing Rain,Ice Pellets,Fog',
       'Drizzle,Ice Pellets,Fog', 'Drizzle,Snow', 'Rain,Ice Pellets',
       'Drizzle,Snow,Fog', 'Rain,Snow Grains', 'Rain,Snow,Ice Pellets',
       'Snow Showers,Fog', 'Moderate Snow,Blowing Snow'], dtype=object)

# What are the observations recorded at index 1234?
>>> weather_data.loc[1234]
temp                -1.4
dew                 -7.0
hum                   66
wind                  11
vis                 48.3
kpa               101.72
weather    Mostly Cloudy
Name: 1234, dtype: object

# extract all of the rows were the temperature observation is greater than 9.3
>>> temp_greater_9_3 = weather_data[weather_data['temp']>9.3]

# create a new dataframe that contains only humidity and visibility data
>>> hum_and_vis = weather_data[["hum", "vis"]]
>>> hum_and_vis.head()
   hum  vis
0   86  8.0
1   87  8.0
2   89  4.0
3   88  4.0
4   88  4.8

# display the first four rows
>>> temp_greater_9_3.head()
      temp  dew  hum  wind   vis     kpa        weather
1599   9.7 -2.7   42    13  24.1  101.36   Mainly Clear
1600  11.4 -2.3   38    15  24.1  101.31  Mostly Cloudy
1601   9.9 -1.9   44     9  24.1  101.25  Mostly Cloudy
1611  10.1 -0.9   46    24  25.0  100.69  Mostly Cloudy
1612  10.0 -0.7   47    28  25.0  100.64  Mostly Cloudy

# display the numbers of rows and columns
>>> temp_greater_9_3.shape
(4379, 7)
```
---