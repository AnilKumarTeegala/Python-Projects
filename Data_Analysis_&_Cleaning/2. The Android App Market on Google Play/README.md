**PROJECT**

# The Android App Market on Google Play

Loading, cleaning, and visualizing the scraped Google Play Store data to gain insights into the Android app market.

## Project Description

Mobile apps are everywhere. They are easy to create and can be lucrative. Because of these two factors, more and more apps are being developed. In this project, you will do a comprehensive analysis of the Android app market by comparing over ten thousand apps in Google Play across different categories. You'll look for insights in the data to devise strategies to drive growth and retention. The [data](https://www.kaggle.com/lava18/google-play-store-apps) for this project was scraped from the [Google Play](https://play.google.com/store/apps?hl=en) website. While there are many popular datasets for Apple App Store, there aren't many for Google Play apps, which is partially due to the increased difficulty in scraping the latter as compared to the former. The data files are as follows:

- [`apps.csv`](datasets/apps.csv): contains all the details of the apps on Google Play. These are the features that describe an app.
- [`user_reviews.csv`](datasets/user_reviews.csv): contains 100 reviews for each app, [most helpful first](https://www.androidpolice.com/2019/01/21/google-play-stores-redesigned-ratings-and-reviews-section-lets-you-easily-filter-by-star-rating/). The text in each review has been pre-processed, passed through a sentiment analyzer engine and tagged with its sentiment score.

## Project Tasks

1. Google Play Store apps and reviews
2. Data cleaning
3. Exploring app categories
4. Distribution of app ratings
5. Size and price of an app
6. Relation between app category and app price
7. Filter out "junk" apps
8. Popularity of paid apps vs free apps
9. Sentiment analysis of user reviews

### Task 1: Google Play Store apps and reviews

Import the data, drop duplicate rows, and inspect the data.

- Load `datasets/apps.csv` into a DataFrame and assign it to the variable `apps_with_duplicates`.
- Drop all duplicate rows from `apps_with_duplicates` and assign the result to `apps`.
- Print the total number of apps.
- Display and inspect the `apps` dataframe for issues such as missing values. Which columns have missing (null) values?
  **Make a note of the 4 columns that have missing values: `Rating`, `Size`, `Current Ver`, `Android Ver`.
  We will deal with this later in Task #5.**
- Finally, display a random sample of 5 rows from `apps`.

## Good to know

This project lets you apply the skills from [Joining Data with pandas](https://www.datacamp.com/courses/joining-data-with-pandas). We recommend that you take this course before starting this project.

The [data](https://www.kaggle.com/lava18/google-play-store-apps) for this project was scraped from the [Google Play](https://play.google.com/store/apps?hl=en) website. While there are many popular datasets for Apple App Store, there aren't many for Google Play apps, which is partially due to the increased difficulty in scraping the latter as compared to the former.

A good practice is to always use the `info()`[documentation](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.info.html) function on your dataframe before beginning any analysis. This method prints information about the dataframe including the column data types, non-null values and memory usage.

Helpful links:

- pandas `read_csv()`[documentation](https://pandas.pydata.org/pandas-docs/version/0.17.0/generated/pandas.read_csv.html)
- pandas `drop_duplicates()`[documentation](https://pandas.pydata.org/pandas-docs/version/0.17/generated/pandas.DataFrame.drop_duplicates.html)

*Note: This project also uses the plotting libraries [Seaborn](https://seaborn.pydata.org/) and [Plotly](https://plotly.com/python/) to help visualize the results of some steps. However, the tasks have been written in such a way that you should be able to complete them without any prior experience.*

--------------------

### Task 2: Data cleaning

Clean the dataset.

- Create a list named `chars_to_remove` that contains the following characters: `+` `,` and `$`.
- Create a list named `cols_to_clean` that contains the following column names: `Installs` and `Price`.
- For each column in `cols_to_clean` in the `apps` DataFrame, replace each character in `chars_to_remove` with the empty string `''`.
  **Note: Make sure to use an empty string `''` and not a space character `' '`**
- Finally, convert `Installs` and `Price` columns to `float` data type using `astype()` function.

**Important Note: If you run this same cell twice in a row or in succession, you will get an error. To avoid this, please always use the `Check Project` button after each task to run your notebook.**

Helpful links:

- `astype()` [documentation](https://pandas.pydata.org/docs/reference/api/pandas.Series.astype.html)

--------------

### Task 3: Exploring app categories

Create data for a bar chart that shows the distribution of apps across different categories.

- Find the number of unique app categories. Save your result in `num_categories`.
- Count the number of apps in each category and sort the categories in descending order of app count. Save your answer in `num_apps_in_category`.


Helpful links:

- `unique()` [documentation](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.unique.html)
- `value_counts()` [documentation](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.value_counts.html)
- `sort_values()` [documentation](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.sort_values.html)

------------

### Task 4: Distribution of app ratings

Create a plot annotation for average app rating.

- Find the average app rating and assign it to `avg_app_rating`.


Helpful links:

- `mean()` [documentation](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.mean.html)
- Plotly histogram [documentation](https://plot.ly/python/histograms/)

---------

### Task 5: Size and price of an app

Examine the relationship between size, price, and rating of apps using `jointplot()`.

Recall from Task #1 that we had observed some missing values in the `Rating` and `Size` columns. To make rational decisions, it is important that we do not consider these missing values in our analysis. We will work with a subset `apps_with_size_and_rating_present` DataFrame for this task.

- Select rows from `apps` where both `Rating` and `Size` values are present, ie - they are not null. Store the result in the `apps_with_size_and_rating_present` dataframe.
- From `apps_with_size_and_rating_present`, select the categories having atleast `250` apps. Assign the result to `large_categories` dataframe.
- Fill out `x` and `y` to create a joint plot of `Rating` as a function of `Size`.
- From `apps_with_size_and_rating_present` dataframe, select all `Paid` apps. Save the result in `paid_apps`.
- Fill out `x` and `y` to create a joint plot of `Rating` as a function of `Price`.


Helpful links:

- There are many ways to subset a dataframe and select rows based on a column value. [This exercise](https://campus.datacamp.com/courses/data-manipulation-with-pandas/transforming-data?ex=7) from Data Manipulation with pandas may be a good starting place.
- `jointplot()` [documentation](https://seaborn.pydata.org/generated/seaborn.jointplot.html)

--------

### Task 6: Relation between app category and app price

Use a strip plot to visualize the distribution of paid apps across different categories.

- Plot a strip plot with x-axis extending along the `Price` range and y-axis depicting the `Category`.
- Find apps priced above `$200`. Print the `Category`, `App` and `Price` columns for such apps.

Here are some interesting websites that can estimate app price:

- [Estimate my app](https://estimatemyapp.com/)
- [How much to make an app](http://howmuchtomakeanapp.com/)

Helpful links:

- `stripplot()` [documentation](https://seaborn.pydata.org/generated/seaborn.stripplot.html)
- [Filter rows](https://cmdlinetips.com/2018/02/how-to-subset-pandas-dataframe-based-on-values-of-a-column/) in pandas
--------------
### Task 7: Filter out "junk" apps

Filter out "junk" apps.
**Note: For simplicity, we will continue to use the `popular_app_cats` dataframe (from previous task) and not our original dataframe `apps`**

- Select rows from `popular_app_cats` that contain apps priced below $100 and assign it to `apps_under_100`.
- Re-plot your strip plot using `apps_under_100` dataframe (instead of `popular_app_cats` used in the previous task).

--------

### Task 8: Popularity of paid apps vs free apps

Prep the data for a box plot that compares the number of installs of paid apps vs. number of installs of free apps.

- From `apps`, filter rows where for `Type` == `Paid`, and select the `Installs` column and assign it to `y` of `trace0`.
- From `apps`, filter rows where for `Type` == `Free`, and select the `Installs` column and assign it to `y` of `trace1`.


Helpful links:

- Plotly box plot [documentation](https://plot.ly/python/box-plots/)
- Interpreting box plots [article](https://www.wellbeingatschool.org.nz/information-sheet/understanding-and-interpreting-box-plots)
-------------------
### Task 9: Sentiment analysis of user reviews

Load the user review data and plot it to visualize sentiment of paid vs. free apps.

- Read `datasets/user_reviews.csv` into the `reviews_df` DataFrame.
- Merge `apps` and `reviews_df` DataFrames and assign the result to `merged_df`.
- Create a box plot with `Type` on the x-axis and `Sentiment_Polarity` on the y-axis.

Hurry Done🥳🥳🥳🥳
