# A/B Testing for Cookie Cats Game Gate Placement

This project analyzes the results of an A/B test conducted on the mobile game Cookie Cats. The test involved moving the first in-game gate that requires players to wait or make a purchase to progress from level 30 (group A - control) to level 40 (group B - test). The primary goal is to determine the impact of this change on player retention (1-day and 7-day) and the number of game rounds played.

## Business Problem

The game developers at Tactile Entertainment are experimenting with the placement of the first in-app purchase gate in Cookie Cats. They want to understand if moving this gate from level 30 to level 40 has a significant effect on how long players continue to play the game and their engagement, measured by the number of game rounds played. The findings will help inform decisions on game design and monetization strategies.

## Methodology

The project follows a step-by-step A/B testing methodology:

1.  **Data Loading and Exploration:** The `cookie_cats.csv` dataset is loaded, and initial exploratory data analysis (EDA) is performed to understand the data structure, identify missing values, and examine summary statistics.
2.  **Outlier Analysis and Handling:** An extreme outlier in the `sum_gamerounds` variable is identified and removed to ensure it does not skew the analysis.
3.  **Visual Analysis:** Distributions of game rounds played for both groups (gate at level 30 and gate at level 40) are visualized using histograms and box plots to get an initial sense of any differences. The number of users at different game round milestones is also examined.
4.  **Retention Rate Analysis:** 1-day and 7-day retention rates are calculated and compared between the two groups. The combination of both retention metrics is also explored.
5.  **Statistical Hypothesis Testing:**
    * The control group (gate at level 30) and the test group (gate at level 40) are defined.
    * The Shapiro-Wilk test is applied to assess the normality of the `sum_gamerounds` distribution for both groups.
    * Based on the normality test results, a suitable statistical test is chosen to compare the means (or distributions) of `sum_gamerounds` between the two groups. Since the data is not normally distributed, the non-parametric Mann-Whitney U test is used.
    * The null hypothesis (H0: there is no significant difference in `sum_gamerounds` between the two groups) and the alternative hypothesis (H1: there is a significant difference in `sum_gamerounds` between the two groups) are formulated.
    * The chosen statistical test is performed, and the p-value is evaluated to either reject or fail to reject the null hypothesis.
6.  **Conclusion and Recommendations:** Based on the statistical test results and the analysis of retention rates, conclusions are drawn about the impact of moving the gate to level 40. Recommendations are provided regarding which gate placement strategy might be more beneficial.

## Code Description

The project is implemented in a Jupyter Notebook (`A B Testing Step by Step.ipynb`), which has been converted to a Python script. The script performs the following steps:

* **Import Libraries:** Imports necessary libraries such as `numpy`, `pandas`, `seaborn`, `matplotlib.pyplot`, `scipy.stats`, and `warnings`.
* **`load` Function:** A utility function to load data from CSV or Excel files and display basic information (number of observations, columns, data types, missing values, memory usage).
* **Data Loading:** The `cookie_cats.csv` dataset is loaded using the `load` function.
* **Initial Data Exploration:** The number of unique users is checked, and descriptive statistics for `sum_gamerounds` are displayed.
* **A/B Group Summary:** Summary statistics (count, median, mean, standard deviation, max) of `sum_gamerounds` are calculated for both the 'gate_30' and 'gate_40' versions.
* **Visualizations (Before Outlier Removal):** Histograms showing the distribution of `sum_gamerounds` for each group and a box plot comparing the two groups are generated. Time series plots of `sum_gamerounds` for both groups are also created.
* **Outlier Removal:** The row with the maximum `sum_gamerounds` (an extreme outlier) is removed from the dataset.
* **Visualizations (After Outlier Removal):** Similar visualizations as before are generated on the cleaned data.
* **User Progression Analysis:** The number of users at each `sum_gamerounds` milestone is plotted to understand player drop-off. The number of users who reached gates at level 30 and 40 is specifically examined.
* **Retention Analysis:**
    * Counts and ratios of `retention_1` (1-day retention) and `retention_7` (7-day retention) are calculated.
    * Summary statistics of `sum_gamerounds` are calculated for each version, broken down by `retention_1` and `retention_7` status.
    * A combined 'Retention' variable is created for users retained on both day 1 and day 7, and `sum_gamerounds` statistics are compared for retained vs. non-retained users in each version.
    * A new 'NewRetention' categorical variable combining `retention_1` and `retention_7` is created, and `sum_gamerounds` statistics are analyzed for each category within each version.
* **A/B Testing Function (`AB_Test`):** A function is defined to perform the A/B test, including:
    * Splitting the data into group A (gate_30) and group B (gate_40).
    * Applying the Shapiro-Wilk test for normality.
    * If data is parametric, applying Levene's test for homogeneity of variances and then the appropriate t-test (independent samples t-test or Welch's t-test).
    * If data is non-parametric, applying the Mann-Whitney U test.
    * Returning a DataFrame with the test results (p-value, hypothesis outcome, test type, and comments).
* **Applying A/B Test:** The `AB_Test` function is called to compare the `sum_gamerounds` between the two gate placement strategies.
* **Conclusion:** The results of the A/B test and the retention rate analysis are summarized, providing insights into the impact of moving the gate. The average 1-day and 7-day retention rates for both groups are calculated and compared.

## Data Source

The project uses the `cookie_cats.csv` dataset, which contains data from players of the mobile game Cookie Cats who were part of an A/B test. The dataset includes user IDs, the version of the game they were assigned (gate at level 30 or 40), the number of game rounds they played, and their 1-day and 7-day retention status.

## Libraries Used

* `numpy`: For numerical operations.
* `pandas`: For data manipulation and analysis.
* `seaborn`: For statistical data visualization.
* `matplotlib.pyplot`: For creating plots and visualizations.
* `scipy.stats`: For statistical tests (Shapiro-Wilk, Levene, Mann-Whitney U, t-tests).
* `warnings`: To manage warning messages.

## Running the Code

To run the analysis, you will need:

1.  Python 3 installed on your system.
2.  The required libraries installed. You can install them using pip:
    ```bash
    pip install numpy pandas seaborn matplotlib scipy
    ```
3.  The `cookie_cats.csv` file in the same directory as the Python script or provide the correct path to the file.

Simply execute the `A B Testing Step by Step.ipynb` script (or run it as a Jupyter Notebook) to perform the A/B test analysis and generate the results.
