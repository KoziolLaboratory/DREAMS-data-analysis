# DREAMS Data Analysis Pipeline

## Overview

DREAMS (**DNA RNA Elements Areal Mass Spectrometry**) is a spatial mass spectrometry–based analytical approach developed to characterize the spatial distribution of **free DNA and RNA modifications** across tissue sections, enabling spatial profiling of epigenetic and epitranscriptomic landscapes.

This repository contains the core analysis scripts and reference files used for DREAMS data processing and downstream analyses, including:

- preprocessing of mass spectrometry imaging (MSI) raw data
- extraction of modification signals based on reference m/z annotations
- intensity normalization across tissue sections
- sample merging and technical replicate integration
- region-specific modification analysis
- statistical analysis and data visualization

---

## Project Background

DNA and RNA modifications play essential roles in regulating gene expression and RNA processing and are fundamental to maintaining cellular functions. However, the spatial organization of these modifications within biological tissues remains poorly understood.

To address this challenge, we developed DREAMS (DNA RNA Elements Areal Mass Spectrometry), a spatial mass spectrometry framework designed to directly detect and characterize the spatial distribution of free nucleic acid modifications in tissue sections.

Using a **Tet1 knockout mouse brain model**, DREAMS revealed previously unrecognized regulatory roles of TET enzymes in modulating diverse nucleic acid modifications. Notably, this approach uncovered spatially dependent regulatory patterns, including the region-specific modulation of **N1-methyladenosine (m1A)** in RNA by TET1.

This analytical framework provides a new technical and biological perspective for investigating the spatial epigenetic and epitranscriptomic regulation of the brain.

---

## Repository Structure

```text
.
├── KoziolLab_MSdata_scripts.R
│   Main analysis workflow for DREAMS MSI data

├── MS_Modifications.R
│   Core functions for preprocessing, normalization, statistical analysis, and visualization

├── Modification_reference_Pos-dopamine.csv
│   Reference m/z annotation file for dopamine-related modifications in positive ion mode

├── Modification_reference_Pos-nucleoside tide-final.csv
│   Reference annotation file for nucleoside modifications in positive ion mode

├── Modification_reference_Neg-nucleoside tide-final.csv
│   Reference annotation file for nucleoside modifications in negative ion mode

├── Modification_reference_Neg-cholesterol sulfate glutamate glutamine.csv
│   Reference annotation file for selected compounds in negative ion mode

├── names.csv
│   Reference table for standardized modification nomenclature
```

---

## Requirements

This analysis pipeline is implemented in **R**.

Recommended environment:

- R >= 4.1

Required R packages:

```r
tidyverse
readxl
tools
MetaboAnalystR
pls
janitor
ggrepel
openxlsx
ggpubr
rstudioapi
```

Install missing dependencies with:

```r
install.packages(c(
  "tidyverse",
  "readxl",
  "tools",
  "pls",
  "janitor",
  "ggrepel",
  "openxlsx",
  "ggpubr",
  "rstudioapi"
))
```

Install MetaboAnalystR:

```r
if (!requireNamespace("BiocManager", quietly = TRUE))
    install.packages("BiocManager")

BiocManager::install("MetaboAnalystR")
```

---

## Main Functions

The core functions implemented in `MS_Modifications.R` include:

| Function | Description |
|---------|-------------|
| `GenrateExcelforMSdata()` | Generate Excel templates for organizing MSI raw data |
| `CalculateModificationIntensity()` | Extract modification signal intensities based on reference m/z annotations |
| `MergeModificationIntensity()` | Merge modification intensity data across samples |
| `NormalizationIntensitySlides()` | Normalize signal intensities across tissue sections |
| `MergeTechnicalReplicates()` | Merge technical replicate datasets |
| `PickBrainRegion()` | Extract region-specific datasets |
| `volcano_plotting()` | Generate volcano plots |
| `T_Anavo_plotting()` | Perform statistical comparison and visualization |
| `RunMetaboAnalystR()` | Run downstream metabolomics analysis using MetaboAnalystR |
| `BoxModification()` | Generate boxplots for modification signal visualization |

---

## Usage

Load the core functions:

```r
source("MS_Modifications.R")
```

Run the main analysis workflow:

```r
source("KoziolLab_MSdata_scripts.R")
```

A typical analysis workflow includes:

### 1. Generate data templates

```r
GenrateExcelforMSdata(
  SamplesNames = c("Sample1", "Sample2"),
  BrainRegionNames = c("cortex", "hippocampus"),
  SectionNames = c("01", "02")
)
```

### 2. Extract modification signal intensities

```r
CalculateModificationIntensity(
  MSFilePath = "rawdata/",
  ModificationReferenceFile = "Modification_reference_Pos.csv"
)
```

### 3. Merge sample data

```r
MergeModificationIntensity(
  CSVPath = "processed_data/"
)
```

### 4. Normalize data

```r
NormalizationIntensitySlides(
  MergeModificationIntensityFile = "merged.csv",
  SectionIndex = c("-01", "-02", "-03")
)
```

---

## Input Data Requirements

Required input files include:

- MSI raw signal intensity files
- modification reference annotation files
- modification nomenclature standardization files

Reference annotation files should generally contain:

- modification names
- corresponding m/z values
- annotation metadata

---

## Output

The analysis pipeline generates:

- modification signal intensity matrices
- normalized datasets
- merged sample-level result tables
- statistical analysis outputs
- visualization figures

---

## Contact
For questions, bug reports, or collaboration inquiries, please open an issue in this repository.

---
## LICENSE
This project is covered under the MIT License.

