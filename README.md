
# Week 1 - Preprocessing

## Please run the cells of the notebook as you get to them while reading
import pandas as pd
import numpy as np
from datetime import datetime, timedelta
# 1. Lesson on how to search for Python commands

Let's consider a few possible ways to learn about Python programming.  Let's suppose you want to learn how to produce a short summary of the information in your DataFrame.

1. Your **instructor** could provide the information.

You could be provided with a lesson about functions like info() and describe().  If you have a pandas DataFrame called df, then you can summarize its contents using df.info() or df.describe().  df.info() provides a list of column names with their counts and data types.  df.describe() will provide information such as the mean, min, max, standard deviation, and quantiles.  Thus:
import pandas as pd
import numpy as np
from datetime import datetime, timedelta

# Each inner list represents a single row of the DataFrame
df = pd.DataFrame([[1, 4], [2, 5], [3, 6], [4, 7]], columns = ['A', 'B'])
df.describe()
df.info()
df.head()
df.shape
df.columns
df.dtypes

print(df.info())
print(df.describe())
print(df.head())
print(f"Shape: {df.shape}")
In this describe() result, we see that the two columns A and B each have four elements.  The means and other statistics are shown.

2. You could look up the information on **Google**.

If I Google the question "how do I briefly summarize the contents of a dataframe using Python," I receive the following link (among others), which discusses the describe() command mentioned above:

https://www.w3schools.com/python/pandas/ref_df_describe.asp

It also provide the complete usage information:

dataframe.describe(percentiles, include, exclude, datetime_is_numeric)

It explains that "percentiles" is set by default to [0.25, 0.5, 0.75] but we could change that.  Let's try it!  Since there are three intervals here rather than four, it might be more meaningful to ask about a 33rd and 67th percentile rather than 25, 50, and 75.  We can use 1/3 for 0.33 and 2/3 for 0.67 to get the exact percentile values.
df = pd.DataFrame([[1, 4], [2, 5], [3, 6], [4, 7]], columns = ['A', 'B'])
df.describe(percentiles = [1/3, 2/3])

**<span style="color:blue">1. Studying notes</span>**

count = how many values in the columns. There are 4 values.

mean = average = sum/how many values

$ \text{Std} = \sqrt{\frac{\sum (x_i - \text{Mean})^2}{n}} $.

### Explanation of Terms
\[
\begin{aligned}
&\bullet \ x_i : \text{Each value in the dataset.} \\
&\bullet \ \text{Mean} : \text{The arithmetic mean of the dataset.} \\
&\bullet \ n : \text{The total number of data points.} \\
&\bullet \ (x_i - \text{Mean})^2 : \text{The squared deviation of each value from the mean.}
\end{aligned}
\]
Apparently, the 50% value (the median) stays even though we did not specifically request it.

3. You could look up the official **documentation**.

Now that we know we want the pandas describe() function, try Googling: pandas documentation describe.

Here is the general documentation page for pandas:

https://pandas.pydata.org/docs/index.html

Here is the specific page for the describe() function:

https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.describe.html

When I look at this, it appears to be showing the most recent (currently 2.2) version of pandas; this is shown in the upper right corner.

4. You could also ask **ChatGPT**.

Let's try it.  ChatGPT, "how do I briefly summarize the contents of a dataframe using Python"

When I do this, ChatGPT mentions describe() among other options, but does not go into detail.  However, I could ask it.  ChatGPT, "tell me more about describe() in Python for summarizing dataframes."

Then, I get a good explanation of describe(), although it does not mention the percentiles option.  One advantage of using Google or the documentation in addition of ChatGPT is that these sources may provide interesting information that does not directly answer our question.  Thus, we might not have known about the various arguments, such as percentiles, if we only used ChatGPT.  A second issue is that ChatGPT sometimes hallucinates (it makes up information).  In general, by examining multiple sources - Google, documentation, and ChatGPT - we can get more information.
**<span style="color:green"> Answer </span>**

I have added: <br>
print(df.info()) - summary, and structure; <br>
print(df.describe()) - generates descriptive statistics for numeric columns; <br>
print(df.head()) - displays the first 5 rows; <br>
print(f"Shape: {df.shape}") - provides the dimensions of the DataFrame.


