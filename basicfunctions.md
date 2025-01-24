# Data Preprocessing Guide with `pandas` ETL

## Import library and read csv
Importing Required Library 

`import pandas as pd`

Read the values from a CSV file

`data = pd.read_csv('file.csv')`


## Basic commands to check data
Check the length of the data

`len(data)`

**Check for missing values**, returns True where values are missing

`data.isna()`

View a summary of missing values

`data.isna().sum()`

Calculate and display missing value percentages

`missing_percentage = data.isna().sum() / len(data) * 100`

## Time in dataframe & manipulation

Convert the 'time' column from object to datetime for better visibility

`data['time'] = pd.to_datetime(data['time'])`

Find the earliest and latest date-time values
```
data['time'].min()  # Earliest

data['time'].max()  # Latest
```

Replace missing values in a column with the earliest value

`data['Last Seen'].fillna(value=data['Last Seen'].min(), inplace=True)`


## Filter out smallest errors using .isna().sum() and using .fillna() function

Use dropna() to drop majority of missing values, then assign it as a sample data Dropna() removes all the records that contain missing values 

`data_sample = data.dropna()`

Drop a specific column:

`data_sample = data_sample.drop(columns='Tags')`

View unique values in a column called 'City'
``` 
city_unique = data_sample['City'].unique()
city_unique.sort() 
```


Replace specified values with a specified value
```
data_sample['City'].replace(to_replace=[
    'Winston Salem', 'Winston Salem ', 'Winston salem', 'Winston salem ', 
    'Winston-Salem', 'Winston-Salem ', 'Winston-Salem, NC', 'Winston-salem'
], value="Winston_Salem", inplace=True)
```

Remove empty spaces

`data_sample['City'] = data_sample['City'].str.strip()`

Capitalize the first letter of each word

`data_sample['City'] = data_sample['City'].str.title()`

Replace values with a dictionary

```
for state_name in us_state_to_abbrev:
    data_sample['State'].replace(to_replace=state_name, value=us_state_to_abbrev[state_name], inplace=True)

Use items() method to return a tuple of values from a dictionary

Example: [('Alabama', 'AL'), ('Alaska', 'AK'), ('Arizona', 'AZ')]
```

## Column & row data manipulation

### Merge the original dataframe with another dataframe (states_df)
```
data_sample = pd.merge(data_sample, states_df, on='State', how='left')  # how= parameter indicates join type (e.g., left, right, inner)
```

### Rename a column
`data_sample.rename(columns={'State': 'State Abbreviation'}, inplace=True)`

### Use pop() to remove a column and return it as a Series
`state_name_col = data_sample.pop('State Name')`

### Insert a column into a DataFrame at a specified location
`data_sample.insert(3, 'State Name', state_name_col)`

### Zip codes are 5 digits; use slicing to limit them to five
`data_sample['Zip'] = data_sample['Zip'].str[:5]`

### Boolean index to check for zip codes with a length of five digits
`zip_code_boolean_index = data_sample['Zip'].str.len() == 5`

### Drop records that have a zip code length not equal to five

`data_sample = data_sample[zip_code_boolean_index]`

### Drop rows where column name is 'City' and values are 'G' or 'Lmao'
```
data_sample = data_sample[data_sample['City'] != 'G']
data_sample = data_sample[data_sample['City'] != 'Lmao']
```