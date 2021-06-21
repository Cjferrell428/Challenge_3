# Challenge_3
Crypto Arbitrage Assignment

Import the required libraries and dependencies.
import pandas as pd
from pathlib import Path
%matplotlib inline
Collect the Data
To collect the data that you’ll need, complete the following steps:

Instructions.

Using the Pandas read_csv function and the Path module, import the data from bitstamp.csv file, and create a DataFrame called bitstamp. Set the DatetimeIndex as the Timestamp column, and be sure to parse and format the dates.

Use the head (and/or the tail) function to confirm that Pandas properly imported the data.

Repeat Steps 1 and 2 for coinbase.csv file.

Step 1: Using the Pandas read_csv function and the Path module, import the data from bitstamp.csv file, and create a DataFrame called bitstamp. Set the DatetimeIndex as the Timestamp column, and be sure to parse and format the dates.
csvpath = Path("../Python_Project/bitstamp") 
bitstamp_df = pd.read_csv(
    Path("../Python_Project/bitstamp.csv"),
    index_col="Timestamp", 
    parse_dates=True, 
    infer_datetime_format=True)
# Read in the CSV file called "bitstamp.csv" using the Path module. 
# The CSV file is located in the Resources folder.
# Set the index to the column "Date"
# Set the parse_dates and infer_datetime_format parameters
csvpath = Path("../Python_Project/bitstamp") 
bitstamp_df = pd.read_csv(
    Path("../Python_Project/bitstamp.csv"),
    index_col="Timestamp", 
    parse_dates=True, 
    infer_datetime_format=True)
Step 2: Use the head (and/or the tail) function to confirm that Pandas properly imported the data.
# Use the head (and/or tail) function to confirm that the data was imported properly.
bitstamp_df.head()
Open	High	Low	Close	BTC Volume	USD Volume	Weighted Price
Timestamp							
2018-01-01 00:00:00	13681.04	13681.04	13637.93	$13646.48	3.334553	45482.128785	13639.647479
2018-01-01 00:01:00	13646.48	13658.75	13610.18	$13658.75	2.663188	36361.390888	13653.332816
2018-01-01 00:02:00	13616.93	13616.93	13610.06	$13610.22	0.084653	1152.144036	13610.136247
2018-01-01 00:03:00	13610.27	13639.09	13610.27	$13639.09	7.182986	97856.416478	13623.361128
2018-01-01 00:04:00	13635.35	13636.35	13620.00	$13620.0	1.069665	14582.660932	13632.923329
Step 3: Repeat Steps 1 and 2 for coinbase.csv file.
# Read in the CSV file called "coinbase.csv" using the Path module. 
# The CSV file is located in the Resources folder.
# Set the index to the column "Timestamp"
# Set the parse_dates and infer_datetime_format parameters
coinbase_df = pd.read_csv(
    Path("../Python_Project/coinbase.csv"),
    index_col="Timestamp", 
    parse_dates=True, 
    infer_datetime_format=True)
# Use the head (and/or tail) function to confirm that the data was imported properly.
coinbase_df.head()
Open	High	Low	Close	BTC Volume	USD Volume	Weighted Price
Timestamp							
2018-01-01 00:00:00	13620.00	13620.00	13608.49	$13608.49	20.812754	283451.08537	13619.105106
2018-01-01 00:01:00	13607.14	13607.14	13601.66	$13601.66	13.474359	183283.97801	13602.426919
2018-01-01 00:02:00	13601.44	13601.44	13580.00	$13580.0	11.536360	156789.19686	13590.872506
2018-01-01 00:03:00	13587.31	13587.31	13542.70	$13550.34	16.328039	221413.64182	13560.332806
2018-01-01 00:04:00	13550.34	13585.95	13550.34	$13583.44	9.955364	135141.26944	13574.719401
Prepare the Data
To prepare and clean your data for analysis, complete the following steps:

For the bitstamp DataFrame, replace or drop all NaN, or missing, values in the DataFrame.

Use the str.replace function to remove the dollar signs ($) from the values in the Close column.

Convert the data type of the Close column to a float.

Review the data for duplicated values, and drop them if necessary.

Repeat Steps 1–4 for the coinbase DataFrame.