# 2. Weekly graph question
In Storytelling With Data, on page 1: examine the pie chart graph in the upper left corner of the graphs.  Please write a short explanation of the pros and cons of this graph.  What do you think of the choice of pie chart as a format?  The color scheme?  The legend?  The title?  How would you draw it differently if you were creating this graph?
<img src="Survey Results.png" alt="Pie Chart" width="500">

**<span style="color:green"> Answer </span>**

**Pros**  
1. **Clear Title:** The title "Survey Results" clearly indicates the chart’s purpose.  
2. **Simple Representation:** Pie charts effectively show parts of a whole.  
3. **Percentage Labels:** Including percentages helps readers quickly understand the data distribution.

**Cons**  
1. **Choice of Pie Chart:** Pie charts are not effective for comparing close values, like 19% versus 25%.  
2. **Color Scheme:** Colors are distinct, but may pose accessibility issues for those with color vision deficiencies.  
3. **Legend Placement:** The legend's position requires viewers to constantly shift their gaze, making it harder to match slices with categories.  
4. **Title Specificity:** The title is too generic and lacks context; a more specific title would improve clarity.

**Suggested Improvements**  
1. **Use a Different Chart Type:** Consider a bar chart for better comparison of similar values.  
2. **Improve the Color Scheme:** Use a colorblind-friendly palette with thematic colors.  
3. **Add Labels Directly:** Place category names on or near the slices for easier identification.  
4. **Make the Title More Informative:** A descriptive title, like "Survey Results on Audience Engagement," would enhance understanding.

**How I Would Redraw It**  
1. **Use a Horizontal Bar Chart:** This allows for clearer comparisons.  
2. **Add Data Labels:** Show category names and percentages directly on the bars.  
3. **Choose a Colorblind-Friendly Palette:** Group sentiments like "Positive" and "Negative."  
4. **Provide a Subtitle:** Add context about the survey, such as "Survey on Audience Reactions to Event X."



# 3. Homework - Bank Customers

I will begin by creating a file for you to analyze.  I will show you all of the steps I used to create it.  Please run this code in order to create and save a file about bank customers.

### The numbered problems are for you to solve.
num_customers = 100
np.random.seed(0) # Random numbers (same every time you run the code)
df_bank = pd.DataFrame(columns = ["CustomerID"]) # creates an empty DataFrame with a single column
# This generates a range of numbers from 0 to num_customers - 1.
# If num_customers = 100, it creates an array: [0, 1, 2, ..., 99].
df_bank["CustomerID"] = [str(x) for x in np.arange(num_customers)]
# These define the start and end dates for generating random birthdates.
start = datetime(1950, 1, 1)
end = datetime(2024, 1, 1)
# This calculates the difference between the two dates in days.
numdays = (end - start).days
# Generates an array of num_customers random integers between 0 and numdays - 1.
random_days = np.random.randint(0, numdays, size = num_customers)
# Formats the birthdates into the YYYY-MM-DD format (e.g., "1985-03-14").
df_bank["BirthDate"] = start + pd.to_timedelta(random_days, unit='D')
df_bank["BirthDate"] = df_bank["BirthDate"].dt.strftime('%Y-%m-%d')
def make_ssn_string(num):
    # Convert to a 9-digit string.
    ssn_str = f'{num:09}'
    # ssn_str[0:3]: Extracts the first 3 characters (area number).
    # ssn_str[3:5]: Extracts the next 2 characters (group number).
    # ssn_str[5:9]: Extracts the last 4 characters (serial number).
    return ssn_str[0:3] + "-" + ssn_str[3:5] + "-" + ssn_str[5:9]
