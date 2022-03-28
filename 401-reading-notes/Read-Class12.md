## What kind of data does pandas handle?

Reading from [pandas](https://pandas.pydata.org/pandas-docs/stable/getting_started/intro_tutorials/01_table_oriented.html)

Reading from [Pandas reading](https://canvas.instructure.com/courses/4333667/discussion_topics/14075569)

I want to start using pandas
```
import pandas as pd
```
To load the pandas package and start working with it, import the package. The community agreed alias for pandas is pd, so loading pandas as pd is assumed standard practice for all of the pandas documentation.


I want to store passenger data of the Titanic. For a number of passengers, I know the name (characters), age (integers) and sex (male/female) data.
```
df = pd.DataFrame(
    {
        "Name": [
            "Braund, Mr. Owen Harris",
            "Allen, Mr. William Henry",
            "Bonnell, Miss. Elizabeth",
        ],
        "Age": [22, 35, 58],
        "Sex": ["male", "male", "female"],
    }
)


df
Out[3]: 
                       Name  Age     Sex
0   Braund, Mr. Owen Harris   22    male
1  Allen, Mr. William Henry   35    male
2  Bonnell, Miss. Elizabeth   58  female
```
To manually store data in a table, create a DataFrame. When using a Python dictionary of lists, the dictionary keys will be used as column headers and the values in each list as columns of the DataFrame.

A DataFrame is a 2-dimensional data structure that can store data of different types (including characters, integers, floating point values, categorical data and more) in columns. It is similar to a spreadsheet, a SQL table or the data.frame in R.

The table has 3 columns, each of them with a column label. The column labels are respectively Name, Age and Sex.

The column Name consists of textual data with each value a string, the column Age are numbers and the column Sex is textual data.

In spreadsheet software, the table representation of our data would look very similar:

>Each column in a DataFrame is a Series


---------------------------------------------------

I’m just interested in working with the data in the column Age
```
df["Age"]
Out[4]: 
0    22
1    35
2    58
Name: Age, dtype: int64
```
When selecting a single column of a pandas DataFrame, the result is a pandas Series. To select the column, use the column label in between square brackets [].

>If you are familiar to Python dictionaries, the selection of a single column is very similar to selection of dictionary values based on the key.

You can create a Series from scratch as well:
```
ages = pd.Series([22, 35, 58], name="Age")

ages
Out[6]: 
0    22
1    35
2    58
Name: Age, dtype: int64
```
A pandas Series has no column labels, as it is just a single column of a DataFrame. A Series does have row labels.

Do something with a DataFrame or Series
I want to know the maximum Age of the passengers

We can do this on the DataFrame by selecting the Age column and applying max():
```
df["Age"].max()
Out[7]: 58
Or to the Series:
```
```
ages.max()
Out[8]: 58
```
As illustrated by the max() method, you can do things with a DataFrame or Series. pandas provides a lot of functionalities, each of them a method you can apply to a DataFrame or Series. As methods are functions, do not forget to use parentheses ().

I’m interested in some basic statistics of the numerical data of my data table
```
df.describe()
Out[9]: 
             Age
count   3.000000
mean   38.333333
std    18.230012
min    22.000000
25%    28.500000
50%    35.000000
75%    46.500000
max    58.000000
```
The describe() method provides a quick overview of the numerical data in a DataFrame. As the Name and Sex columns are textual data, these are by default not taken into account by the describe() method.

Many pandas operations return a DataFrame or a Series. The describe() method is an example of a pandas operation returning a pandas Series or a pandas DataFrame.

**REMEMBER**
- Import the package, aka import pandas as pd

- A table of data is stored as a pandas DataFrame

- Each column in a DataFrame is a Series

- You can do things by applying a method to a DataFrame or Series
  
## How do I read and write tabular data?

I want to analyze the Titanic passenger data, available as a CSV file.

titanic = pd.read_csv("data/titanic.csv")
pandas provides the read_csv() function to read data stored as a csv file into a pandas DataFrame. pandas supports many different file formats or data sources out of the box (csv, excel, sql, json, parquet, …), each of them with the prefix read_*.

Make sure to always have a check on the data after reading in the data. When displaying a DataFrame, the first and last 5 rows will be shown by default:

```
titanic
Out[3]: 
     PassengerId  Survived  Pclass                                               Name  ...            Ticket     Fare  Cabin  Embarked
0              1         0       3                            Braund, Mr. Owen Harris  ...         A/5 21171   7.2500    NaN         S
1              2         1       1  Cumings, Mrs. John Bradley (Florence Briggs Th...  ...          PC 17599  71.2833    C85         C
2              3         1       3                             Heikkinen, Miss. Laina  ...  STON/O2. 3101282   7.9250    NaN         S
3              4         1       1       Futrelle, Mrs. Jacques Heath (Lily May Peel)  ...            113803  53.1000   C123         S
4              5         0       3                           Allen, Mr. William Henry  ...            373450   8.0500    NaN         S
..           ...       ...     ...                                                ...  ...               ...      ...    ...       ...
886          887         0       2                              Montvila, Rev. Juozas  ...            211536  13.0000    NaN         S
887          888         1       1                       Graham, Miss. Margaret Edith  ...            112053  30.0000    B42         S
888          889         0       3           Johnston, Miss. Catherine Helen "Carrie"  ...        W./C. 6607  23.4500    NaN         S
889          890         1       1                              Behr, Mr. Karl Howell  ...            111369  30.0000   C148         C
890          891         0       3                                Dooley, Mr. Patrick  ...            370376   7.7500    NaN         Q

[891 rows x 12 columns]
```

I want to see the first 8 rows of a pandas DataFrame.


```
titanic.head(8)
Out[4]: 
   PassengerId  Survived  Pclass                                               Name  ...            Ticket     Fare  Cabin  Embarked
0            1         0       3                            Braund, Mr. Owen Harris  ...         A/5 21171   7.2500    NaN         S
1            2         1       1  Cumings, Mrs. John Bradley (Florence Briggs Th...  ...          PC 17599  71.2833    C85         C
2            3         1       3                             Heikkinen, Miss. Laina  ...  STON/O2. 3101282   7.9250    NaN         S
3            4         1       1       Futrelle, Mrs. Jacques Heath (Lily May Peel)  ...            113803  53.1000   C123         S
4            5         0       3                           Allen, Mr. William Henry  ...            373450   8.0500    NaN         S
5            6         0       3                                   Moran, Mr. James  ...            330877   8.4583    NaN         Q
6            7         0       1                            McCarthy, Mr. Timothy J  ...             17463  51.8625    E46         S
7            8         0       3                     Palsson, Master. Gosta Leonard  ...            349909  21.0750    NaN         S

[8 rows x 12 columns]
```
To see the first N rows of a DataFrame, use the head() method with the required number of rows (in this case 8) as argument.

>Interested in the last N rows instead? pandas also provides a tail() method. For example, titanic.tail(10) will return the last 10 rows of the DataFrame.


A check on how pandas interpreted each of the column data types can be done by requesting the pandas dtypes attribute:

```
titanic.dtypes
Out[5]: 
PassengerId      int64
Survived         int64
Pclass           int64
Name            object
Sex             object
Age            float64
SibSp            int64
Parch            int64
Ticket          object
Fare           float64
Cabin           object
Embarked        object
dtype: object
```
For each of the columns, the used data type is enlisted. The data types in this DataFrame are integers (int64), floats (float64) and strings (object).

>When asking for the dtypes, no brackets are used! dtypes is an attribute of a DataFrame and Series. Attributes of DataFrame or Series do not need brackets. Attributes represent a characteristic of a DataFrame/Series, whereas a method (which requires brackets) do something with the DataFrame/Series as introduced in the first tutorial.


## How do I select specific columns from a DataFrame?

I’m interested in the age of the Titanic passengers.
```
ages = titanic["Age"]

ages.head()
Out[5]: 
0    22.0
1    38.0
2    26.0
3    35.0
4    35.0
Name: Age, dtype: float64
```
To select a single column, use square brackets [] with the column name of the column of interest.

Each column in a DataFrame is a Series. As a single column is selected, the returned object is a pandas Series. We can verify this by checking the type of the output:
```
type(titanic["Age"])
Out[6]: pandas.core.series.Series
And have a look at the shape of the output:

titanic["Age"].shape
Out[7]: (891,)
```
DataFrame.shape is an attribute (remember tutorial on reading and writing, do not use parentheses for attributes) of a pandas Series and DataFrame containing the number of rows and columns: (nrows, ncolumns). A pandas Series is 1-dimensional and only the number of rows is returned.

I’m interested in the age and sex of the Titanic passengers.
```
age_sex = titanic[["Age", "Sex"]]

age_sex.head()
Out[9]: 
    Age     Sex
0  22.0    male
1  38.0  female
2  26.0  female
3  35.0  female
4  35.0    male
```
To select multiple columns, use a list of column names within the selection brackets [].

**Note**
>The inner square brackets define a Python list with column names, whereas the outer brackets are used to select the data from a pandas DataFrame as seen in the previous example.

The returned data type is a pandas DataFrame:
```
type(titanic[["Age", "Sex"]])
Out[10]: pandas.core.frame.DataFrame
titanic[["Age", "Sex"]].shape
Out[11]: (891, 2)
```
The selection returned a DataFrame with 891 rows and 2 columns. Remember, a DataFrame is 2-dimensional with both a row and column dimension.

## How to create plots in pandas?

I want a quick visual check of the data.
```
air_quality.plot()
Out[5]: <AxesSubplot:xlabel='datetime'>
../../_images/04_airqual_quick.png
```
With a DataFrame, pandas creates by default one line plot for each of the columns with numeric data.

I want to plot only the columns of the data table with the data from Paris.
```
air_quality["station_paris"].plot()
Out[6]: <AxesSubplot:xlabel='datetime'>
../../_images/04_airqual_paris.png
```
To plot a specific column, use the selection method of the subset data tutorial in combination with the plot() method. Hence, the plot() method works on both Series and DataFrame.

I want to visually compare the  values measured in London versus Paris.
```
air_quality.plot.scatter(x="station_london", y="station_paris", alpha=0.5)
Out[7]: <AxesSubplot:xlabel='station_london', ylabel='station_paris'>
../../_images/04_airqual_scatter.png
```
Apart from the default line plot when using the plot function, a number of alternatives are available to plot data. Let’s use some standard Python to get an overview of the available plot methods:
```
[
    method_name
    for method_name in dir(air_quality.plot)
    if not method_name.startswith("_")
]

Out[8]: 
['area',
 'bar',
 'barh',
 'box',
 'density',
 'hexbin',
 'hist',
 'kde',
 'line',
 'pie',
 'scatter']
Note
```

In many development environments as well as IPython and Jupyter Notebook, use the TAB button to get an overview of the available methods, for example air_quality.plot. + TAB.

One of the options is DataFrame.plot.box(), which refers to a boxplot. The box method is applicable on the air quality example data:
```
air_quality.plot.box()
Out[9]: <AxesSubplot:>
```