Step 1: For the bitstamp DataFrame, replace or drop all NaN, or missing, values in the DataFrame.
bitstamp_df.dropna()
# For the bitstamp DataFrame, replace or drop all NaNs or missing values in the DataFrame
bitstamp_df.dropna() #dropna() will drop all Nan values in the data frame and looks like this took effect
Open	High	Low	Close	BTC Volume	USD Volume	Weighted Price
Timestamp							
2018-01-01 00:00:00	13681.04	13681.04	13637.93	$13646.48	3.334553	45482.128785	13639.647479
2018-01-01 00:01:00	13646.48	13658.75	13610.18	$13658.75	2.663188	36361.390888	13653.332816
2018-01-01 00:02:00	13616.93	13616.93	13610.06	$13610.22	0.084653	1152.144036	13610.136247
2018-01-01 00:03:00	13610.27	13639.09	13610.27	$13639.09	7.182986	97856.416478	13623.361128
2018-01-01 00:04:00	13635.35	13636.35	13620.00	$13620.0	1.069665	14582.660932	13632.923329
...	...	...	...	...	...	...	...
2018-03-31 23:55:00	6935.01	6939.07	6922.56	$6922.56	1.044354	7240.034602	6932.550078
2018-03-31 23:56:00	6922.02	6922.02	6918.00	$6920.32	3.069539	21245.076275	6921.260233
2018-03-31 23:57:00	6920.33	6936.42	6920.33	$6934.72	28.239049	195789.408220	6933.286106
2018-03-31 23:58:00	6927.65	6929.42	6927.65	$6927.65	0.839507	5817.007705	6929.080007
2018-03-31 23:59:00	6929.98	6929.98	6928.00	$6928.01	0.209363	1450.735763	6929.289993
129067 rows × 7 columns

Step 2: Use the str.replace function to remove the dollar signs ($) from the values in the Close column.
# Use the str.replace function to remove the dollar sign, $
bitstamp_df.loc[:, 'Close'] = bitstamp_df.loc[:, 'Close'].str.replace("$", "")
bitstamp_df.head() #Checking to ensure that the changes took effect
​
​
Open	High	Low	Close	BTC Volume	USD Volume	Weighted Price
Timestamp							
2018-01-01 00:00:00	13681.04	13681.04	13637.93	13646.48	3.334553	45482.128785	13639.647479
2018-01-01 00:01:00	13646.48	13658.75	13610.18	13658.75	2.663188	36361.390888	13653.332816
2018-01-01 00:02:00	13616.93	13616.93	13610.06	13610.22	0.084653	1152.144036	13610.136247
2018-01-01 00:03:00	13610.27	13639.09	13610.27	13639.09	7.182986	97856.416478	13623.361128
2018-01-01 00:04:00	13635.35	13636.35	13620.00	13620.0	1.069665	14582.660932	13632.923329
Step 3: Convert the data type of the Close column to a float.
# Convert the Close data type to a float
bitstamp_df.loc[:, "Close"] = bitstamp_df.loc[:, "Close"].astype("float")
bitstamp_df.dtypes #dtypes function shows that it made "Close" a float data type in which we can now use this for calculations in our analysis
Open              float64
High              float64
Low               float64
Close             float64
BTC Volume        float64
USD Volume        float64
Weighted Price    float64
dtype: object
Step 4: Review the data for duplicated values, and drop them if necessary.
# Review the data for duplicate values, and drop them if necessary
bitstamp_df = bitstamp_df.drop_duplicates() # drop_duplicates function drops all duplicated items from the data frame
bitstamp_df #Checking to make sure duplicated items were dropped
Open	High	Low	Close	BTC Volume	USD Volume	Weighted Price
Timestamp							
2018-01-01 00:00:00	13681.04	13681.04	13637.93	13646.48	3.334553	45482.128785	13639.647479
2018-01-01 00:01:00	13646.48	13658.75	13610.18	13658.75	2.663188	36361.390888	13653.332816
2018-01-01 00:02:00	13616.93	13616.93	13610.06	13610.22	0.084653	1152.144036	13610.136247
2018-01-01 00:03:00	13610.27	13639.09	13610.27	13639.09	7.182986	97856.416478	13623.361128
2018-01-01 00:04:00	13635.35	13636.35	13620.00	13620.00	1.069665	14582.660932	13632.923329
...	...	...	...	...	...	...	...
2018-03-31 23:55:00	6935.01	6939.07	6922.56	6922.56	1.044354	7240.034602	6932.550078
2018-03-31 23:56:00	6922.02	6922.02	6918.00	6920.32	3.069539	21245.076275	6921.260233
2018-03-31 23:57:00	6920.33	6936.42	6920.33	6934.72	28.239049	195789.408220	6933.286106
2018-03-31 23:58:00	6927.65	6929.42	6927.65	6927.65	0.839507	5817.007705	6929.080007
2018-03-31 23:59:00	6929.98	6929.98	6928.00	6928.01	0.209363	1450.735763	6929.289993
129068 rows × 7 columns