ssn_vector_func = np.vectorize(make_ssn_string)
# Generating Random SSNs
df_bank["SSN"] = ssn_vector_func(np.random.randint(0, 999999999, size = num_customers))
# This line adds a new column named "AccountID" to the df_bank DataFrame. 
# The values in this column are randomly generated integers within a specified range
df_bank["AccountID"] = np.random.randint(0, num_customers, size = num_customers)
# This generates an array of random integers between 0 and 365 * 80 (the total number of days in 80 years).
random_days = np.random.randint(0, 365 * 80, size = num_customers)
df_bank["AccountOpened"] = (pd.to_datetime(df_bank["BirthDate"]) + pd.to_timedelta(random_days, unit='D')).dt.strftime('%Y-%m-%d')
# Accesses the value in the row with index 0 and the column "BirthDate" and changes it to "1980".
df_bank.loc[0, "BirthDate"] = "1980"
# Accesses the value in the row with index 1 and the column "BirthDate" and changes it to "no date".
df_bank.loc[1, "BirthDate"] = "no date"
# Accesses the value in the row with index 2 and the column "AccountID" and changes it to NaN.
df_bank.loc[2, "AccountID"] = np.nan
# This line adds a new column named "AccountType" to the df_bank DataFrame. 
# The values in this column are randomly assigned from the list 
# ["checking", "savings", "cd"] for each custome
df_bank["AccountType"] = np.random.choice(["checking", "savings", "cd"], size = num_customers)
Load the bank_customers.csv file.  (There is no practical reason to save it, then load it - we're just demonstrating how this would be done.)
I am calling the loaded df by a new name, df_bank_loaded, to make clear why it's not the same variable as the old df.  Of course, in actuality the two contain the exact same data!  But it's good to get in the habit of naming things carefully.
# Copying a Row from One DataFrame to Another
df_bank.loc[num_customers - 1] = df.loc[0]
# Saving the Updated DataFrame to a CSV File
df_bank.to_csv("bank_customers.csv", index=False)
# Reads a CSV file and stores it in a DataFrame
df_bank_loaded = pd.read_csv("bank_customers.csv")
# Displays the first 5 rows of the DataFrame
print(df_bank_loaded.head())
# Displays the last 5 rows of the DataFrame
print(df_bank_loaded.tail())
# Describes the DataFrame
print(df_bank_loaded.describe())
# Information about the DataFrame
print(df_bank_loaded.info())
1. Use describe() and info() to analyze the data.   Also, look at the first few rows.
Suggested Google Search or ChatGPT prompt: "how do I use the describe function in python"

Example Google result: https://www.w3schools.com/python/pandas/ref_df_describe.asp
# The first few rows
df_bank_loaded.iloc[0:5]
# Describe the DataFrame
df_bank_loaded.describe()
# Information about the DataFrame
df_bank_loaded.info()
If you used describe() and info(), you now know that BirthDate and AccountOpened are strings.  But we want them to be dates.  Let's convert them to dates (or Timestamps in pandas).  When we try this, we get a ValueError.
try:
    # This line converts the "BirthDate" column to a datetime object.
    df_bank_loaded["BirthDate"] = pd.to_datetime(df_bank_loaded["BirthDate"], format='%Y-%m-%d')
    print("It worked!")
    # Handle any errors
except ValueError as e:
    print(f"ValueError for BirthDate: {e}")
try:
    # Converts the "AccountOpened" column into pandas datetime objects
    df_bank_loaded["AccountOpened"] = pd.to_datetime(df_bank_loaded["AccountOpened"], format='%Y-%m-%d')
    print("It worked!")
    # Handle any errors
except ValueError as e:
    print(f"ValueError for AccountOpened: {e}")
The simple way to fix this is to remove the rows that have bad dates for BirthDate.  I Googled:

"How to remove rows from a dataframe that have poorly formatted dates using python"

https://stackoverflow.com/questions/21556744/pandas-remove-rows-whose-date-does-not-follow-specified-format

This recommends that I verify that the date is a string of length 10, because YYYY-MM-DD has that length:

df1\[df1.BirthDate.str.len() !=10]
# This code evaluates how many rows in the df_bank_loaded DataFrame 
# have a "BirthDate" value with exactly 10 characters
len(df_bank_loaded[df_bank_loaded.BirthDate.str.len() == 10])
# This code filters the df_bank_loaded DataFrame to find rows where the length of the 
# "BirthDate" string is not equal to 10, and then retrieves the first 5 such rows
df_bank_loaded[df_bank_loaded.BirthDate.str.len() != 10].iloc[0:5]
Now we can make this permanent, creating a new DataFrame df_bank_datefix.
I am making a copy in order to ensure that df_bank_datefix is a new DataFrame rather than being a slice of the old one.
# This code filters the df_bank_loaded DataFrame to include only 
# rows where the "BirthDate" column contains strings with a length of 
# exactly 10 characters (e.g., dates in the format YYYY-MM-DD). 
# The filtered result is copied into a new DataFrame called df_bank_datefix
df_bank_datefix = df_bank_loaded[df_bank_loaded.BirthDate.str.len() == 10].copy()
Test again:
# This code tries to convert the "BirthDate" column in the df_bank_datefix DataFrame 
# into datetime objects using the specified format '%Y-%m-%d'.
try:
    df_bank_datefix["BirthDate"] = pd.to_datetime(df_bank_datefix["BirthDate"], format='%Y-%m-%d')
    print("It worked!")
except ValueError as e:
    print(f"ValueError: {e}")
2. To check that it worked, use a summary function that will tell you if the BirthDate field is now a datetime type
df_bank_datefix.info()
3. Check whether there are any null values in the DataFrame.  If so, remove those rows or (if you prefer) fill in the value with an appropriate number.

First try at a Google search or ChatGPT prompt: "how do I find out if there are any null values in a pandas DataFrame?"

This page gives an answer.  Unfortunately, it took my request too literally: it tells me only if there are any, and not which rows have them.  On reflection, that's not really what I want - I think I asked the wrong question.  I want to see the rows, not just _whether_ there are any.

https://stackoverflow.com/questions/29530232/how-to-check-if-any-value-is-nan-in-a-pandas-dataframe

ChatGPT likewise doesn't give the answer I want - because I asked the wrong question.

Next try at a Google search or ChatGPT prompt: "how do I check which rows have null values in a pandas DataFrame?"

This page gives an answer:

https://stackoverflow.com/questions/36226083/how-to-find-which-columns-contain-any-nan-value-in-pandas-dataframe

ChatGPT also gives a good answer.  I recommend looking at both of them!

Now try it on your own:

Suggested Google search or ChatGPT prompt: "how do I remove rows with null values in a pandas DataFrame?"

Suggested Google search or ChatGPT prompt: "how do I fill in null values in a pandas DataFrame?"
print(df_bank_datefix.isna().any())
4. Find out if there are any duplicate rows (two rows exactly the same).  List their row numbers.  Then remove the duplicates
Suggested Google search or ChatGPT prompt: "how can I find out if there are any duplicate rows in a DataFrame using Python"

Again, Google provides me with a page that addresses the question:

https://saturncloud.io/blog/how-to-find-all-duplicate-rows-in-a-pandas-dataframe/

To remove the duplicates, do this search: "how can I remove the duplicate rows in a DataFrame using Python"

This leads me to the following documentation.

https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.drop_duplicates.html
df_bank_datefix.drop_duplicates()
5. Check whether the customers all have unique AccountIDs.  If not, provide the first example of a non-unique AccountId.
Suggested Google search or ChatGPT prompt: "how can I find the first non-unique item from a pandas Series in python"

By the way: why didn't I ask the question "how can I check whether the customers all have unique AccountIDs"?

The problem would be that Google and ChatGPT don't know what "customers" you are talking about.  It's important to understand that the AccountIDs are a column of a DataFrame, and as such they are a Series.  Therefore, we should use the correct vocabulary and ask about a Series.  If you mess up and ask about a "list" instead of a Series, you _might_ get an answer that still works.  But it's better to get the vocabularly right.

It's important to add "in python" because this task could be performed in many languages.

ChatGPT gave me this suggestion: data[data.isin(data[data.duplicated()])].iloc[0]
However, ChatGPT did not explain how this code worked and even claimed (falsely) that it was going to use the value_counts() function in the solution.  So although the code is correct, I personally found ChatGPT's answer very confusing.  You could, perhaps, ask ChatGPT to explain further how this code works.

ChatGPT, "How does this code work: data[data.isin(data[data.duplicated()])].iloc[0]"

On the other hand, Google leads me to the documentation for the duplicated() function:

https://pandas.pydata.org/docs/reference/api/pandas.Series.duplicated.html

Here, I can see that when I really need is data.duplicated(keep = False), where "data" should be the Series in question.  However, this just gives me a Series of boolean values indicating which ones are duplicates.  I have to somehow know that extracting the numerical values instead of a Series of booleans involves boolean indexing: data\[data.duplicated(keep = False)].

So as usual, I'd suggest that a combination of Google, documentation, and ChatGPT will give you the best information.
# Identify all duplicate AccountIDs
duplicate_rows = df_bank_datefix[df_bank_datefix["AccountID"].duplicated(keep=False)]
print("Duplicate AccountIDs:")
print(duplicate_rows)
6. Count how many distinct AccountIDs there are.
Suggested Google search or ChatGPT prompt: "how can I find out how many distinct items there are in a pandas Series using python"

This time Google provides me with a page that's specifically made to answer this question:

https://www.geeksforgeeks.org/how-to-count-distinct-values-of-a-pandas-dataframe-column/
distinct_account_ids_with_nan = df_bank_datefix["AccountID"].nunique(dropna=False)
print(f"Number of distinct AccountIDs (including NaN): {distinct_account_ids_with_nan}")
7. Remove the duplicate AccountIDs so that each AccountID appears only once.

This will involve using data.duplicated() but this time without keep = False.  We don't want to drop all duplicates; we want to leave one example of each value.
df_bank_datefix = df_bank_datefix[~df_bank_datefix["AccountID"].duplicated(keep="first")]
df_bank_datefix.reset_index(drop=True, inplace=True)
8. What are the mean, median, and mode customer age in years?  (Rounding down to the next lower age.)
Are there any outliers?  (Customers with very large or very small ages, compared with the other ages?)
Suggested Google search or ChatGPT prompt: "how can I find out the mean, median, and mode of a pandas Series"
print("Mean for all numeric columns:")
print(df_bank_datefix.select_dtypes(include=[np.number]).mean())
9. One-hot encode the AccountType column.  This means creating a new "checking," "savings", and "cd" columns so that you can run machine learning algorithms.
**<span style="color:red"> Corrected </span>**

I had to change <mark><span style="color: blue;">df1</span></mark> to the existed data frame <mark><span style="color: blue;">df_bank_datefix</span></mark>, because df1 was not defined
one_hot = pd.get_dummies(df_bank_datefix["AccountType"])
df_bank_datefix = df_bank_datefix.join(one_hot)
df_bank_datefix.iloc[0:5]
Now, change the cd, checking, and savings columns into integers.
# Convert cd, checking, and savings columns to integers
df_bank_datefix[["cd", "checking", "savings"]] = df_bank_datefix[["cd", "checking", "savings"]].astype(int)

# Display the first 5 rows to confirm the changes
print(df_bank_datefix.iloc[0:5])
10. Are there any other data values that do not seem right?  If not, give an example?
I don't think Google or ChatGPT alone will help you here.  To answer the question, look at the columns and think about what relationships they should have with each other.  For example, it seems reasonable to expect that BirthDate would be no earlier than 120 years ago (it's unlikely that a customer would be this old.)  Now we can ask Google:

