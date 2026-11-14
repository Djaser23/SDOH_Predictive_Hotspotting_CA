# SDOH_Predictive_Hotspotting_CA

Census-tract analysis of how socioeconomic and housing conditions relate to chronic disease prevalence in California.

**Status:** Data cleaning and merge complete. Analysis in progress.

## Research Question

How well can tract-level socioeconomic and housing measures from the American Community Survey (poverty, education, rent burden, unemployment, housing vacancy) predict modeled prevalence of costly, preventable chronic conditions across California census tracts?

*PLACES values are modeled estimates, so this analysis tests how well ACS measures reproduce those estimates, not measured tract-level health rates.*

## Data Sources

### American Community Survey (ACS)

- **Source:** U.S. Census Bureau, American Community Survey 5-year estimates, 2023 release (2019-2023).
- **Geography:** California census tracts (9,129 tracts).
- **Access:** Census Data API, using the code in `notebooks/01_extraction.ipynb`. A free Census API key is required. Store it as `CENSUS_API_KEY` in a `.env` file at the project root.
- **Content:** 38 variables covering income and poverty, rent burden, educational attainment, employment, housing, and population. Variable codes and definitions are in [data_dictionary.md](data_dictionary.md).
- **Variable reference:** https://api.census.gov/data/2023/acs/acs5/variables.html

### CDC PLACES

- **Source:** CDC PLACES, census tract level, 2025 release (mostly 2023 Behavioral Risk Factor Surveillance System (BRFSS) survey data; five measures use 2022 data).
- **Geography:** California census tracts (9,070 tracts).
- **Access:** CDC data portal (Socrata API, dataset `cwsq-ngmh`), using the code in `notebooks/01_extraction.ipynb`. An app token is optional and only raises rate limits.
- **Content:** 40 health measures (chronic conditions, health behaviors, prevention, disability, health status, and health-related social needs), reported as crude prevalence percentages of adults.
- **Methodology:** https://www.cdc.gov/places/methodology/index.html

### Notes on the data

- PLACES values are modeled estimates, not direct counts. The CDC produces them with a multilevel regression and poststratification model built on BRFSS survey data, with county-level poverty from the ACS among the listed model inputs. Results in this project describe those estimates, not measured tract-level rates.
- The PLACES file contains crude prevalence only, so rates are not age-adjusted. Median age will be included as a covariate in the models as a rough control, which does not fully account for differences in age structure.
- The two datasets are joined on an 11-character GEOID (state + county + tract). The merged file, `sdoh_merged_CA.csv`, covers the 9,070 tracts present in both sources. The 59 ACS tracts with no PLACES data are not included.
- Raw and processed data files are not stored in the repository (`data/raw/` and `data/processed/` are gitignored). Run `notebooks/01_extraction.ipynb` to download the raw ACS and PLACES files, then `notebooks/02_cleaning.ipynb` to produce the cleaned and merged files in `data/processed/` (`acs5_2023_tract_CA_clean.csv` and `sdoh_merged_CA.csv`).

## Data Dictionary

Column definitions, units, and notes on data quality are in [data_dictionary.md](data_dictionary.md). The dictionary currently covers the ACS columns only. PLACES measures will be documented once the final modeling file is built.