Step 5: Repeat Steps 1–4 for the coinbase DataFrame.
 #checking work to ensure changes took effect
# Repeat Steps 1–4 for the coinbase DataFrame
coinbase_df.dropna()
coinbase_df.loc[:, "Close"] = coinbase_df.loc[:, "Close"].str.replace("$", "")
coinbase_df.loc[:, "Close"] = coinbase_df.loc[:, "Close"].astype("float")
coinbase_df = coinbase_df.drop_duplicates()
coinbase_df.head() #checking work to ensure changes took effect
​
Open	High	Low	Close	BTC Volume	USD Volume	Weighted Price
Timestamp							
2018-01-01 00:00:00	13620.00	13620.00	13608.49	13608.49	20.812754	283451.08537	13619.105106
2018-01-01 00:01:00	13607.14	13607.14	13601.66	13601.66	13.474359	183283.97801	13602.426919
2018-01-01 00:02:00	13601.44	13601.44	13580.00	13580.00	11.536360	156789.19686	13590.872506
2018-01-01 00:03:00	13587.31	13587.31	13542.70	13550.34	16.328039	221413.64182	13560.332806
2018-01-01 00:04:00	13550.34	13585.95	13550.34	13583.44	9.955364	135141.26944	13574.719401
Analyze the Data
Your analysis consists of the following tasks:

Choose the columns of data on which to focus your analysis.

Get the summary statistics and plot the data.

Focus your analysis on specific dates.

Calculate the arbitrage profits.

Step 1: Choose columns of data on which to focus your analysis.
Select the data you want to analyze. Use loc or iloc to select the following columns of data for both the bitstamp and coinbase DataFrames:

Timestamp (index)

Close

# Use loc or iloc to select `Timestamp (the index)` and `Close` from bitstamp DataFrame
bitstamp_sliced = bitstamp_df.iloc[:, 3]
​
# Review the first five rows of the DataFrame
bitstamp_sliced.head()
Timestamp
2018-01-01 00:00:00    13646.48
2018-01-01 00:01:00    13658.75
2018-01-01 00:02:00    13610.22
2018-01-01 00:03:00    13639.09
2018-01-01 00:04:00    13620.00
Name: Close, dtype: float64
# Use loc or iloc to select `Timestamp (the index)` and `Close` from coinbase DataFrame
coinbase_sliced = coinbase_df.iloc[:, 3]
​
# Review the first five rows of the DataFrame
coinbase_sliced.head()
Timestamp
2018-01-01 00:00:00    13608.49
2018-01-01 00:01:00    13601.66
2018-01-01 00:02:00    13580.00
2018-01-01 00:03:00    13550.34
2018-01-01 00:04:00    13583.44
Name: Close, dtype: float64
Step 2: Get summary statistics and plot the data.
Sort through the time series data associated with the bitstamp and coinbase DataFrames to identify potential arbitrage opportunities. To do so, complete the following steps:

Generate the summary statistics for each DataFrame by using the describe function.

For each DataFrame, create a line plot for the full period of time in the dataset. Be sure to tailor the figure size, title, and color to each visualization.

In one plot, overlay the visualizations that you created in Step 2 for bitstamp and coinbase. Be sure to adjust the legend and title for this new visualization.

Using the loc and plot functions, plot the price action of the assets on each exchange for different dates and times. Your goal is to evaluate how the spread between the two exchanges changed across the time period that the datasets define. Did the degree of spread change as time progressed?