"How can I find out how long ago a pandas date is"

Google provides this helpful link, although it is not exactly the solution - you'll have to work with it a bit:

https://stackoverflow.com/questions/26072087/pandas-number-of-days-elapsed-since-a-certain-date

If you check, I think you'll find that all dates are more recent than 120 years ago.  What about the AccountOpened columns?  I see some obviously wrong dates there just by looking at the first few rows.

Along those same lines, are there any birth dates that are too recent?  Do we think that any two year olds will have opened bank accounts?  How common do you think this is in real life?  How common is it in our data set?  Can you detect the two year olds opening bank accounts using just one column, or do you need two columns?
import pandas as pd

# Create a datetime index from 2014-01-01 to 2014-01-06, every 30 minutes
x = pd.date_range(start='2014-01-01', end='2014-01-06', freq='30T')

# Create a DataFrame with the index
df = pd.DataFrame(index=x, columns=['time since'])

# Set a base date
basedate = pd.Timestamp('2011-11-25')

# Calculate "time since" directly on the index
df['time since'] = (df.index - basedate).days

# Display the first few rows
print(df.head())
11. Use Matplotlib and/or Seaborn to analyse the ages at which customers open their account.  Is there a connection between the year they are born vs. the age at which they open the account?  Graph this in whatever way you think is best.
I asked Google and ChatGPT: "How can I plot dates vs. dates in Matplotlib".  This gave me a hard time at first - I had to tell ChatGPT it was giving me the wrong information because it tried to plot dates vs. numbers.  Eventually, I found out that you plot dates vs. dates in the same way you'd plot numbers vs. numbers.

