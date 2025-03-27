# Banknotes-Data-Analysis-Dashboard

## Overview ##
This Python script builds an interactive dashboard using the `Dash` framework with a dark theme, styled via `dash_bootstrap_components` and the `DARKLY` theme. The dashboard's purpose is to analyze a dataset of banknotes by exploring attributes of the figures depicted on them, such as their profession, lifespan, and geographic distribution. The script is divided into several key sections:
- Data loading and preprocessing
- Feature engineering
- Filter options
- Interactive visualizations organized across multiple tabs

The tabs provide distinct analyses, including main analysis, trends, geography, correlation, machine learning, network visualization, and forecasting.

## 1. Importing Libraries ##
The script imports various Python libraries to support its functionality:
- **Data Manipulation and Visualization:**
    - `pandas` and `numpy` handle data processing.
    - `plotly.express` and `plotly.graph_objects` create interactive visualizations.
- **Dash and Bootstrap Components:**
    - `Dash` (with submodules `dcc`, `html`, and `dash_table`) constructs the web application.
    - `dash_bootstrap_components` applies a dark theme.
- **Machine Learning and Evaluation:**
    - `sklearn.ensemble.RandomForestClassifier` implements a RandomForest model.
    - `sklearn.metrics` computes accuracy, F1-score, precision, and recall.
- **Statistical Testing:**
    - `scipy.stats.chi2_contingency` conducts chi-squared tests.
- **Forecasting:**
    - `Prophet` performs time-series forecasting.
- **Network Visualization:**
    - **networkx** generates graphs of relationships between figures.

## 2. Data Loading and Preprocessing ##
- **Loading the Dataset:**
    - The script loads data from a CSV file named `banknotesData.csv` using `pandas.read_csv()`.
    - It prints few first and last rows to confirm successful loading.
- **Handling Missing Values:**
    - Numeric columns are filled with median values.
    - String columns are filled with "Unknown".
    - The `deathDate` column is converted to numeric values, with invalid entries coerced to `NaN`.

## 3. Feature Engineering ##
- **Pioneer Flag:**
    - A new column, `isPioneer`, is added.
    - It is True if `knownForBeingFirst` (stripped and lowercased) equals "yes", otherwise False.
- **Profession Standardization and Classification:**
    - The `profession` column is converted to title case and saved as `profession_clean`.
    - A function, `classify_profession()`, categorizes professions and storing results in `prof_category`.
- **LifeSpan Calculation:**
    - The `lifeSpan` column is calculated as the absolute difference between `deathDate` and `firstAppearanceDate`, ensuring positive values.

## 4. Filter Options and Helper Variables ##
The dashboard includes interactive filters:
- **Dropdown Filters:**
    - Options for `Country`, `Gender`, `Pioneer`, and `Profession`.
- **Range Sliders:**
    - Sliders for `First Appearance Year` and `Bill Value`.
- **Specialized Filters:**
    - A dropdown for profession category in the geography tab.
    - A country filter for the network visualization.

## 5. App Layout ##
The dashboard layout is built with Dash components:
- **Header and Global Filters:**
    - A header appears at the top.
    - Global filters include dropdowns for `Country`, `Gender`, `Pioneer`, and `Profession`, plus sliders for `First Appearance Year` and `Bill Value`.
    - A "Reset Filters" button resets all filters to defaults.
- **Tabs:**
    - ***Main Analysis Tab:***
        - Bar chart of profession category counts
        - Scatter plot of bill value vs. waiting time
        - Grouped bar chart of professions by gender
        - Box plot of waiting time by pioneer status
        - Data table of the dataset
    - ***Trends Analysis Tab:***
        - Line chart of banknote distribution over time
        - Radio button to group by gender or profession
        - Moving average lines for smoothing
    - ***Geography Analysis Tab:***
        - Choropleth map of banknote distribution by country
        - Dropdown to filter by profession category
    - ***Correlation Analysis Tab:***
        - Heatmap of numerical correlations
        - Cross-tab heatmap of gender vs. profession
        - Chi-squared test results
    - ***Machine Learning Tab:***
        - Bar chart of RandomForest feature importance
        - Text displaying accuracy, F1-score, precision, and recall
    - ***Network Visualization Tab:***
        - Interactive graph of relationships between figures
        - Built with `networkx` and `kamada_kawai_layout`
        - Country filter for nodes
    - ***Forecasting Tab:***
        - Time-series forecast of banknote counts using Prophet
        - Visualization of historical and forecasted data

## 6. Callbacks ##
Dash callbacks make the dashboard interactive:
- **Reset Filters Callback:**
    - Triggered by the "Reset Filters" button to restore default filter values.
- **Main Visualization Callback:**
    - Responds to changes in all filters.
    - ***Data Filtering:*** Applies selected filters to the dataset.
    - ***Main Analysis:*** Updates bar, scatter, grouped bar, box plot, and table.
    - ***Trends:*** Reindexes data for all years, adds smoothing, and updates the line chart.
    - ***Geography:*** Groups data by country and updates the choropleth map.
    - ***Correlation:*** Computes heatmaps and chi-squared results.
    - ***Machine Learning:*** Trains a RandomForest model, showing feature importance and metrics.
    - ***Network:*** Builds a networkx graph with nodes and edges, using kamada_kawai_layout.
    - ***Forecasting:*** Uses Prophet to forecast five years ahead, plotting historical and predicted data.

## 7. Running the Application ##
- The script runs the Dash app in debug mode.
- It starts a local server, allowing access to the dashboard via a web browser.