# Generate the summary statistics for the bitstamp DataFrame
bitstamp_sliced.describe()
count    129067.000000
mean      10459.842453
std        2315.976088
min        5944.000000
25%        8613.370000
50%       10145.950000
75%       11444.810000
max       17234.980000
Name: Close, dtype: float64
# Generate the summary statistics for the coinbase DataFrame
coinbase_sliced.describe()
count    129322.000000
mean      10449.140958
std        2317.197419
min        5882.310000
25%        8609.230000
50%       10137.440000
75%       11397.237500
max       17177.990000
Name: Close, dtype: float64
# Create a line plot for the bitstamp DataFrame for the full length of time in the dataset 
# Be sure that the figure size, title, and color are tailored to each visualization
bitstamp_sliced.plot(figsize=(10, 5), title="Bitstamp", color="blue")
<AxesSubplot:title={'center':'Bitstamp'}, xlabel='Timestamp'>

# Create a line plot for the coinbase DataFrame for the full length of time in the dataset 
# Be sure that the figure size, title, and color are tailored to each visualization
coinbase_sliced.plot(figsize=(10, 5), title="Coinbase", color="orange")
<AxesSubplot:title={'center':'Coinbase'}, xlabel='Timestamp'>

# Overlay the visualizations for the bitstamp and coinbase DataFrames in one plot
# The plot should visualize the prices over the full lenth of the dataset
# Be sure to include the parameters: legend, figure size, title, and color and label
bitstamp_sliced.plot(legend=True, figsize=(15, 7), title="BIT VS. COIN", color="blue", label="BITSTAMP")
coinbase_sliced.plot(legend=True, figsize=(15, 7), color="orange", label="COINBASE")
<AxesSubplot:title={'center':'BIT VS. COIN'}, xlabel='Timestamp'>

# Using the loc and plot functions, create an overlay plot that visualizes 
# the price action of both DataFrames for a one month period early in the dataset
# Be sure to include the parameters: legend, figure size, title, and color and label
bitstamp_sliced.loc['2018-01-01' : '2018-01-31'].plot(
    legend=True, figsize=(15, 10), title="January 2018", color="blue", label="BITSTAMP")
coinbase_sliced.loc['2018-01-01' : '2018-01-31'].plot(
    legend=True, figsize=(15, 10), color="orange", label="COINBASE")
<AxesSubplot:title={'center':'January 2018'}, xlabel='Timestamp'>

# Using the loc and plot functions, create an overlay plot that visualizes 
# the price action of both DataFrames for a one month period later in the dataset
# Be sure to include the parameters: legend, figure size, title, and color and label 
bitstamp_sliced.loc['2018-03-01' : '2018-03-31'].plot(
    legend=True, figsize=(15, 10), title="March 2018", color="blue", label="BITSTAMP")
coinbase_sliced.loc['2018-03-01' : '2018-03-31'].plot(
    legend=True, figsize=(15, 10), color="orange", label="COINBASE")
<AxesSubplot:title={'center':'March 2018'}, xlabel='Timestamp'>

sistant. 
**Question** Based on the visualizations of the different time periods, has the degree of spread change as time progressed?
​
**Answer** As time has progressed the data shows that the same trend that occured early on in the year matched what happened in later months (March). The degree of spread change was practically the same early on as it was in later months (March). The one difference is in January at the end of the month the degree of spread was greater for bitstamp then it was for coinbase. All other data remained consistant. 
Step 3: Focus Your Analysis on Specific Dates
Focus your analysis on specific dates by completing the following steps:

Select three dates to evaluate for arbitrage profitability. Choose one date that’s early in the dataset, one from the middle of the dataset, and one from the later part of the time period.

For each of the three dates, generate the summary statistics and then create a box plot. This big-picture view is meant to help you gain a better understanding of the data before you perform your arbitrage calculations. As you compare the data, what conclusions can you draw?

# Create an overlay plot that visualizes the two dataframes over a period of one day early in the dataset. 
# Be sure that the plots include the parameters `legend`, `figsize`, `title`, `color` and `label` 
bitstamp_sliced.loc['2018-01-15'].plot(
    legend=True, figsize=(15, 10), title="January 15, 2018", color="blue", label="BITSTAMP")
coinbase_sliced.loc['2018-01-15'].plot(
    legend=True, figsize=(15, 10), color="orange", label="COINBASE")
<AxesSubplot:title={'center':'January 15, 2018'}, xlabel='Timestamp'>