Think in terms of Storytelling With Data to plot these as best you can.  Once you've seen the result, try to think of the best way to plot the data so as to show the user what you want them to see.  Title the graph so as to display the lesson that you want the user to take away.
Here are some options for the axes:

1. A scatter or line plot: On the x-axis, the date they are born.  On the y-axis, the date they open the account.
2. A scatter or line plot: On the x-axis, the date they are born.  On the y-axis, the age in years at which they open the account.
3. A scatter or line plot: On the x-axis, they year (integer) they are born.  On the y-axis, the age in years at which they open the account.
4. A histogram: on the x-axis, the age at which they open the account.

Here is an example:
import matplotlib.pyplot as plt

ax = plt.gca() # get an "Axes" object to draw on; gca stands for "get current Axes"
ax.scatter(df_bank_datefix["BirthDate"], df_bank_datefix["AccountOpened"]) # create a scatter plot based on these two dates
ax.set_ylabel("Account Opened") # label the y axis
ax.set_xlabel("Birth Date") # label the x axis
# 4. Storytelling With Data graph
Choose any graph in the Introduction of Storytelling With Data.  Using matplotlib to reproduce it in a rough way.  I don't expect you to spend an enormous amount of time on this; I understand that you likely will not have time to re-create every feature of the graph.  However, if you're excited about learning to use matplotlib, this is a good way to do that.  You don't have to duplicate the exact values on the graph; just the same rough shape will be enough.  If you don't feel comfortable using matplotlib yet, do the best you can and write down what you tried or what Google searches you did to find the answers.
<img src="Non Profit Support.png" alt="Pie Chart" width="500">

