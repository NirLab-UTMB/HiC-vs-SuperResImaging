# Hi-C ↔ Imaging Comparison Pipeline (MATLAB)

![MATLAB](https://img.shields.io/badge/MATLAB-R2021b+-orange)
![Status](https://img.shields.io/badge/status-active-success)
![License](https://img.shields.io/badge/license-academic-blue)
![Field](https://img.shields.io/badge/field-3D%20Genome%20Organization-purple)

MATLAB pipeline for comparing Hi-C contact matrices with imaging-derived chromatin distance/contact matrices.  
Designed for genome architecture studies where imaging resolution must be matched to Hi-C resolution prior to correlation or visualization.

---

## Overview

This repository contains a MATLAB live script that:

- Loads high-resolution Hi-C matrices  
- Bins Hi-C data to match imaging resolution  
- Cleans and formats matrices  
- Generates heatmaps  
- Prepares matrices for correlation analyses  
- Enables direct comparison between Hi-C and imaging datasets  

Typical use case:  
Comparing chromatin tracing data with Hi-C contact maps.

Notes:
Use Juicebox (https://github.com/aidenlab/Juicebox.git) to pull the HiC map of choice and convert it into a csv for input for this script

---

## Repository Structure

repo/
│
├── HiC_comparison_Imaging-2.mlx    Main MATLAB live script  
├── README.md                       Documentation  

---

## Requirements

### Software
- MATLAB R2021b or newer recommended  
- Live Script support  
- Statistics functions  
- Basic plotting tools  

### MATLAB Path Dependencies
This script uses a custom colormap:

wrcmap

Add to path if needed:
addpath('path_to_colormap')

---

## Input Data Format

### Hi-C Matrix
- CSV format  
- Square matrix  
- Optional coordinate labels in first row  
- Numeric values elsewhere  

Example:
filename = 'HiC_data.csv';
rawData = readmatrix(filename);

---

## Workflow

### 1. Load Hi-C Matrix
rawData = readmatrix(filename);
hic_1kb = rawData(2:end, :);

### 2. Trim Matrix
Ensures matrix dimensions are divisible by bin size.

bin_size = 2;
trim_dim = min_dim - mod(min_dim, bin_size);

### 3. Bin Hi-C Matrix
Matches Hi-C resolution to imaging resolution.

block = hic_1kb(row_range, col_range);
hic_new(i,j) = mean(block(:));

### 4. Visualization
imagesc(hic_new)
colormap(wrcmap)
colorbar

### 5. Hi-C ↔ Imaging Comparison
After binning:
- Import imaging matrix  
- Ensure matching dimensions  
- Compute correlations  
- Generate comparison plots  

---

## Quick Start

1. Clone repo:
git clone 

2. Open MATLAB and navigate to repo:
cd('path_to_repo')

3. Edit paths in script:
filename = 'path_to_hic_matrix.csv';
folderPath = 'output_folder';
bin_size = 2;

4. Run live script section-by-section.

---

## Output

The script generates:
- Binned Hi-C matrices  
- Heatmaps  
- CSV exports  
- Comparison figures  

Saved to:
folderPath/

---

## Customization

Change resolution:
bin_size = 5;

Use pre-binned Hi-C:
Skip binning section and load matrix directly.

---

## Troubleshooting

Matrix not square  
Ensure input Hi-C matrix is square.

Dimension mismatch  
Hi-C and imaging matrices must match after binning.

Missing colormap  
addpath('path_to_wrcmap')

---

## License

Academic use permitted.  
Contact author for redistribution or commercial use.
