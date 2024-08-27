# African Disease Analysis and Monitoring System (ADAMS)

## Overview

The African Disease Analysis and Monitoring System (ADAMS) is a comprehensive tool designed for analyzing and visualizing disease outbreaks across Africa. This system helps public health officials, researchers, and policymakers understand disease patterns, track outbreak trends, and identify high-risk areas. ADAMS leverages data analysis and geospatial visualization to provide actionable insights into disease distribution and risk levels.

## Features

- **Data Ingestion**: Import and manage disease case data, including suspected, confirmed, and total cases.
- **Risk Assessment**: Calculate and visualize disease risk at a provincial level using various metrics.
- **Geospatial Mapping**: Display disease data on interactive maps to identify high-risk areas and trends.
- **Trend Analysis**: Analyze trends over time to monitor the evolution of disease outbreaks.
- **Reporting**: Generate detailed reports and visualizations for stakeholders.

## Installation

### Prerequisites

- R (version 4.0 or higher)
- RStudio (optional but recommended)
- Required R packages: `sf`, `ggplot2`, `dplyr`

### Setup

1. **Install R and RStudio**: Follow the instructions on the [CRAN website](https://cran.r-project.org/) and the [RStudio website](https://rstudio.com/products/rstudio/download/).

2. **Install Required Packages**: Open R or RStudio and install the required packages by running the following commands:
    ```r
    install.packages(c("sf", "ggplot2", "dplyr"))
    ```

3. **Download the Repository**: Clone or download this repository to your local machine.
    ```bash
    git clone https://github.com/yourusername/adams.git
    ```

4. **Load the Project**: Open the project in RStudio or run the scripts from the command line.

## Usage

1. **Load Data**: Ensure you have the required datasets, including:
   - Disease case data (CSV or other formats)
   - Shapefiles for geographical boundaries

2. **Run Analysis**:
   - Load the datasets into R.
   - Perform data cleaning and transformation as needed.
   - Calculate metrics such as incidence rates and cluster risk.

3. **Generate Visualizations**:
   - Create visualizations using `ggplot2` for data analysis and risk assessment.
   - Generate maps with `sf` to visualize disease distribution and risk levels.

4. **View Results**:
   - Review the output maps and reports to understand disease patterns and risks.

## Example

Here is an example of how to calculate and visualize cluster risk:

```r
# Load necessary libraries
library(ggplot2)
library(sf)
library(dplyr)

# Load data
drc <- st_read("path_to_shapefile/drc_provinces.shp")
province_data <- read.csv("path_to_data/province_data.csv")

# Prepare data
province_data <- province_data %>%
  mutate(ClusterRisk = IncidenzaTotale * (ConfirmedCases / TotalCases))

drc <- drc %>%
  left_join(province_data, by = "NAME_1")

# Plot the map
ggplot(drc) +
  geom_sf(aes(fill = ClusterRisk)) +
  scale_fill_gradient(low = "lightblue", high = "darkblue", name = "Cluster Risk") +
  theme_minimal() +
  ggtitle("Cluster Risk by Province in DRC") +
  theme(legend.position = "bottom")