The graph appears to show trends in support for different types of non-profit organizations over time, from 2010 to 2015. 
Axes and Labels: 

1. **X-Axis (Years):**  
   - Represents the years from 2010 to 2015.  
   - Shows the progression of support over time.  

2. **Y-Axis (% Support):**  
   - Indicates the percentage of support for each category, ranging from 0% to 100%.  
   - The percentages are relative to total support.  

3. **Title:**  
   - "Non Profit Support" provides context for the data being visualized.
	
import matplotlib.pyplot as plt

# Data for the graph (years and % support for each category)
years = [2010, 2011, 2012, 2013, 2014, 2015]
arts_culture = [20, 25, 30, 35, 40, 45]
education = [70, 80, 75, 70, 65, 60]
health = [50, 60, 65, 70, 75, 80]
human_services = [60, 85, 70, 60, 55, 50]
other = [40, 45, 50, 35, 30, 40]

# Create the plot
plt.figure(figsize=(10, 6))

# Plot each category
plt.plot(years, arts_culture, label="Arts & Culture", color="blue", linewidth=2)
plt.plot(years, education, label="Education", color="red", linewidth=2)
plt.plot(years, health, label="Health", color="green", linewidth=2)
plt.plot(years, human_services, label="Human Services", color="purple", linewidth=2)
plt.plot(years, other, label="Other", color="gray", linewidth=2)

# Add labels, title, and legend
plt.xlabel("Years", fontsize=12)
plt.ylabel("% Support", fontsize=12)
plt.title("Non Profit Support", fontsize=14)
plt.legend(loc="best", fontsize=10)

# Add grid for better readability
plt.grid(True, linestyle="--", alpha=0.7)

# Show the plot
plt.tight_layout()
plt.show()