# Using the early date that you have selected, calculate the arbitrage spread 
# by subtracting the bitstamp lower closing prices from the coinbase higher closing prices
arbitrage_spread_early = bitstamp_sliced.loc['2018-01-15'] - coinbase_sliced.loc['2018-01-15']
# Month one's day used had an ultimate decrease in prices by the end of the day but had the most amount of spread between the other two months days used
# Generate summary statistics for the early DataFrame
arbitrage_spread_early.describe()
count    1440.000000
mean       28.953458
std        35.145705
min      -106.080000
25%        10.000000
50%        34.035000
75%        52.217500
max       170.980000
Name: Close, dtype: float64
arbitrage_spread_early.plot(kind="box")
# Visualize the arbitrage spread from early in the dataset in a box plot
arbitrage_spread_early.plot(kind="box")
<AxesSubplot:>

# Create an overlay plot that visualizes the two dataframes over a period of one day from the middle of the dataset. 
# Be sure that the plots include the parameters `legend`, `figsize`, `title`, `color` and `label` 
bitstamp_sliced.loc['2018-02-15'].plot(
    legend=True, figsize=(15, 10), title="February 15, 2018", color="blue", label="BITSTAMP")
coinbase_sliced.loc['2018-02-15'].plot(
    legend=True, figsize=(15, 10), color="orange", label="COINBASE")
<AxesSubplot:title={'center':'February 15, 2018'}, xlabel='Timestamp'>

# Using the date in the middle that you have selected, calculate the arbitrage spread 
# by subtracting the bitstamp lower closing prices from the coinbase higher closing prices
arbitrage_spread_middle = bitstamp_sliced.loc['2018-02-15'] - coinbase_sliced.loc['2018-02-15']
# Month two's day used had an increase in prices by the end of the day but the least amount of spread between the other two months days used.
# Generate summary statistics 
arbitrage_spread_middle.describe()
count    1440.000000
mean        5.760007
std        14.908671
min       -48.800000
25%        -3.995000
50%         6.960000
75%        16.217500
max        55.470000
Name: Close, dtype: float64
.plot(kind="box")
# Visualize the arbitrage spread from the middle of the dataset in a box plot
arbitrage_spread_middle.plot(kind="box")
<AxesSubplot:>

# Create an overlay plot that visualizes the two dataframes over a period of one day from late in the dataset. 
# Be sure that the plots include the parameters `legend`, `figsize`, `title`, `color` and `label` 
bitstamp_sliced.loc['2018-03-15'].plot(
    legend=True, figsize=(15, 10), title="March 15, 2018", color="blue", label="BITSTAMP")
coinbase_sliced.loc['2018-03-15'].plot(
    legend=True, figsize=(15, 10), color="orange", label="COINBASE")
<AxesSubplot:title={'center':'March 15, 2018'}, xlabel='Timestamp'>

# Using the date from the late that you have selected, calculate the arbitrage spread 
# by subtracting the bitstamp lower closing prices from the coinbase higher closing prices
arbitrage_spread_late = bitstamp_sliced.loc['2018-03-15'] - coinbase_sliced.loc['2018-03-15']
# Month three's day used had an increase in prices by the end of the day but the second to least amount of spread between the other two months days used.
# Generate summary statistics for the late DataFrame
arbitrage_spread_late.describe()
count    1437.00000
mean        8.76572
std        10.74975
min       -24.71000
25%         1.74000
50%         8.74000
75%        15.74000
max        48.98000
Name: Close, dtype: float64
# Visualize the arbitrage spread from late in the dataset in a box plot
arbitrage_spread_late.plot(kind="box")
<AxesSubplot:>

Step 4: Calculate the Arbitrage Profits
Calculate the potential profits for each date that you selected in the previous section. Your goal is to determine whether arbitrage opportunities still exist in the Bitcoin market. Complete the following steps:

For each of the three dates, measure the arbitrage spread between the two exchanges by subtracting the lower-priced exchange from the higher-priced one. Then use a conditional statement to generate the summary statistics for each arbitrage_spread DataFrame, where the spread is greater than zero.

For each of the three dates, calculate the spread returns. To do so, divide the instances that have a positive arbitrage spread (that is, a spread greater than zero) by the price of Bitcoin from the exchange you’re buying on (that is, the lower-priced exchange). Review the resulting DataFrame.

