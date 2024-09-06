#### Introduction
- [**Overview**](https://www.youtube.com/watch?v=DkjCaAMBGWM&t=0):
  - This video covers essential techniques for using the Pandas library in Python to perform data manipulation and wrangling.
  - Pandas is a widely used Python library for handling data, especially now with its integration into Excel.
  - The video condenses key functions based on extensive experience to help both beginners and advanced users effectively use Pandas.

#### Setting Up the Environment
- [**Importing Libraries**](https://www.youtube.com/watch?v=DkjCaAMBGWM&t=0):
  - Begin by importing Pandas and printing system information and the Pandas version.
  - The IDE used in the video is Jupyter Lab with a solarized dark theme.

#### Reading and Writing Data
- [**Reading Data**](https://www.youtube.com/watch?v=DkjCaAMBGWM&t=90):
  - Pandas can read various file types (CSV, Excel, etc.) using methods that start with `read_` (e.g., `read_csv`).
  - Common parameters for reading files include the delimiter, use of specific columns, date parsing, and chunking for large files.
  - Example: `df = pd.read_csv('data.csv', delimiter='\t', usecols=['column1', 'column2'], parse_dates=['date_column'])`.

- [**Writing Data**](https://www.youtube.com/watch?v=DkjCaAMBGWM&t=186):
  - DataFrames can be written to different file types or databases using methods like `to_csv` and `to_sql`.
  - Example: `df.to_csv('output.csv', index=False)` to save a DataFrame without saving the index.

#### Understanding Your DataFrame
- [**Exploring DataFrame Structure**](https://www.youtube.com/watch?v=DkjCaAMBGWM&t=220):
  - `.head()` displays the first 5 rows; `.tail()` displays the last 5 rows.
  - `.sample()` extracts a random subset of rows, with options for a fixed number or a fraction of rows.
  - `.columns` provides a list of column names, and `.index` gives the index values.
  - `.info()` lists the size, columns, data types, and memory usage of the DataFrame.
  - `.describe()` generates descriptive statistics for numeric columns and frequency statistics for non-numeric columns.
  - `.shape` returns the number of rows and columns, and `len()` yields the number of rows.

#### Subsetting and Filtering Data
- [**Subsetting Columns and Rows**](https://www.youtube.com/watch?v=DkjCaAMBGWM&t=371):
  - Columns can be subsetted by providing a list within brackets: `df[['column1', 'column2']]`.
  - Slicing can subset columns dynamically, such as selecting the first or last few columns.
  - Advanced subsetting using list comprehensions to filter columns based on specific criteria, like columns containing certain text: `df[[col for col in df.columns if 'time' in col]]`.

#### Advanced Subsetting and Filtering
- [**Filtering Columns by Data Type**](https://www.youtube.com/watch?v=DkjCaAMBGWM&t=443.):
  - Use `select_dtypes` to return a subset of columns based on their data type.
  - Example: `df.select_dtypes(include='int')` returns only integer columns.

- [**Selecting Single Columns**](https://www.youtube.com/watch?v=DkjCaAMBGWM&t=455.):
  - Providing a single column name returns a Series: `df['column']`.
  - To get a DataFrame with a single column, use double brackets: `df[['column']]`.

- [**Row Subsetting with `iloc` and `loc`**](https://www.youtube.com/watch?v=DkjCaAMBGWM&t=479):
  - `iloc` uses index locations to access data, while `loc` uses labels.
  - Example with `iloc`: `df.iloc[1, 3]` accesses the element at the second row and fourth column (indexing starts at 0).
  - `iloc` can also slice: `df.iloc[:5, :5]` returns the first 5 rows and columns.
  - Example with `loc`: `df.loc[condition]` where `condition` is a boolean expression.

#### Boolean Indexing
- [**Boolean Filtering with `loc`**](https://www.youtube.com/watch?v=DkjCaAMBGWM&t=589):
  - Create boolean conditions to filter rows, e.g., `df.loc[df['Airline'] == 'Spirit Airlines']`.
  - Combine multiple conditions using `&` (and) or `|` (or) operators.
  - Use `~` to invert a boolean condition.

- [**Query Method**](https://www.youtube.com/watch?v=DkjCaAMBGWM&t=651):
  - Use `query()` for string-based boolean filtering: `df.query('DepartureTime > 1130 & Origin == "JFK"')`.
  - Access external variables with `@` in the query string.
  
- **Practical Application**:
  - The boxplot is used to compare multiple teams by adding additional data for a third team, the New England Revolution. The plot shows the difference in player quality between this team and the stronger teams like FC Barcelona and Real Madrid.
  - By adjusting the figure size and adding labels, the plot is made more informative and visually appealing.

```python
"Box and Whisker Example"

plt.style.use('default')
plt.figure(figsize=(5,8))
barcelona = fifa.loc[fifa.Club=='FC Barcelona']['Overall']
madrid = fifa.loc[fifa.Club=='Real Madrid']['Overall']
revs = fifa.loc[fifa.Club=='New England Revolution']['Overall']
labels=['FC Barcelona','Real Madrid','NE Revolution']
boxes = plt.boxplot([barcelona, madrid, revs],labels=labels, patch_artist=True, medianprops={'linewidth':2})

for box in boxes['boxes']:
	box.set(color='orange', linewidth=2, facecolor='green')

plt.title('Professional Soccer Team Comparison')
plt.show()
```

#### Summarizing Data
- [**Basic Statistics**](https://www.youtube.com/watch?v=DkjCaAMBGWM&t=696):
  - Methods include `mean()`, `min()`, `max()`, `std()`, `var()`, `count()`, `sum()`, and `quantile()`.
  - Example: `df['column'].mean()` returns the mean of a column.
  - `quantile()` can take a list to return multiple quantiles.

- [**Aggregation with `agg`**](https://www.youtube.com/watch?v=DkjCaAMBGWM&t=742):
  - Use `agg()` to run multiple statistics on columns: `df.agg(['mean', 'std'])`.
  - `agg()` can also take a dictionary: `df.agg({'column1': ['mean', 'std'], 'column2': ['sum']})`.

- [**Categorical Summarization**](https://www.youtube.com/watch?v=DkjCaAMBGWM&t=77):
  - Methods for categorical data: `unique()`, `nunique()`, `value_counts()`.
  - Example: `df['column'].value_counts(normalize=True)` gives the fraction of each unique value.

#### Advanced Column Methods
- [**Ranking and Shifting**](https://www.youtube.com/watch?v=DkjCaAMBGWM&t=841):
  - `rank()` computes the rank of values in a column.
  - `shift()` shifts values up or down by a specified number.

- [**Cumulative Calculations**](https://www.youtube.com/watch?v=DkjCaAMBGWM&t=874):
  - `cumsum()`, `cummax()`, `cummin()` for cumulative operations on a series or DataFrame.

#### Advanced Aggregations and Rolling Calculations
- [**Rolling Method**](https://www.youtube.com/watch?v=DkjCaAMBGWM&t=892):
  - Apply rolling calculations by specifying a window period.
  - Example: `df['column'].rolling(window=5).mean()` calculates the rolling mean over a window of 5 periods.
  - Features include setting `center=True` to center the rolling window.

- [**Clip Values**](https://www.youtube.com/watch?v=DkjCaAMBGWM&t=923.):
  - Use `clip()` to limit values to a specified range.
  - Example: `df['column'].clip(lower=1000, upper=2000)` clips values below 1000 and above 2000.

#### Grouping and Aggregating Data
- [**Group By**](https://www.youtube.com/watch?v=DkjCaAMBGWM&t=948.):
  - Group data using `groupby()` and apply aggregate functions.
  - Example: `df.groupby('Airline')['DepartureDelay'].mean()` calculates the average departure delay for each airline.
  - Use `agg()` to run multiple aggregations: `df.groupby('Airline').agg({'DepartureDelay': ['mean', 'std']})`.

#### Creating and Sorting New Columns
- [**Creating New Columns**](https://www.youtube.com/watch?v=DkjCaAMBGWM&t=1012):
  - Perform operations on a column to create new columns.
  - Example: `df['DepartureTime2'] = df['DepartureTime'] / 60`.
  - Use `assign()` for chaining operations: `df.assign(DepartureTime3=df['DepartureTime'] / 60)`.

- [**Sorting Data**](https://www.youtube.com/watch?v=DkjCaAMBGWM&t=1054):
  - Sort data using `sort_values()` by specifying columns.
  - Example: `df.sort_values('ArrivalDelay', ascending=False)`.
  - Chain with `reset_index(drop=True)` to reset the index after sorting.

#### Handling Missing Data
- [**Identifying and Handling Missing Values**](https://www.youtube.com/watch?v=DkjCaAMBGWM&t=1111.):
  - Identify missing values with `isna()` and count them with `sum()`.
  - Example: `df['ArrivalDelay'].isna().sum()` counts NaNs.
  - Drop rows with `dropna(subset=['column'])` or fill them with `fillna(value)`.

#### Combining DataFrames
- [**Concatenation**](https://www.youtube.com/watch?v=DkjCaAMBGWM&t=119):
  - Stack DataFrames vertically or horizontally using `concat()`.
  - Example: `pd.concat([df1, df2], axis=0)` for vertical stacking or `axis=1` for horizontal stacking.

- [**Merging DataFrames**](https://www.youtube.com/watch?v=DkjCaAMBGWM&t=1264):
  - Merge DataFrames based on similar columns using `merge()`.
  - Example: `df1.merge(df2, on=['Airline', 'Date'])`.
  - Specify merge types: `'left'`, `'right'`, `'inner'`, or `'outer'`.

#### Merging DataFrames
- [**Merge Specific Columns**](https://www.youtube.com/watch?v=DkjCaAMBGWM&t=1309):
  - Use the `on` parameter to specify columns for merging: `df1.merge(df2, on='common_column')`.
  - If columns to merge on have different names, use `left_on` and `right_on`: `df1.merge(df2, left_on='col1', right_on='col2')`.

- [**Handling Suffixes in Merging**](https://www.youtube.com/watch?v=DkjCaAMBGWM&t=1320):
  - Automatically adds suffixes `_x` and `_y` to similarly named columns.
  - Customize suffixes with the `suffixes` parameter: `df1.merge(df2, on='column', suffixes=('_departure', '_arrival'))`.

#### Conclusion
- [**Wrap-Up**](https://www.youtube.com/watch?v=DkjCaAMBGWM&t=1355):
  - This tutorial aimed to provide a solid foundation for data manipulation using Pandas.
  - There are many more advanced features and functions in Pandas beyond this introduction.
  - Feedback and requests for future topics are welcome in the comments.