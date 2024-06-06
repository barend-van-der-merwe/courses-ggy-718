[[Training Schedule]]

## Session 1
### Importing packages
For more specialized functionality, a large number (5,708,479) of python packages have been developed. These packages contain code that was developed by a third party (and therefore caution needs to be exercised when installing them) ([[Matthes2023]]). You can view a package as a collection of functions that you can make use of when writing your code.

In order to make use of these functions two steps need to be taken: the package needs to be installed using either conda or pip (see Day 1), and the package (or a function within the package) needs to be imported into your code using the `import` statement. When a package is imported, the name of the package needs to be stated before a function within that package can be executed. For example, `random.randint()` uses the function `randint()` that can be found within the `random` package.

To avoid having to write out the package name each time, which can be long in certain instances, the package can be loaded with an alias. Alternatively, you can import a function directly from the package. When you did this, it is not needed to specify the package name when calling the function.

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
Comma separated value files (`.csv`) are a very common file format used in data science. Since csv files are text files, they do not have the risks associated with proprietary file formats such as `.xlsx`. Python does have built-in support for loading csv through the `csv` package. However, if you are going to work with data, this package is not the most user-friendly. Therefore, we need to make use of another package, Pandas, in order to load the csv files.

Pandas introduces two new data structures that we did not look at earlier: Series and DataFrame ([[Vasiliev2022]]) (we will look at those in the next section). To understand these structures, it is best to draw on MS Excel as an example. A series in pandas essentially corresponds to a single column in MS Excel. It is similar to a list but differs in some notable ways. The first difference is that, while it is possible to have different types of data in a Series, this is not usually done in practice ([[Vasiliev2022]]). The second difference is that a Series corresponds to a 1D labelled array ([[Vasiliev2022]]). An array data structure is not included with the standard Python installation. It is a data structure that groups elements of the same data type ([[Vaughan2023]]). The labels used by default are integer values (that corresponds to the index of the value) but they can be changed to any value specified by the user ([[Vasiliev2022]]). Just as with a list, the index values can be used to extract the corresponding entry in the Series.

To load a csv file, the `read_csv()` function in the Pandas package is used.

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
### Extracting data from a DataFrame
#### Information about the DataFrame
he Pandas package is considered the de facto standard when it comes to working with data-centered python applications ([[Vasiliev2022]]). When a csv file is loaded into python (using pandas) it is stored as a DataFrame which is a Python class (which we will discuss a little later). A DataFrame is similar to the entire spreadsheet (i.e. it consists of multiple individual Series). Each column within the DataFrame can be of a different data type ([[Vasiliev2022]]). In some ways it is similar to the dictionary discussed earlier where the key corresponds to the label of the column ([[Vasiliev2022]]). This makes it possible to access individual columns by just specifying the name of the column.

The WeatherData.csv file we loaded contains the following information:
1. **temp**: Temperature in $^\circ C$
3. **dew**: The dew point temperature in $^\circ C$
4. **hum**: The humidity (%).
5. **wind**: Wind speed in $km.hr^{−1}$.
6. **vis**: The visibility at the time of observation in km.
7. **kpa**: The pressure at the time of observation in kilopascals.
8. **weather**: The weather at the time of observation

It is usually a good idea to extract a sample of the data after it has been loaded to check whether everything is in order. The top four rows of the DataFrame can be extracted using the `.head()` method. Using `shape` attribute (note that there are no brackets) we can obtain information on the size of the DataFrame (i.e. how many rows and columns does it have). Another method, `info()` can also be called to get more descriptive information about the DataFrame such as the column index, its heading, how many non-null values it contains, and what data type it contains.

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
#### Subsetting the DataFrame
Before we start an analysis, it may be beneficial to either extract data from the DataFrame or to subset the entire DataFrame based on some criteria. This is usually the case when a single DataFrame contains all of the data for the analysis. If we are working with an unknown dataset, we can use the `unique()` method to get the unique entries (i.e. removing all the duplicate entries) of a column within our DataFrame. This is more useful for data that are stored as strings or Booleans as opposed to data stored as either integers or floats.

If we are interested in extracting data at a specific point within the DataFrame, we can use the `.loc[]` and `.iloc[]` attributes and passing the appropriate values as the indices. We can extract selected rows by using the index method and specifying the columns as a list. If we want to extract rows that meet a certain criteria, then we can use a combination of index calls to do so.

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

# what data is in the weather column at index 1234
>>> weather_data["weather"].loc[1234]
'Mostly Cloudy'

# same question using iloc
>>> weather_data.iloc[1234,6]
'Mostly Cloudy'

# selecting multiple rows of data
>>> weather_data.loc[[1,2,3,4]]
   temp  dew  hum  wind  vis     kpa               weather