For each of the three dates, narrow down your trading opportunities even further. To do so, determine the number of times your trades with positive returns exceed the 1% minimum threshold that you need to cover your costs.

Generate the summary statistics of your spread returns that are greater than 1%. How do the average returns compare among the three dates?

For each of the three dates, calculate the potential profit, in dollars, per trade. To do so, multiply the spread returns that were greater than 1% by the cost of what was purchased. Make sure to drop any missing values from the resulting DataFrame.

Generate the summary statistics, and plot the results for each of the three DataFrames.

Calculate the potential arbitrage profits that you can make on each day. To do so, sum the elements in the profit_per_trade DataFrame.

Using the cumsum function, plot the cumulative sum of each of the three DataFrames. Can you identify any patterns or trends in the profits across the three time periods?

(NOTE: The starter code displays only one date. You'll want to do this analysis for two additional dates).

1. For each of the three dates, measure the arbitrage spread between the two exchanges by subtracting the lower-priced exchange from the higher-priced one. Then use a conditional statement to generate the summary statistics for each arbitrage_spread DataFrame, where the spread is greater than zero.
NOTE: For illustration, only one of the three dates is shown in the starter code below.

# For the date early in the dataset, measure the arbitrage spread between the two exchanges
# by subtracting the lower-priced exchange from the higher-priced one
arbitrage_spread_middle = bitstamp_sliced.loc['2018-02-15'] - coinbase_sliced.loc['2018-02-15']
arbitrage_spread_late = bitstamp_sliced.loc['2018-03-15'] - coinbase_sliced.loc['2018-03-15']
arbitrage_spread_early = bitstamp_sliced.loc['2018-01-15'] - coinbase_sliced.loc['2018-01-15']
​
# Use a conditional statement to generate the summary statistics for each arbitrage_spread DataFrame
​
arbitrage_spread_middle.describe()
arbitrage_spread_late.describe()
arbitrage_spread_early.describe()
count    1440.000000
mean       28.953458
std        35.145705
min      -106.080000
25%        10.000000
50%        34.035000
75%        52.217500
max       170.980000
Name: Close, dtype: float64
2. For each of the three dates, calculate the spread returns. To do so, divide the instances that have a positive arbitrage spread (that is, a spread greater than zero) by the price of Bitcoin from the exchange you’re buying on (that is, the lower-priced exchange). Review the resulting DataFrame.
# For the date early in the dataset, calculate the spread returns by dividing the instances when the arbitrage spread is positive (> 0) 
# by the price of Bitcoin from the exchange you are buying on (the lower-priced exchange).
spread_return_middle= arbitrage_spread_middle[arbitrage_spread_middle>0] / coinbase_sliced.loc['2018-02-15']
spread_return_late= arbitrage_spread_late[arbitrage_spread_late>0] / coinbase_sliced.loc['2018-03-15']
spread_return_early= arbitrage_spread_early[arbitrage_spread_early>0] / coinbase_sliced.loc['2018-01-15']
​
# Review the spread return DataFrame
spread_return_middle.head()
spread_return_late.head()
spread_return_early.head().dropna()
Timestamp
2018-01-15 00:01:00    0.001451
2018-01-15 00:02:00    0.002781
2018-01-15 00:03:00    0.001365
2018-01-15 00:04:00    0.002754
Name: Close, dtype: float64
3. For each of the three dates, narrow down your trading opportunities even further. To do so, determine the number of times your trades with positive returns exceed the 1% minimum threshold that you need to cover your costs.
# For the date early in the dataset, determine the number of times your trades with positive returns 
# exceed the 1% minimum threshold (.01) that you need to cover your costs
profitable_trades_middle = spread_return_middle[spread_return_middle > .01]
profitable_trades_late = spread_return_late[spread_return_late > .01]
profitable_trades_early = spread_return_early[spread_return_early > .01]
​
# Review the first five profitable trades
profitable_trades_middle.head()
profitable_trades_late.head()
profitable_trades_early.head()
Timestamp
2018-01-15 09:01:00    0.010570
2018-01-15 09:02:00    0.010075
2018-01-15 09:03:00    0.011180
2018-01-15 09:05:00    0.012042
2018-01-15 09:06:00    0.010843
Name: Close, dtype: float64
4. Generate the summary statistics of your spread returns that are greater than 1%. How do the average returns compare among the three dates?
# For the date early in the dataset, generate the summary statistics for the profitable trades
# or you trades where the spread returns are are greater than 1%
profitable_trades_middle.describe()
profitable_trades_late.describe()
profitable_trades_early.describe()
count    5.000000
mean     0.010942
std      0.000736
min      0.010075
25%      0.010570
50%      0.010843
75%      0.011180
max      0.012042
Name: Close, dtype: float64
5. For each of the three dates, calculate the potential profit, in dollars, per trade. To do so, multiply the spread returns that were greater than 1% by the cost of what was purchased. Make sure to drop any missing values from the resulting DataFrame.
# For the date early in the dataset, calculate the potential profit per trade in dollars 
# Multiply the profitable trades by the cost of the Bitcoin that was purchased
profit_late = profitable_trades_late * coinbase_sliced.loc['2018-03-15']
profit_middle = profitable_trades_middle * coinbase_sliced.loc['2018-02-15']
profit_early = profitable_trades_early * coinbase_sliced.loc['2018-01-15']
​
# Drop any missing values from the profit DataFrame
profit_per_trade_late = profit_late.dropna()
profit_per_trade_middle = profit_middle.dropna()
profit_per_trade_early = profit_early.dropna()
​
# View the early profit DataFrame
profit_per_trade_late.head()
profit_per_trade_middle.head()
profit_per_trade_early.head()
Timestamp
2018-01-15 09:01:00    149.59
2018-01-15 09:02:00    142.92
2018-01-15 09:03:00    158.67
2018-01-15 09:05:00    170.98
2018-01-15 09:06:00    153.97
Name: Close, dtype: float64
6. Generate the summary statistics, and plot the results for each of the three DataFrames.
# Generate the summary statistics for the early profit per trade DataFrame
profit_per_trade_late.describe()
profit_per_trade_middle.describe()
profit_per_trade_early.describe()
count      5.000000
mean     155.226000
std       10.545489
min      142.920000
25%      149.590000
50%      153.970000
75%      158.670000
max      170.980000
Name: Close, dtype: float64
# Plot the results for the early profit per trade DataFrame
profit_per_trade_late.plot(figsize=(10, 7), title="Coinbase Profits")
profit_per_trade_middle.plot(figsize=(10, 7), title="Coinbase Profits")
profit_per_trade_early.plot(figsize=(10, 7), title="Coinbase Profits")
​
<AxesSubplot:title={'center':'Coinbase Profits'}, xlabel='Timestamp'>

7. Calculate the potential arbitrage profits that you can make on each day. To do so, sum the elements in the profit_per_trade DataFrame.
# Calculate the sum of the potential profits for the early profit per trade DataFrame
profit_sum = profit_per_trade_middle.sum()
profit_sum = profit_per_trade_late.sum()
profit_sum = profit_per_trade_early.sum()
profit_sum
776.1299999999992
8. Using the cumsum function, plot the cumulative sum of each of the three DataFrames. Can you identify any patterns or trends in the profits across the three time periods?
# Use the cumsum function to calculate the cumulative profits over time for the early profit per trade DataFrame
cumulative_profit_late = profit_per_trade_late.cumsum()
cumulative_profit_middle = profit_per_trade_middle.cumsum()
cumulative_profit_early = profit_per_trade_early.cumsum()
# Plot the cumulative sum of profits for the early profit per trade DataFrame
cumulative_profit_late.plot(figsize=(10, 7), title="Cumulative Coinbase Profits")
cumulative_profit_middle.plot(figsize=(10, 7), title="Cumulative Coinbase Profits")
cumulative_profit_early.plot(figsize=(10, 7), title="Cumulative Coinbase Profits")
<AxesSubplot:title={'center':'Cumulative Coinbase Profits'}, xlabel='Timestamp'>

**Question:** After reviewing the profit information across each date from the different time periods, can you identify any patterns or trends?
    
**Answer:** The greatest profit trend comes early on in the data set in January. There seems to be a large variance in the spread between bitstamp and coinbase. During this time, the largest amount of profits are accumulated. As time continues the spread between the two exchanges decreases. While the day selected for the month of January was an ultimate decrease in prices, it shows that the spread and profit potential for coinbase is the best. The day's selected for the other two months had an increase in prices for the days but don't have as great of a spread. For this reason the day selected in the month of January is the greatest profit potential.
