
# The World’s Mood Map: Can News Tone Predict Protests, Conflict, and Diplomacy?

## Project Overview

This project is a Python Data Analytics course project that analyzes global news event data from the **GDELT 2.0 Event Database**. The goal is to investigate whether the tone of global news coverage can reveal patterns related to protests, conflict, diplomacy, and international tension.

The project uses structured event data extracted from global news sources. Each event contains information such as the date, country, event type, media tone, number of mentions, number of sources, and Goldstein Scale score. Using Python, the notebook performs data collection, cleaning, feature engineering, exploratory data analysis, visualization, and the creation of a custom **Global Tension Index**.

---

## Research Question

**Can the tone of global news coverage help identify countries or events associated with protests, conflict, and diplomacy?**

The project explores whether negative media tone, event type, and media attention are connected to higher levels of reported conflict or protest activity.

---

## Dataset

### Dataset Name

**GDELT 2.0 Event Database**

### Source

GDELT 2.0 Master File List:  
`http://data.gdeltproject.org/gdeltv2/masterfilelist.txt`

### Data Format

The dataset is provided as compressed `.CSV.zip` files. Each file contains global news event records from a specific 15-minute time interval.

### Dataset Size

The full GDELT database is extremely large and continuously updated. This notebook downloads a sample of recent `.export.CSV.zip` files from the GDELT master file list. The sample still provides more than 1,000 rows and more than 10 columns, satisfying the project requirements.

---

## Key Columns Used

| Column | Description |
|---|---|
| `GLOBALEVENTID` | Unique identifier for each event |
| `SQLDATE` | Date of the event |
| `Actor1Name` | First actor involved in the event |
| `Actor1CountryCode` | Country code of the first actor |
| `Actor2Name` | Second actor involved in the event |
| `Actor2CountryCode` | Country code of the second actor |
| `EventCode` | Specific event code |
| `EventRootCode` | Broader event category code |
| `QuadClass` | General category: cooperation or conflict |
| `GoldsteinScale` | Numerical score of cooperation or conflict intensity |
| `NumMentions` | Number of event mentions |
| `NumSources` | Number of sources reporting the event |
| `NumArticles` | Number of articles covering the event |
| `AvgTone` | Average tone of news coverage |
| `ActionGeo_CountryCode` | Country where the event occurred |
| `ActionGeo_Lat` | Latitude of the event location |
| `ActionGeo_Long` | Longitude of the event location |
| `SOURCEURL` | News source URL |

---

## Tools and Libraries Used

The project is implemented fully in Python using the following libraries:

- `pandas` — data loading, cleaning, and aggregation
- `numpy` — numerical operations
- `matplotlib` — static visualizations
- `seaborn` — statistical visualizations
- `plotly` — interactive charts and maps
- `scikit-learn` — scaling and optional clustering
- `requests` — downloading data from GDELT
- `zipfile` — reading compressed CSV files

---

## Notebook Structure

The notebook is organized into the following main sections:

1. **Project Introduction**
   - Explains the topic, research problem, and dataset.

2. **Library Imports**
   - Imports all required Python libraries.

3. **Project Configuration**
   - Sets the GDELT master file URL, number of files to download, and data folder.

4. **GDELT Column Definition**
   - Defines official GDELT column names because raw GDELT files do not include headers.

5. **Data Download**
   - Downloads the GDELT master file list.
   - Selects recent `.export.CSV.zip` files.
   - Downloads and reads selected files.

6. **Data Cleaning**
   - Converts date columns.
   - Converts numeric columns.
   - Removes rows with missing essential values.
   - Prepares the dataset for analysis.

7. **Feature Engineering**
   - Creates new analytical variables such as:
     - `event_category`
     - `attention_score`
     - `negative_tone`
     - `is_conflict`
     - `is_protest`
     - `is_diplomacy`
     - `weekday`
     - `hour_added`

8. **Exploratory Data Analysis**
   - Summarizes dataset shape, missing values, date range, countries, and event categories.

9. **Research Question Analysis**
   - Answers four main analysis questions using grouped statistics and visualizations.

10. **Global Tension Index**
    - Creates a custom index that combines negative tone, conflict share, material conflict, media attention, and Goldstein Scale.

11. **Optional Clustering**
    - Uses KMeans clustering to group countries by tone, conflict, diplomacy, and attention patterns.

12. **Exports**
    - Saves cleaned data and summary tables as CSV files for poster/report use.

---

## Main Research Questions

### Q1: Do countries with more negative news tone experience more conflict-related events?

This question compares average news tone with the share of conflict events by country.

Variables used:

- `AvgTone`
- `QuadClass`
- `ActionGeo_CountryCode`
- `GoldsteinScale`
- `NumMentions`

Methods used:

- Country-level grouping
- Correlation analysis
- Scatter plot
- Choropleth map

---

### Q2: Which event types attract the most international media attention?

This question identifies which event categories receive the highest number of mentions, sources, and articles.

Variables used:

- `EventRootCode`
- `event_category`
- `NumMentions`
- `NumSources`
- `NumArticles`
- `AvgTone`

Methods used:

- Grouped aggregation
- Attention score calculation
- Bubble chart
- Bar chart

---

### Q3: Are diplomatic events reported with a different tone than protest or conflict events?

This question compares tone and Goldstein Scale across event categories.

Variables used:

- `event_category`
- `AvgTone`
- `GoldsteinScale`
- `NumSources`
- `NumMentions`

Methods used:

- Distribution comparison
- Violin plot
- Boxplot
- Summary statistics

---

### Q4: How does global event intensity change across time?

This question examines how event volume, tone, conflict, protest, and diplomacy change over time.

Variables used:

- `event_date`
- `event_category`
- `AvgTone`
- `NumMentions`
- `is_conflict`
- `is_protest`
- `is_diplomacy`

Methods used:

- Time-series aggregation
- Rolling averages
- Line chart
- Stacked area chart
- Heatmap

---

## Global Tension Index

The project creates an original metric called the **Global Tension Index**.

The index combines:

1. Negative news tone
2. Conflict event share
3. Material conflict share
4. Media attention
5. Negative Goldstein Scale

Each component is standardized and then combined into a final score from 0 to 100.

A higher score means that a country appears more tense in the sampled global news data.

Important note: this index is not an official political risk index. It is a student-created analytical metric for comparing reported tension across countries.

---

## Visualizations Included

The notebook produces several chart types suitable for an academic poster:

1. Choropleth map — average news tone by country
2. Scatter plot — average tone vs. conflict share
3. Heatmap — correlation between tone, conflict, protest, and attention
4. Bubble chart — event categories by tone, Goldstein Scale, and mentions
5. Bar chart — top event root codes by total media mentions
6. Violin plot — news tone distribution by event category
7. Boxplot — Goldstein Scale by event category
8. Line chart — event volume and average tone over time
9. Heatmap — event frequency by weekday and hour
10. Stacked area chart — event categories over time
11. Bar chart — top countries by Global Tension Index
12. Choropleth map — Global Tension Index by country

---

## How to Run the Notebook

### Step 1: Install Required Libraries

Run the following command in the terminal if some libraries are missing:

```bash
pip install pandas numpy matplotlib seaborn plotly scikit-learn requests