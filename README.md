# KL Field Porosity Analysis

## Project Overview

This project demonstrates a beginner-friendly Python and Excel workflow
for analyzing sample porosity data associated with the KL Field learning
project. It summarizes porosity measurements, assigns porosity classes,
visualizes the results, and exports the data and summary statistics to
an Excel workbook.

> **Important:** The workbook currently discussed contains five
> illustrative sample records (A--E). These results should not be
> treated as validated field-wide KL Field findings unless the values
> are confirmed against the actual project dataset.

## Project Files

-   `KL_Field_Porosity_Results.xlsx` --- Excel workbook containing the
    sample data and summary statistics.
-   `KL_Field_Porosity_Class_Distribution.png` --- high-resolution chart
    showing the percentage distribution of porosity classes.
-   `KL_Field_Analysis.ipynb` --- Jupyter Notebook for the Python
    analysis, if saved separately.

## Workbook Contents

The Excel workbook contains two worksheets:

### `Sample_Data`

Contains the columns:

-   `Sample` --- sample identifier.
-   `Porosity` --- porosity value, expressed as a percentage.
-   `prosity_Class` --- porosity class assigned using the threshold
    described below. The column name preserves the spelling used in the
    current dataset.

### `Summary`

Contains summary statistics for the `Porosity` column:

-   Count
-   Minimum
-   Maximum
-   Mean
-   Median

## Methods

The analysis was performed in Python using pandas and Matplotlib in a
Jupyter Notebook.

1.  Loaded and inspected the sample dataset.
2.  Checked for missing values and duplicate rows.
3.  Calculated descriptive statistics, including count, minimum,
    maximum, mean, and median.
4.  Classified samples as `High` when porosity was greater than or equal
    to 20%, and `Low` when porosity was below 20%.
5.  Calculated the count and percentage of samples in each class.
6.  Filtered samples with porosity strictly above the overall mean.
7.  Used the interquartile range (IQR) method to check for potential
    outliers.
8.  Created bar charts and a box plot to visualize the results.
9.  Exported the sample data and summary statistics to Excel.

## Results from the Current Five-Sample Example

  Metric                                             Result
  ----------------------------------------------- ---------
  Number of samples                                       5
  Minimum porosity                                       8%
  Maximum porosity                                      36%
  Mean porosity                                         20%
  Median porosity                                       20%
  High-class samples                                3 (60%)
  Low-class samples                                 2 (40%)
  Samples strictly above the mean                   2 (40%)
  Potential outliers identified by the IQR rule           0

Class-level summary:

  Class     Count   Mean porosity   Minimum   Maximum
  ------- ------- --------------- --------- ---------
  High          3          26.67%       20%       36%
  Low           2             10%        8%       12%

The class threshold is 20%, so a sample with exactly 20% porosity is
classified as `High`.

## Software and Libraries

-   Python
-   Jupyter Notebook / Anaconda
-   pandas
-   Matplotlib
-   openpyxl (used by pandas to write Excel `.xlsx` files)

## How to Reproduce the Excel Export

The following example writes the sample data and summary statistics to
separate worksheets:

``` python
import pandas as pd

summary = df["Porosity"].agg(["count", "min", "max", "mean", "median"])
summary_df = summary.reset_index()
summary_df.columns = ["Statistic", "Value"]

with pd.ExcelWriter("KL_Field_Porosity_Results.xlsx") as writer:
    df.to_excel(writer, sheet_name="Sample_Data", index=False)
    summary_df.to_excel(writer, sheet_name="Summary", index=False)
```

## Limitations and Next Steps

-   The current example contains only five samples, so it is intended to
    demonstrate the workflow rather than support robust geological
    conclusions.
-   Confirm the classification threshold and units before using the
    workflow on real field data.
-   For a full petrophysical study, apply quality control to actual
    well-log data and document any missing-value treatment, assumptions,
    and calculations.
-   If the workbook is used in a research submission, replace
    illustrative records with verified project data and retain
    reproducible notebook code.

## Authoring Note

The Excel workbook and chart were saved on the Windows computer in the
folder:

`C:\\Users\\owner`

The README should be placed in the same project folder or in the root of
the GitHub repository.
