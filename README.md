# DREAMS Data Analysis

## Overview

DREAMS (**DNA RNA Elements Areal Mass Spectrometry**) is a spatial mass spectrometry–based approach developed to profile nucleic acid modifications across tissue sections, enabling spatial characterization of epigenetic and epitranscriptomic landscapes.

This repository contains the analysis scripts and reference files used for DREAMS data processing and downstream analysis, including:

- preprocessing of mass spectrometry imaging (MSI) raw data
- modification signal extraction based on reference m/z annotations
- intensity normalization across tissue sections
- sample merging and technical replicate integration
- region-specific modification analysis
- statistical testing and visualization

DREAMS was developed to investigate the spatial distribution of DNA and RNA modifications in biological tissues, with applications in studying epigenetic regulation, RNA processing, and enzyme-mediated nucleic acid modification dynamics.

---

## Project Background

DNA and RNA modifications play essential roles in regulating gene expression and RNA processing, yet their spatial organization within tissues remains poorly understood.

To address this, we developed DREAMS (DNA RNA Elements Areal Mass Spectrometry), a spatial mass spectrometry framework for profiling nucleic acid modifications directly in tissue sections.

Using DREAMS in mouse brain models with **Tet1, Tet2, and Tet3 deletions**, we identified previously unrecognized regulatory roles of TET enzymes in modulating diverse nucleic acid modifications. Notably, DREAMS revealed spatially dependent regulation, including TET1-associated modulation of **N1-methyladenosine (m1A)** in RNA.

This framework provides a spatially resolved view of the epigenetic and epitranscriptomic landscape in the brain.

---

## Repository Structure

```text
.
├── KoziolLab_MSdata_scripts.R
│   Main analysis workflow for DREAMS MSI data

├── MS_Modifications.R
│   Core functions for preprocessing, normalization, statistical analysis, and visualization

├── Modification_reference_Pos-dopamine.csv
│   Reference m/z annotations for positive ion dopamine-related modifications

├── Modification_reference_Pos-nucleoside tide-final.csv
│   Reference m/z annotations for positive ion nucleoside modifications

├── Modification_reference_Neg-nucleoside tide-final.csv
│   Reference m/z annotations for negative ion nucleoside modifications

├── Modification_reference_Neg-cholesterol sulfate glutamate glutamine.csv
│   Reference annotations for selected negative ion compounds

├── names.csv
│   Reference table for standardizing modification nomenclature
```

---

## Requirements

This pipeline is implemented in **R**.

Recommended environment:

- R >= 4.1

Required packages:

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

Install missing packages with:

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

For MetaboAnalystR:

```r
if (!requireNamespace("BiocManager", quietly = TRUE))
    install.packages("BiocManager")

BiocManager::install("MetaboAnalystR")
```

---

## Main Functions

The core functions implemented in `MS_Modifications.R` include:

| Function | Description |
|--------|-------------|
| `GenrateExcelforMSdata()` | Generate Excel templates for MSI raw data organization |
| `CalculateModificationIntensity()` | Extract modification intensities based on reference m/z annotations |
| `MergeModificationIntensity()` | Merge modification signals across samples |
| `NormalizationIntensitySlides()` | Normalize intensity values across slides |
| `MergeTechnicalReplicates()` | Merge technical replicates |
| `PickBrainRegion()` | Select region-specific datasets |
| `volcano_plotting()` | Generate volcano plots |
| `T_Anavo_plotting()` | Statistical comparison visualization |
| `RunMetaboAnalystR()` | Metabolomics downstream analysis |
| `BoxModification()` | Boxplot visualization for modification signals |

---

## Usage

Load the analysis functions:

```r
source("MS_Modifications.R")
```

Run the main workflow:

```r
source("KoziolLab_MSdata_scripts.R")
```

Typical workflow:

### 1. Generate data templates

```r
GenrateExcelforMSdata(
  SamplesNames = c("Sample1", "Sample2"),
  BrainRegionNames = c("cortex", "hippocampus"),
  SectionNames = c("01", "02")
)
```

### 2. Extract modification intensities

```r
CalculateModificationIntensity(
  MSFilePath = "rawdata/",
  ModificationReferenceFile = "Modification_reference_Pos.csv"
)
```

### 3. Merge samples

```r
MergeModificationIntensity(
  CSVPath = "processed_data/"
)
```

### 4. Normalize intensities

```r
NormalizationIntensitySlides(
  MergeModificationIntensityFile = "merged.csv",
  SectionIndex = c("-01", "-02", "-03")
)
```

---

## Input Data

Expected input data include:

- MSI-derived raw signal intensity files
- modification reference annotation tables
- modification nomenclature mapping files

Reference tables should contain:

- modification names
- m/z values
- annotation metadata

---

## Output

The pipeline generates:

- processed modification intensity matrices
- normalized datasets
- merged sample-level tables
- statistical comparison outputs
- publication-ready visualizations

---

## Citation

If you use DREAMS or this analysis pipeline in your work, please cite the associated publication.

---

## Contact

For questions, bug reports, or collaboration inquiries, please open an issue in this repository.
