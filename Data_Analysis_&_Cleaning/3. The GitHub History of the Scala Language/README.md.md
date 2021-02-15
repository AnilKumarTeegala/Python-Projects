**PROJECT**

# The GitHub History of the Scala Language

Find the true Scala experts by exploring its development history in Git and GitHub.

## Project Description
Open source projects contain entire development histories, such as who made changes, the changes themselves, and code reviews. In this project, you'll be challenged to read in, clean up, and visualize the real-world project repository of Scala that spans data from a version control system (Git) as well as a project hosting site (GitHub). With almost 30,000 commits and a history spanning over ten years, Scala is a mature language. You will find out who has had the most influence on its development and who are the experts.

The dataset includes the project history of Scala retrieved from Git and GitHub as a set of CSV files.				

## Project Tasks

1. Scala's real-world project repository data
2. Preparing and cleaning the data
3. Merging the DataFrames
4. Is the project still actively maintained?
5. Is there camaraderie in the project?
6. What files were changed in the last ten pull requests?
7. Who made the most pull requests to a given file?
8. Who made the last ten pull requests on a given file?
9. The pull requests of two special developers
10. Visualizing the contributions of each developer

### Task 1 Scala's real-world project repository data

Import the dataset into the notebook. All the relevant files can be found in the `datasets` subfolder.

- Import the `pandas` module.
- Load in `'datasets/pulls_2011-2013.csv'` and `'datasets/pulls_2014-2018.csv'`as pandas DataFrames and assign them to `pulls_one` and `pulls_two` respectively.
- Similarly, load in `'datasets/pull_files.csv'` and assign it to `pull_files`.

------

### Good to know

For this Project, you need to be comfortable with pandas. The skills required to complete this Project are covered in [Data Manipulation with pandas](https://learn.datacamp.com/courses/data-manipulation-with-pandas), and [Merging DataFrames with pandas](https://www.datacamp.com/courses/merging-dataframes-with-pandas).

### Task 2 Preparing and cleaning the data

Combine the two pulls DataFrames and then convert `date` to a `DateTime` object.

- Append `pulls_one` to `pulls_two` and assign the result to `pulls`.
- Convert the `date` column for the `pulls` object from a string into a `DateTime` object.

------

For the conversion, we recommend using pandas' `to_datetime()` function. Set the `utc` parameter to `True`, as this will simplify future operations.

Coordinated Universal Time (UTC) is the basis for civil time today. This 24-hour time standard is kept using highly precise atomic clocks combined with the Earth's rotation.

### Task 3 Merging the DataFrames

Merge the two DataFrames.

- Merge `pulls` and `pull_files` on the `pid` column. Assign the result to the `data` variable.

The `pandas` DataFrame has a `merge` method that will perform the joining of two DataFrames on a common field.

### Task 4 Is the project still actively maintained?

Calculate and plot project activity in terms of pull requests.

- Group `data` by month and year (i.e. '2011-01', '2011-02', etc), and count the number pull requests (`pid`). Store the counts in a variable called `count`
  - There are a number of ways to accomplish this.
  - One way would be to create two new columns containing the year and month attributes of the `date` column, and then group by these two variables.
- Plot `counts` using a bar chart (this has been done for you).

*Note, the scaffolding exists to help you create the two columns as suggested above. However, this exercise will only check whether you create `counts` correctly. Thus, alternate solutions are more than welcome!*

### Task 5 Is there camaraderie in the project?

Plot pull requests by user.

- Group the pull requests by each user and count the number of pull requests they submitted. Store the counts in a variable called `by_user`.
- Plot the histogram for `by_user`.\

### Task 6: What files were changed in the last ten pull requests?

Identify the files changed in the last ten pull requests.

- Select the last ten pull requests and name the resulting DataFrame `last_10`.
- Merge `last_10` with the `pull_files` DataFrame on `pid`, assigning the result to `joined_pr`.
- Identify the unique files in `joined_pr` (via the `file` column) using `set()`.

Python's `DateTime` objects are comparable and sortable. A more recent date is larger than an older date. In task 2, we converted the `date` column into `DateTime` objects. Therefore, the largest ten values in the `date` column are the most recent ones.

pandas' `nlargest` method ([documentation](https://pandas.pydata.org/pandas-docs/version/0.17.0/generated/pandas.DataFrame.nlargest.html)) is helpful for the first bullet.

[Here](https://stackoverflow.com/questions/39551566/create-a-set-from-a-series-in-pandas) is an example of using `set()` on Stack Overflow.

### Task 7: Who made the most pull requests to a given file?

Identify the top 3 developers that submitted pull requests to `src/compiler/scala/reflect/reify/phases/Calculate.scala`.

- Select the pull requests that changed that file and name the resulting DataFrame `file_pr`.
- Count the number of changes made by each developer and name the resulting DataFrame `author_counts`.
- Print the top 3 developers.

pandas' `nlargest` method ([documentation](https://pandas.pydata.org/pandas-docs/version/0.17.0/generated/pandas.DataFrame.nlargest.html)) is helpful for the third bullet.

### Task 8: Who made the last ten pull requests on a given file?

Identify the most recent ten pull requests that touched `src/compiler/scala/reflect/reify/phases/Calculate.scala`.

- Select the pull requests that touched the file and name the resulting DataFrame `file_pr`.
- Merge `file_pr` with the `pulls` DataFrame on the `pid` column and name the resulting DataFrame `joined_pr`.
- Using `set()`, create a set of users for the ten most recent pull requests.

To find the ten most recent pull requests, use the `nlargest` function of a `DataFrame`. Again, pandas' `nlargest` method ([documentation](https://pandas.pydata.org/pandas-docs/version/0.17.0/generated/pandas.DataFrame.nlargest.html)) may be helpful for this third bullet.

### Task 9: The pull requests of two special developers

Plot the number of pull requests for two developers, over time.

- Using the `pulls` DataFrame, select all of the pull requests by these two developers and name the resulting DataFrame `by_author`.
- Fill in the `groupby` parameters to count the number of pull requests submitted by each author each year. That is, group by `user` and the year property of `date`.
- Plot `counts_wide` using a bar chart.

pandas' `isin` method ([documentation](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.isin.html) will be helpful for bullet one.

`DateTime` objects expose the components of a date through their `dt` accessors.

`counts` is transformed to a wide format to make plotting the bar chart of pull request count (y-axis) by year (x-axis) by user (legend) easier.

### Task 10: Visualizing the contributions of each developer

Calculate the number of pull requests submitted by a developer to a file each year.

- Select the pull requests submitted by the authors from the `data` DataFrame and name the results `by_author`.
- Select the pull requests from `by_author` that affect the file and name the results `by_file`.
- Transform `grouped` into a wide format using `pivot_table`. Name the results `by_file_wide`.

The code required to complete bullet one in this task is the same as the code for bullet one in task 9, except on the `data` DataFrame instead of the `pulls` DataFrame.

`by_file` is transformed to a wide format to make plotting the bar chart of pull request count (y-axis) by year (x-axis) by user (legend) easier. The columns for `by_file_wide` are as follows:

- Index column: `date`
- Columns to expand: `user`
- Value columns: `pid`
- Fill value: 0