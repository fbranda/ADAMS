## ADAMS data structure

# Mpox
**Directory:**  surveillance/yyyy/Mpox (where yyyy is the year of monitoring)<br>
**Name file:** Surveillance-data-mpox-outbreak-yyyy-by-country.csv <br>


| Field name                  | Description                       |Format                       | Example             |
|-----------------------------|-----------------------------------|-------------------------------|---------------------|
| **Source**              | Origin of the information	 | PDF | https://github.com/fbranda/ADAMS/blob/main/bulletins/2023/Africa-CDC-1-23.pdf	|
| **DateOfIssue**         | Date on which the data were published	   | Data (YYYY-MM-DD) | 2024-08-23 	|
| **Country**              | Name of the country where the cases were registered	 | Text | Democratic Republic of the Congo  	|
| **Latitude**       | Latitude of the country where the cases were recorded | Numeric | -3.9416119 	|
| **Longitude**                        |   Longitude of the country where the cases were recorded | Numeric | 11.0375552 	|
| **NewSuspectedCases**                       | New suspected cases reported since the previous bulletin	  | Numeric | 582 	|
| **TotalSuspectedCases**  | Total suspected cases up to the date of publication of the bulletin | Numeric  | 5000	|
| **NewProbableCases**                | New probable cases reported since the previous bulletin	  | Numeric | 10 	|
| **TotalProbableCases**             | Total probable cases up to the date of publication of the bulletin | Numeric  | 100	|
| **NewConfirmedCases**             | New confirmed cases reported since the previous bulletin	  | Numeric | 200 	|
| **TotalConfirmedCases**              | Total confirmed cases up to the date of publication of the bulletin | Numeric  | 500	|
| **TotalActiveCases**              | Total active confirmed cases at the date of publication	 | Numeric  | 385	|
| **NewRecoveredCases**              | New recovered cases since the previous bulletin	 | Numeric  | 30	|
| **TotalRecoveredCases**              | Total recovered cases up to the date of publication	 | Numeric  | 100	|
| **NewConfirmedDeaths**               | New deaths cases reported since the previous bulletin	  | Numeric | 2 	|
| **TotalConfirmedDeaths**              | Total deaths cases up to the date of publication of the bulletin | Numeric  | 15	|
| **CFR**              | Case fatality rate | Numeric | 8.0	|


**Directory:**  surveillance/yyyy/Mpox/DRC (where yyyy is the year of monitoring)<br>
**Name file:** track-outbreak-DRC-yyyy-by-province.csv <br>
| Field name                  | Description                       |Format                       | Example             |
|-----------------------------|-----------------------------------|-------------------------------|---------------------|
| **Source**              | Origin of the information	 | PDF | https://github.com/fbranda/ADAMS/blob/main/bulletins/SITREP/Mpox/SITREP-Mpox-1.pdf	|
| **Week**         | Number of the week of epidemiological surveillance	   | Numeric | 2	|
| **Province**              | Name of the province where the cases were registered	 | Text | Bas-Uele   	|
| **Latitude**       | Latitude of the province where the cases were recorded | Numeric | 3.6682004 	|
| **Longitude**                        |   Longitude of the province where the cases were recorded | Numeric | 22.4296578 	|
| **NewSuspectedCases**                       | New suspected cases reported since the previous bulletin	  | Numeric | 582 	|
| **TotalSuspectedCases**  | Total suspected cases up to the date of publication of the bulletin | Numeric  | 5000	|
| **TotalConfirmedCases**              | Total confirmed cases up to the date of publication of the bulletin | Numeric  | 500	|
| **NewConfirmedDeaths**               | New deaths cases reported since the previous bulletin	  | Numeric | 2 	|
| **TotalConfirmedDeaths**              | Total deaths cases up to the date of publication of the bulletin | Numeric  | 15	|
| **Lethality**              | `NewConfirmedDeaths`/`TotalSuspectedCases` | Numeric | 0.04	|


**Directory:**  surveillance/yyyy/Mpox/DRC (where yyyy is the year of monitoring)<br>
**Name file:** latest-DRC-by-province.csv <br>
| Field name                  | Description                       |Format                       | Example             |
|-----------------------------|-----------------------------------|-------------------------------|---------------------|
| **Source**              | Origin of the information	 | PDF | https://github.com/fbranda/ADAMS/blob/main/bulletins/SITREP/Mpox/SITREP-Mpox-1.pdf	|
| **Province**              | Name of the province where the cases were registered	 | Text | Bas-Uele   	|
| **TotalSuspectedCases**  | Total suspected cases up to the date of publication of the bulletin | Numeric  | 5000	|
| **TotalConfirmedCases**              | Total confirmed cases up to the date of publication of the bulletin | Numeric  | 500	|
| **TotalCases**              | `TotalSuspectedCases` + `TotalConfirmedCases` | Numeric  | 5500	|
| **TotalCasesDeaths**              | Total deaths cases up to the date of publication of the bulletin | Numeric  | 15	|
| **CFR**              | `TotalConfirmedDeaths`/`TotalCases` | Numeric | 0.27	|
| **Population**              | Official population by province (Source: https://www.investindrc.cd/fr/Provinces) | Numeric | 0.27	|








