

# Growth Curve Data Analysis

This project provides an R-based pipeline for processing, analyzing, and visualizing microbial growth curve data from 96-well plates. The workflow includes data cleaning, normalization, area under the curve (AUC) calculation, and publication-quality plotting for two experimental datasets (Set A and Set B).

---

## Table of Contents

- [Project Overview](#project-overview)
- [Folder Structure](#folder-structure)
- [Requirements](#requirements)
- [Data Processing Workflow](#data-processing-workflow)
- [Visualization](#visualization)
- [Usage](#usage)
- [Troubleshooting](#troubleshooting)


---

## Project Overview

This pipeline automates the analysis of microbial growth curves measured in 96-well plates. It:
- Reads and processes raw CSV data for multiple days and two datasets (Set A and Set B).
- Normalizes OD600 readings by subtracting blank controls.
- Calculates mean OD600 values and AUC for each strain and treatment.
- Produces faceted plots with growth curves and annotated AUC values.

---

## Folder Structure

```
Final_Project/
│
├── Growth_curve_IDE_5/
│   ├── A_0.csv
│   ├── A_1.csv
│   ├── ... (up to A_7.csv)
│   ├── B_0.csv
│   ├── B_1.csv
│   ├── ... (up to B_7.csv)
│
├── combined_data_A.csv
├── combined_data_B.csv
├── growth_curve_analysis.R
├── README.md
└── ...
```

---

## Requirements

- R (version 4.0 or higher recommended)
- R packages:
  - `readr`
  - `dplyr`
  - `tidyr`
  - `gcplyr`
  - `ggplot2`
  - `scales`
  - `ggpubr` (for combining plots)
  - `patchwork` (optional, for alternative plot layouts)

Install packages with:
```r
install.packages(c("readr", "dplyr", "tidyr", "ggplot2", "scales", "ggpubr"))
# For gcplyr (may require Bioconductor or GitHub installation)
# install.packages("devtools")
# devtools::install_github("swb-ief/gcplyr")
```

---

## Data Processing Workflow

1. **Data Import & Cleaning:**  
   Reads CSV files for each day and dataset, removes empty wells and extra columns, and adds row identifiers.

2. **Normalization:**  
   Subtracts the mean blank OD600 (from control wells) from each sample well to correct for background.

3. **Long Format Conversion:**  
   Converts wide-format data to long format for easier analysis and plotting.

4. **AUC Calculation:**  
   Calculates the area under the growth curve (AUC) for each strain and treatment using the `auc()` function from `gcplyr`.

5. **Export:**  
   Writes cleaned and combined data to `combined_data_A.csv` and `combined_data_B.csv`.

---

## Visualization

- **Growth Curves:**  
  Plots mean OD600 over time for each strain and treatment, faceted by strain.
- **AUC Annotation:**  
  Annotates each facet with the calculated AUC value for both treatments.
- **Combined Plots:**  
  Uses `ggpubr::ggarrange()` or `patchwork` to display Set A and Set B plots side by side with a shared legend.

---

## Usage

1. **Place your raw CSV files** in the `Growth_curve_IDE_5` folder, named as `A_0.csv` to `A_7.csv` and `B_0.csv` to `B_7.csv`.
2. **Run the R script** (`growth_curve_analysis.R`) in your R environment.
3. **View the output plots** in your R plotting window or save them as images if desired.
4. **Check the combined CSV files** (`combined_data_A.csv`, `combined_data_B.csv`) for processed data.

---

## Troubleshooting

- **Cannot push to main branch:**  
  Your repository may have branch protection enabled. Create a feature branch and submit a pull request.
- **GPG signing errors:**  
  If you see `gpg: signing failed: No secret key`, either generate a GPG key or disable commit signing with `git config --global commit.gpgsign false`.
- **Data import errors:**  
  Ensure your CSV files are correctly formatted and located in the expected folder.


---

**For questions or contributions, please open an issue or pull request in this repository.**

---
