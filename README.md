## Objective :
- This dataset documents the start and end dates of U.S. presidential terms, including the president’s name, political party, and term duration. It is commonly used to:
- Teach data wrangling and date/time manipulation.
- Create time-based charts (e.g., timeline plots or shaded regions by party).
- Analyze trends in leadership, party dominance, or term lengths.

### Data Fetching
- A reusable function that downloads the raw text content (CSV) from a URL.
- Checks if the request was successful (status_code == 200), otherwise prints an error.
- raw_url stores the URL of the presidential.csv file.
- data stores the raw CSV content (as a string) fetched from GitHub

### Load CSV into DataFrame
- StringIO(data) turns the string into a file-like object so pandas can read it.
- parse_dates=["start", "end"]: automatically parses the date columns.
- presidential: a pandas DataFrame containing structured data of U.S. presidents.
- .info() gives summary of columns, non-null counts, and data types.
- [['name', 'party']]: selects specific columns to view.
- Filters rows for presidents from the Republican party.

### Conditional Filtering: Democrats After 1973
- Filters Democratic presidents who started their term after 1973.
- Shows only their names.

### Calculate Term Length
- Calculates length of each presidential term in years.
- Uses .dt.days to get number of days and divides by 365.25 (accounts for leap years).
- Adds a new column term.length.

### Add 'Elected' Year Column
- Creates a new column elected = one year before the term started.
- In the U.S., elections are typically held the year before the president assumes office

### Handle Anomalies in 'Elected' Column
- Replaces certain invalid or non-standard elected years (1962 and 1973) with NaN (missing value).
- These may correspond to presidents who took office unexpectedly (e.g., after resignation or death).
- Renames the column term.length to term_length for Python-friendly syntax and consistency with naming conventions (no dot notation).
- Displays the updated DataFrame.

First sort: Shows presidents sorted by longest term (descending).
Second sort: Adds tie-breaking sort by:
- Party (alphabetically),
- Election year (earlier years first).

- N: Total number of presidents.
- first_year: Earliest term start year.
- last_yeaer: Latest term end year (note: typo in "last_yeaer").
- num_DEMS: Number of Democratic presidents.
- years: Total number of presidential years (sum of all term lengths).
- avg_term_length: Average term length (in years), rounded to 2 decimals.

### Subset by Party
- Creates two separate DataFrames for Democratic and Republican presidents.
- Builds similar summaries for each political party: 
Number of presidents (N), First and last years in office, Total years served, Average term length.
- Merges the two party-specific summaries into one table.
- Sets index names to clearly identify rows by party.

### Conclusion
- Republicans have held the presidency for a longer total duration (40 years) compared to Democrats (28 years) since the 1950s.
- The average term length is slightly higher for Republicans (5.71 years) than Democrats (5.60 years), indicating comparable presidential tenure across parties.
- The data suggests a relatively balanced pattern of power shifts between the two major U.S. parties, with Republicans having a slight edge in both count and cumulative duration during this period.
