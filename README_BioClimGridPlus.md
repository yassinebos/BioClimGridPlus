# BioClimGrid+: Scripts for Generating Updated Bioclimatic Variables from CHELSA-W5E5

This repository provides reproducible R scripts for generating **bioclimatic variables (BIO1–BIO19)** from the **CHELSA-W5E5** climate dataset (1987–2016).  
These scripts were developed as part of the paper:

**_BioClimGrid+: Open dataset of updated bioclimatic variables with applications in species distribution modelling and digital soil mapping._**

---

## 📘 Overview

The provided scripts allow users to:

1. Download monthly **precipitation** and **temperature** (tasmin, tasmax) data from the CHELSA-W5E5 repository (ISIMIP).  
2. Crop and mask the data to a user-defined **Area of Interest (AOI)**.  
3. Convert daily NetCDF files into monthly GeoTIFFs.  
4. Generate the **19 standard bioclimatic variables** (BIO1–BIO19) using the `terra::biovars()` function.  

The workflow is modular — users can process precipitation and temperature separately, then compute all 19 bioclimatic variables for any selected period.

---

## ⚙️ Requirements

Install and load the following R packages before running the scripts:

```r
install.packages(c("terra", "sf", "httr", "ncdf4"))
```

Then load them in your script:

```r
library(terra)
library(sf)
library(httr)
library(ncdf4)
```

---

## 🚀 How to Use

To run the scripts, edit the **user settings** at the top of the code.  
Only four parameters need to be changed:

```r
download_dir <- "C:/path/to/output_folder"          # Output directory for all downloaded and processed files
aoi_boundary_path <- file.path(download_dir, "AOI.shp")   # Path to AOI shapefile (must be in EPSG:4326)
years_to_process <- c(1987:2016)                    # Years to process (example: 1987–2016)
VAR <- "tasmin"                                     # Variable to download: "tasmin" or "tasmax"
```

### Notes:
- The **AOI shapefile** must exist and use the **WGS84 (EPSG:4326)** coordinate system.  
- The script automatically:
  - Downloads monthly NetCDF files from the **ISIMIP (CHELSA-W5E5)** server.  
  - Crops and masks data to your AOI.  
  - Converts daily values into monthly GeoTIFFs.  
  - Deletes intermediate files after processing.  

Each processed file is saved with the following format:

```
precip_YYYYMM.tif
tasmin_YYYYMM.tif
tasmax_YYYYMM.tif
```

---

## 📂 Output Description

The full workflow produces the following outputs:

- **Monthly GeoTIFFs** of precipitation and temperature.  
- **BIO1–BIO19** layers generated from monthly data using `terra::biovars()`.  
- Each bioclimatic variable is saved as an individual `.tif` file inside the folder:

```
/BIO_variables/
```

Example output filenames:

```
BIO_01_2015.tif
BIO_02_2015.tif
...
BIO_19_2015.tif
```

---

## 🧭 Directory Structure

Example of recommended folder organization:

```
BioClimGridPlus/
│
├── scripts/
│   ├── download_precip.R
│   ├── download_tasmin.R
│   ├── download_tasmax.R
│   └── generate_biovars.R
│
├── data/
│   ├── AOI.shp
│   ├── Prec/
│   ├── Tmin/
│   ├── Tmax/
│   └── BIO_variables/
│
└── README.md
```

---

## 🧪 Validation

In the associated paper, BioClimGrid+ was validated using Moroccan meteorological stations (1987–2016).  
The dataset showed strong agreement with observed temperature (r ≥ 0.91) and precipitation (r up to 0.96), confirming its suitability for use in **species distribution** and **digital soil mapping** applications.

---

## 🔍 Citation

If you use these scripts or the generated data, please cite:

> **Bouslihim, Y. (2025).**  
> *BioClimGrid+: Open dataset of updated bioclimatic variables with applications in species distribution modelling and digital soil mapping.*

---

## 🌍 License

This repository is released under the **MIT License**.  
You are free to use, modify, and share the code with proper attribution.

---

## 📬 Contact

For any questions, suggestions, or collaborations, please contact:  

📧 **yassine.bouslihim@gmail.com**  
📧 **yassine.bouslihim@inra.ma**
