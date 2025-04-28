

# Growth Curve Data Analysis

This repository contains data and scripts used to 

1.analyse the growth curve of strains of Xylella fastidiosa by growing it in a standard media and media amended with 2mM Ca.The experiment setup is done on a 96 well plate assay. The growth is recorded every 24 hour, one time point per day.
.
---

## Table of Contents

- [Project Overview](#project-overview)
- [File Tree](#directory structure)
- [Data](#Raw and procesceed Data)
- [Growth_Curve_IDE_5](#Raw data from plate reader)
- [Data_Processing_Plots_files](#Auto generated file and images)
- [Figures](#Manuscript ready figures)
- [Requirements](#requirements)
- [Data Processing Workflow](#data-processing-workflow)
- [Visualization](#visualization)
- [Usage](#usage)
- [Troubleshooting](#troubleshooting)


---

## Project Overview


- Reads and processes raw CSV data for multiple days and two datasets (Set A and Set B).
- Normalizes OD600 readings by subtracting blank controls.
- Calculates mean OD600 values and AUC for each strain and treatment.
- Produces faceted plots with growth curves and annotated AUC values.

---

## Folder Structure

```
.
├── Data
│   ├── Processed_data
│   │   ├── combined_data.csv
│   │   ├── combined_data_A.csv
│   │   └── combined_data_B.csv
│   └── Raw_data
│       ├── A_0.csv
│       ├── A_1.csv
│       ├── A_2.csv
│       ├── A_3.csv
│       ├── A_4.csv
│       ├── A_5.csv
│       ├── A_6.csv
│       ├── A_7.csv
│       ├── B_0.csv
│       ├── B_1.csv
│       ├── B_1.xlsx
│       ├── B_2.csv
│       ├── B_2.xlsx
│       ├── B_3.csv
│       ├── B_3.xlsx
│       ├── B_4.csv
│       ├── B_4.xlsx
│       ├── B_5.csv
│       ├── B_5.xlsx
│       ├── B_6.csv
│       ├── B_6.xlsx
│       ├── B_7.csv
│       ├── B_7.xlsx
│       ├── B_bio.xlsx
│       ├── B_day_0.xlsx
│       └── B_Plk.xlsx
├── Data_Processing_Plots.md
├── Data_processing_plots.pdf
├── Data_Processing_Plots.R
├── Data_Processing_Plots.Rmd
├── Data_Processing_Plots_files
│   └── figure-gfm
│       ├── unnamed-chunk-10-1.png
│       ├── unnamed-chunk-11-1.png
│       ├── unnamed-chunk-11-2.png
│       └── unnamed-chunk-7-1.png
├── Figures
│   ├── Rplot01_GC.tiff
│   └── Rplot_AUC.tiff
├── file_tree.txt
├── Final_Project.Rproj
├── Growth_curve_IDE_5
│   ├── A_0.csv
│   ├── A_1.csv
│   ├── A_2.csv
│   ├── A_3.csv
│   ├── A_4.csv
│   ├── A_5.csv
│   ├── A_6.csv
│   ├── A_7.csv
│   ├── B_0.csv
│   ├── B_1.csv
│   ├── B_1.xlsx
│   ├── B_2.csv
│   ├── B_2.xlsx
│   ├── B_3.csv
│   ├── B_3.xlsx
│   ├── B_4.csv
│   ├── B_4.xlsx
│   ├── B_5.csv
│   ├── B_5.xlsx
│   ├── B_6.csv
│   ├── B_6.xlsx
│   ├── B_7.csv
│   ├── B_7.xlsx
│   ├── B_bio.xlsx
│   ├── B_day_0.xlsx
│   └── B_Plk.xlsx
└── README.md
```
---
###Growth_Curve_IDE_5

This contains the data generated from the plate reader. As my experiment has three replicate plates of each set. The plates were read is ascending order and their reading are in blocks, the first block is the first plate and so on. 

In one 96 well plate, the first row A is used as a blank for PD2 and row H is used for PD2 + Calcium. The remaining rows B to G have 6 strains of bacteria. This experiment 
 I have used two sets of strains namely strain A and strain B
---

---
##Data

Data contains of processed files and raw files. The processed files have  the OD reading corrected by subtracting from their respective blanks. Combined_data.csv is the file generated from processing and cleaning the plate reader data ssigning the with values of day, plate and treatment along with their both sets and name of the strains.

---

---
##Data_Processing_Plots_files

There are the files automatically generated while knitting the Markdown and contains of images generated while running the script.

---

---
##Figures

The manuscript ready figures generated through the plotting part of the code.The figures contain Area Under Growth Curve and a Normal growth Curve

----

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
