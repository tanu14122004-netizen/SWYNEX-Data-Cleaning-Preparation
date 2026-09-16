# SWYNEX Data Cleaning & Preparation

## Project Overview

This project focuses on cleaning and preparing a publicly available IPL
(Indian Premier League) ball-by-ball dataset for further analysis.

The dataset contains detailed information about IPL matches, including
match details, teams, venues, toss information, batters, bowlers, runs,
wickets, match results, and player information.

The main objective of this project was to identify data quality issues,
analyze them, and prepare a cleaner and more consistent dataset using
Python and Pandas.

---

## Dataset

The dataset is an IPL ball-by-ball dataset containing:

- Match information
- Season and date
- City and venue
- Teams
- Toss information
- Batting and bowling information
- Runs and extras
- Wickets
- Match results
- Player of the Match information

### Dataset Size

- **Rows:** 278,205
- **Columns:** 32

---

## Data Cleaning Process

### 1. Missing Value Analysis

Missing values were analyzed across all columns.

The following columns contained a high percentage of missing values:

- `wicket_kind`
- `player_out`
- `fielder`

These missing values were retained because they represent deliveries where
no relevant dismissal event occurred.

Similarly, missing values in:

- `target_score`
- `required_run_rate`

were retained where these values were not applicable or could not be
reliably derived.

Missing values were therefore not blindly replaced with zero, mean, mode,
or arbitrary values.

---

### 2. City Column

Missing values in the `city` column were investigated using the
corresponding `venue`.

Where the venue provided reliable information, the missing city values
were filled.

For example:

- `Dubai International Cricket Stadium` → `Dubai`
- `Sharjah Cricket Stadium` → `Sharjah`

The city column was then checked again after treatment.

---

### 3. Winner Column

Missing values in the `winner` column were investigated using:

- `match_id`
- `inning`
- `batting_team`
- `result`

The relationship between the winner and the second-innings batting team
was analyzed.

Where the second-innings batting team provided reliable information,
missing winner values were filled.

Where the winner could not be determined reliably from the available
information, the values were retained as missing rather than making
assumptions.

The cleaned winner column was then validated to ensure:

- Each match has at most one unique winner.
- The winner belongs to either `team1` or `team2`.
- Wicket-result matches were checked against the second-innings batting
  team.

---

### 4. Player of the Match

The `player_of_match` column contained missing values.

The missing values were investigated at the `match_id` level to determine
whether a Player of the Match value was available elsewhere in the same
match.

For matches where the Player of the Match information was unavailable
throughout the match, the missing values were retained rather than
assigning an arbitrary player.

---

### 5. Result Margin

The `result_margin` column contained inconsistent data types and
`undefined` values.

The column contained **4,702 `undefined` values**.

The problematic values could not be reliably recovered from the available
data. Since the column was not essential for the intended analysis, it
was removed from the dataset.

---

### 6. Venue Standardization

The `venue` column contained multiple names referring to the same
stadium.

Different naming variations were standardized into consistent venue
names.

Examples include:

- `Arun Jaitley Stadium, Delhi`
  → `Arun Jaitley Stadium`

- `Feroz Shah Kotla`
  → `Arun Jaitley Stadium`

- `M Chinnaswamy Stadium, Bengaluru`
  → `M Chinnaswamy Stadium`

- `M.Chinnaswamy Stadium`
  → `M Chinnaswamy Stadium`

- `Wankhede Stadium, Mumbai`
  → `Wankhede Stadium`

- `Rajiv Gandhi International Stadium, Uppal, Hyderabad`
  → `Rajiv Gandhi International Stadium`

- `Sawai Mansingh Stadium, Jaipur`
  → `Sawai Mansingh Stadium`

This standardization helps prevent the same stadium from appearing as
multiple separate categories during analysis.

---

### 7. Date Validation

The `date` column was checked for:

- Data type
- Missing values
- Sample values
- Number of unique dates

No major correction was required for the date column.

---

### 8. Team Name Validation

The following team-related columns were checked for consistency:

- `team1`
- `team2`
- `toss_winner`
- `winner`
- `batting_team`
- `bowling_team`

The team values were inspected for unexpected or inconsistent entries.

---

### 9. Result and Toss Decision Validation

The `result` column was checked for its unique values.

The dataset contained:

- `runs`
- `wickets`

The `toss_decision` column was also checked and contained:

- `field`
- `bat`

These values were validated as part of the data-quality checking process.

---

### 10. Numerical Data Type Validation

Numerical columns were checked to ensure that their data types were
appropriate.

The following types of fields were validated:

- Match ID
- Season
- Innings
- Over
- Ball
- Runs scored
- Extras
- Current score
- Wickets down
- Balls remaining
- Wickets remaining
- Current run rate
- Required run rate
- Target score

---

### 11. Duplicate Records

The dataset was checked for duplicate rows.

**Result: No duplicate records were found.**

Therefore, no rows were removed because of duplication.

---

## Data Quality Approach

The cleaning process was performed based on the meaning and context of
each column.

Missing values were not automatically removed or replaced.

Where reliable information was available, values were corrected or
recovered.

Where information could not be reliably determined, the original missing
value was retained.

This approach helps maintain the integrity of the original dataset while
making it more consistent and suitable for further analysis.

---

## Tools Used

- **Python**
- **Pandas**
- **NumPy**
- **Jupyter Notebook**

---

## Output

The cleaned dataset was saved as:

`ipl_cleaned_new.csv`

A compressed version of the cleaned dataset is also included in the
repository to meet file-size limitations.

The Jupyter Notebook containing the complete cleaning and validation
process is also included in this repository.

---

## Conclusion

The IPL ball-by-ball dataset was systematically inspected, cleaned, and
validated using Python and Pandas.

The project addressed missing values, inconsistent venue names,
problematic data types, undefined values, and duplicate records.

The final cleaned dataset is now prepared for further data analysis.
