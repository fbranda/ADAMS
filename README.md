# African Disease Analysis and Monitoring System (ADAMS)

## Overview

The African Disease Analysis and Monitoring System (ADAMS) is a comprehensive tool designed for analyzing and visualizing disease outbreaks across Africa. This system helps public health officials, researchers, and policymakers understand disease patterns, track outbreak trends, and identify high-risk areas. ADAMS leverages data analysis and geospatial visualization to provide actionable insights into disease distribution and risk levels.

## Features

- **Data Ingestion**: Import and manage disease case data, including suspected, confirmed, and total cases.
- **Risk Assessment**: Calculate and visualize disease risk at a provincial level using various metrics.
- **Geospatial Mapping**: Display disease data on interactive maps to identify high-risk areas and trends.
- **Trend Analysis**: Analyze trends over time to monitor the evolution of disease outbreaks.
- **Reporting**: Generate detailed reports and visualizations for stakeholders.

## Data collection and management
ADAMS utilizes a structured approach to collect and manage disease outbreak data to ensure comprehensive and up-to-date analysis. Here’s an overview of how data is collected and processed:

1. **Data Health Bulletins**: The system receives disease case data from various reporting mechanisms, including reports from authoritative health organizations such as the African Centers for Disease Control and Prevention (Africa CDC) and the World Health Organization (WHO). Data are typically provided in formats such as PDF. The ingestion process includes parsing and mapping the data to the ADAMS schema to ensure consistency (https://github.com/fbranda/ADAMS/blob/main/data-structure-ADAMS.md).

2. **Geospatial data**: Administrative boundaries and geographic features are incorporated using shapefiles or GeoJSON formats. These files define the spatial extent of regions such as provinces or districts, allowing precise mapping of disease data. Geospatial data come from official geographic information system (GIS) databases and national mapping agencies.


## Data processing pipeline
1. **Data import and normalization**: Data import routines are implemented to handle various file formats and ensure normalization of data from different sources. The import process includes data validation checks to identify and correct anomalies, missing values, or format inconsistencies.

2. **Data integration**: Case data are merged with geospatial data to align disease statistics with geographic boundaries. This process involves spatial joins and data enrichment, in which case counts are aggregated and linked to specific geographic regions.

3. **Data cleaning and transformation**: A series of data cleaning steps are applied to remove duplicates, correct inaccuracies, and handle missing values. Data transformation routines are used to calculate derived metrics such as incidence rates and case fatality rates (CFRs). This involves normalizing case counts against population data and time periods.

4. **Visualization**: Visualization components include interactive maps and graphs generated using libraries such as `ggplot2` and `sf` in R. Customized scripts and dashboards are developed to present data in an intuitive format, facilitating interpretation and decision making.

5. **Risk analysis and assessment**: Advanced statistical methods and machine learning algorithms can be used to analyze disease trends and assess risk levels. Techniques include time series analysis, spatial clustering, and predictive modeling. 


## Limitations and data considerations
1. **Underreporting and data gaps**: Variability in reporting practices across regions can lead to incomplete datasets. 

2. **Real-time data updates**: Continuous integration of new data is critical to maintain the relevance of the system. Automated workflows and scheduled data retrievals are used to update datasets and ensure the most up-to-date information is available.

3. **Data accuracy and consistency**: To improve data accuracy, ADAMS implements cross-validation procedures in which data from multiple sources are compared and reconciled. Discrepancies are flagged for further review, and data consistency checks are performed to ensure reliable results.

## Accessing and updating data
For reporting data anomalies or suggesting improvements, users can contact Francesco Branda at francesco.branda.contact@gmail.com. Feedback is valuable for maintaining data accuracy and enhancing the functionality of ADAMS.


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
library(geodata)

# Load data
drc_provinces <- gadm(country = "COD", level = 1, path = tempdir())
drc_provinces_sf <- st_as_sf(drc_provinces)
map_for_mpox <- read_csv("https://raw.githubusercontent.com/fbranda/ADAMS/main/surveillance/2024/Mpox/DRC/latest-DRC-by-province.csv")

#Prepare data
drc <- merge(drc_provinces_sf, map_for_mpox, by.x = "NAME_1", by.y = "Province")
drc <- drc %>%
  mutate(case_rate = (TotalCases / Population) * 100000)  

#Prepare data for cases plot
centroids <- st_centroid(drc)
centroids_coords <- st_coordinates(centroids)
centroids <- cbind(centroids, centroids_coords)

# Plot the cases map
ggplot(drc) +
  geom_sf(aes(fill = TotalCases)) +
  scale_fill_gradient(low = "lightblue", high = "darkblue", name = "Total Cases") +
  geom_text(aes(x = X, y = Y, label = NAME_1), size = 3, color = "white", data = centroids, check_overlap = TRUE) +
  theme_minimal() +
  ggtitle("Total Cases by Province in DRC") +
  theme(legend.position = "bottom")


#Prepare data for cluster risk plot
drc$IncidenceRate <- (drc$TotalCases / drc$Population) * 100000
drc$CFR <- (drc$Deaths / drc$TotalCases) * 100

# Calculate descriptive statistics
summary(drc$IncidenceRate)
quantile(drc$IncidenceRate, probs = c(0, 0.25, 0.5, 0.75, 1))

breaks <- c(-Inf, 1, 5, 10, 50, 100, 200, Inf)
labels <- c("Very Low", "Low", "Moderate", "High", "Very High", "Extreme", "Outlier")

drc <- drc %>%
  mutate(RiskCategory = cut(IncidenceRate,
                             breaks = breaks,
                             labels = labels,
                             right = FALSE))



# Plot incidence rate map by province
ggplot(drc) +
  geom_sf(aes(fill = RiskCategory)) +
  scale_fill_manual(values = c("Very Low" = "#D0F0C0", "Low" = "#B0E57C", "Moderate" = "#FFFF00", 
                               "High" = "#FF7F50", "Very High" = "#FF4500", "Extreme" = "#FF0000", "Outlier" = "#8B0000"),
                    name = "Risk Category") +
  geom_text(aes(x = X, y = Y, label = NAME_1), size = 3, color = "white", data = centroids, check_overlap = TRUE) +
  theme_minimal() +
  ggtitle("Disease Risk by Province in DRC") +
  theme(legend.position = "bottom")


# Optional: display data in a table.
drc %>%
  arrange(desc(RiskCategory)) %>%
  select(NAME_1, TotalCases, IncidenceRate, RiskCategory)