1  -1.8 -3.7   87     4  8.0  101.24                   Fog
2  -1.8 -3.4   89     7  4.0  101.26  Freezing Drizzle,Fog
3  -1.5 -3.2   88     6  4.0  101.27  Freezing Drizzle,Fog
4  -1.5 -3.3   88     7  4.8  101.23                   Fog

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
## Session 2
### Creating custom functions and classes
#### Custom functions
A function is a reusable set of instructions to perform a specific task ([[Vaughan2023]]). Functions typically contain parameters or arguments that are needed to complete the steps contained within the function ([[Vaughan2023]]). Although there are millions of functions available across the entire Python universe, it is sometimes more convenient to create your own functions rather than try and track one down online. To achieve this, we use a function definition.

A function definition makes use of parameters while a function call makes use of arguments ([[Vaughan2023]]). These arguments/parameters can either be positional or keyword based ([[Vaughan2023]]). Positional arguments must be provided in the correct order in order to work while keyword arguments are linked to specific keywords and can be in any order. Default values can also be created for parameters when the parameter is typically a specific value.

A variable can either have a local or a global scope. A global scope means a variable is accessible by any function within the program. A local scope means the variable is only accessible within the context of the function where it is used.

When creating functions, the `def` keyword is used followed by the name of the function, the parameters in brackets, and the finally a colon (`:`). The colon indicates to Python that the code that follows is part of the function that was just created. Custom functions can be saved in a dedicated file (in the same directory as your script file) using the `import` statement and the specifying the appropriate filename.

---
**Example**
```
# create a function using positional parameters that divides the first number
# given by the second number given.

# script
def division(a, b):
    answer = a/b
    return(answer)

print(division(10,5))
print(division(5,10))

# terminal
2.0
0.5

#create another function using keyword arguments that raises a number
# to a given exponent (set the default value of the exponent to 2)

# script
def power(number, exponent = 2):
    answer = number**exponent
    return(answer)

print(power(number = 2, exponent = 3))
print(power(exponent = 3, number = 2))
print(power(number = 2))

# terminal
8
8
4
```

#### Custom classes
Python classes are regularly used as part of the Object-oriented programming paradigm (OOP) ([[Matthes2023]]) and is used to create objects ([[Vaughan2023]]). The OOP paradigm focuses on grouping related data, functions and attributes together into classes ([[Vaughan2023]]). The benefits of this paradigm is often in larger programs where it can help reduce code duplication thereby making the code easier to update and to maintain ([[Vaughan2023]]). We have already worked with objects, the most recent being the DataFrame created by pandas. But anytime you create a variable you are creating an object.

As an example, let's consider an object clast that can be used to when we are investigating the shape of clasts. This object will have the following attributes: a-axis, b-axis, and c-axis.

```
# Script

class Clast:
    def __init__(self, a_axis, b_axis, c_axis):
        self.a_axis = a_axis
        self.b_axis = b_axis
        self.c_axis = c_axis

clast_1 = Clast(18.3, 5.3, 3)
print(clast_1.a_axis)

# Terminal
18.3
```

The statement `clast_1 = Clast(18.3, 5.3, 3)` instantiates an object of the class Clasts and requires as input the three axes specified. A new object is known as an instance of a class ([[Vaughan2023]]), so the term instantiation refers to the process of creating an instance (i.e. an object) of a class. Functions that exist within a class are referred to as either class functions or methods depending on how they are used (for the sake of simplicity we will only be using methods in this module). The `__init__()` method is a must in all definitions of a class since itis needed in order to create instances of that class. However, we do have the freedom to add whatever other methods we want to this class. Let's add a method to calculate the Zingg classification of the clast and add this classification to the objects attributes. As a refresher, the Zingg classification classifies the shape of a clast as being either a sphere, disc, rod, or blade  based on the following criteria:

| Zing Classification | $\frac{b-axis}{a-axis}$ | $\frac{c-axis}{b-axis}$ |
| ------------------- | ----------------------- | ----------------------- |
| Sphere              | $\geq 0.67$             | $\geq 0.67$             |
| Disc                | $\geq 0.67$             | $< 0.67$                |
| Rod                 | $< 0.67$                | $\geq 0.67$             |
| Blade               | $< 0.67$                | $< 0.67$                |

```
# Script

class Clast:
    def __init__(self, a_axis, b_axis, c_axis):
        self.a_axis = a_axis
        self.b_axis = b_axis
        self.c_axis = c_axis

    def zingg_class(self):
        b_a = self.b_axis/self.a_axis
        c_b = self.c_axis/self.b_axis
        if b_a >= 0.67 and c_b >= 0.67:
            self.zingg = "sphere"
        elif b_a >= 0.67 and c_b < 0.67:
            self.zingg = "disc"
        elif b_a < 0.67 and c_b >= 0.67:
            self.zingg = "rod"
        elif b_a < 0.67 and c_b < 0.67:
            self.zingg = "blade"

clast_1 = Clast(18.3, 5.3, 3)
clast_1.zingg_class()
print(clast_1.zingg)

# Terminal
blade
```

As can be seen, a method is simply a function definition within the class definition with the addition that  it has the `self` parameter passed to it.  This variable is just a reference to the instance itself. Just like custom functions, custom classes can also be saved to a dedicated file so that they can be imported into a script as needed.