
# Data Dictionary

This dictionary describes `sdoh_merged_CA.csv`, the merged tract-level file produced by `02_cleaning`. It has 9,070 California census tracts (one row per tract) and 75 columns. The ACS columns come first, followed by the CDC PLACES health measures. The two sources are joined on `GEOID`.

Sources:
- U.S. Census Bureau, American Community Survey 5-year estimates (2023). Variable labels: https://api.census.gov/data/2023/acs/acs5/variables.html
- CDC PLACES, census tract data, 2025 release (dataset `cwsq-ngmh`). Methodology: https://www.cdc.gov/places/methodology/index.html


| Column | Census code | Group | Description | Unit |
|---|---|---|---|---|
| state | n/a | Identifier | State FIPS code (`06` for California), stored as a string | text |
| county | n/a | Identifier | County FIPS code, stored as a string | text |
| tract | n/a | Identifier | Tract code, stored as a string | text |
| GEOID | n/a | Identifier | `state` + `county` + `tract`, 11 characters, unique per tract | text |
| NAME | n/a | Identifier | Tract name, county, and state (for example, "Census Tract 4001; Alameda County; California") | text |
| income_topcoded | n/a | Income / poverty | True if median_hh_income equals the Census cap of 250001 (the true median is at least that high) | boolean |
| median_hh_income | B19013_001E | Income / poverty | Median household income | dollars |
| poverty_status_total | B17001_001E | Income / poverty | People for whom poverty status was determined (denominator for poverty rate) | count |
| pop_below_poverty | B17001_002E | Income / poverty | People below the poverty level | count |
| renter_hh_total | B25070_001E | Rent burden | Renter households (denominator for rent burden columns) | count |
| rent_burden_lt10 | B25070_002E | Rent burden | Rent is less than 10% of income | count |
| rent_burden_10_15 | B25070_003E | Rent burden | Rent is 10.0 to 14.9% of income | count |
| rent_burden_15_20 | B25070_004E | Rent burden | Rent is 15.0 to 19.9% of income | count |
| rent_burden_20_25 | B25070_005E | Rent burden | Rent is 20.0 to 24.9% of income | count |
| rent_burden_25_30 | B25070_006E | Rent burden | Rent is 25.0 to 29.9% of income | count |
| rent_burden_30_35 | B25070_007E | Rent burden | Rent is 30.0 to 34.9% of income | count |
| rent_burden_35_40 | B25070_008E | Rent burden | Rent is 35.0 to 39.9% of income | count |
| rent_burden_40_50 | B25070_009E | Rent burden | Rent is 40.0 to 49.9% of income | count |
| rent_burden_50plus | B25070_010E | Rent burden | Rent is 50% or more of income | count |
| edu_total_25plus | B15003_001E | Education | Adults 25 and over (denominator) | count |
| edu_no_school | B15003_002E | Education | Adults 25+ with no schooling completed | count |
| edu_nursery | B15003_003E | Education | Adults 25+ whose highest level is nursery school | count |
| edu_kindergarten | B15003_004E | Education | Adults 25+ whose highest level is kindergarten | count |
| edu_grade_1 | B15003_005E | Education | Adults 25+ whose highest level is 1st grade | count |
| edu_grade_2 | B15003_006E | Education | Adults 25+ whose highest level is 2nd grade | count |
| edu_grade_3 | B15003_007E | Education | Adults 25+ whose highest level is 3rd grade | count |
| edu_grade_4 | B15003_008E | Education | Adults 25+ whose highest level is 4th grade | count |
| edu_grade_5 | B15003_009E | Education | Adults 25+ whose highest level is 5th grade | count |
| edu_grade_6 | B15003_010E | Education | Adults 25+ whose highest level is 6th grade | count |
| edu_grade_7 | B15003_011E | Education | Adults 25+ whose highest level is 7th grade | count |
| edu_grade_8 | B15003_012E | Education | Adults 25+ whose highest level is 8th grade | count |
| edu_grade_9 | B15003_013E | Education | Adults 25+ whose highest level is 9th grade | count |
| edu_grade_10 | B15003_014E | Education | Adults 25+ whose highest level is 10th grade | count |
| edu_grade_11 | B15003_015E | Education | Adults 25+ whose highest level is 11th grade | count |
| edu_12th_no_diploma | B15003_016E | Education | Adults 25+ with 12th grade, no diploma | count |
| labor_force | B23025_003E | Employment | Civilian labor force | count |
| unemployed | B23025_005E | Employment | Unemployed civilians in the labor force | count |
| housing_units_total | B25002_001E | Housing | Total housing units | count |
| housing_units_vacant | B25002_003E | Housing | Vacant housing units | count |
| occupied_units_total | B25003_001E | Housing | Occupied housing units (tenure universe) | count |
| renter_occupied_units | B25003_003E | Housing | Renter-occupied housing units | count |
| median_gross_rent | B25064_001E | Housing | Median gross rent | dollars |
| total_pop | B01003_001E | Population | Total population | count |
| median_age | B01002_001E | Population | Median age | years |

**Notes**

- `edu_no_school` through `edu_12th_no_diploma` together make up adults 25+ with less than a high school diploma.
- Census placeholder values such as `-666666666` mean "not available" and are replaced with missing values during cleaning: 126 tracts for median income, 301 for median rent, and 51 for median age.
- All estimates carry a margin of error that is not included in this file.
- 140 tracts have median household income capped at $250,001 and are flagged in the `income_topcoded` column.

## CDC PLACES health measures

Source: CDC PLACES, census tract data, 2025 release (dataset `cwsq-ngmh`). Values are model-based estimates of crude prevalence (not age-adjusted), mostly from 2023 BRFSS data. Column names are the lowercase PLACES `measureid`. Ten of the 40 measures are dropped in `02_cleaning` (see that notebook for reasons).

| Column | PLACES ID | Category | Description | Unit |
|---|---|---|---|---|
| bphigh | BPHIGH | Health Outcomes | High blood pressure among adults | percent of adults |
| cancer | CANCER | Health Outcomes | Cancer (non-skin) or melanoma among adults | percent of adults |
| casthma | CASTHMA | Health Outcomes | Current asthma among adults | percent of adults |
| chd | CHD | Health Outcomes | Coronary heart disease among adults | percent of adults |
| copd | COPD | Health Outcomes | Chronic obstructive pulmonary disease among adults | percent of adults |
| depression | DEPRESSION | Health Outcomes | Depression among adults | percent of adults |
| diabetes | DIABETES | Health Outcomes | Diagnosed diabetes among adults | percent of adults |
| obesity | OBESITY | Health Outcomes | Obesity among adults | percent of adults |
| stroke | STROKE | Health Outcomes | Stroke among adults | percent of adults |
| teethlost | TEETHLOST | Health Outcomes | All teeth lost among adults aged 65 and over | percent of adults 65+ |
| binge | BINGE | Health Risk Behaviors | Binge drinking among adults | percent of adults |
| csmoking | CSMOKING | Health Risk Behaviors | Current cigarette smoking among adults | percent of adults |
| lpa | LPA | Health Risk Behaviors | No leisure-time physical activity among adults | percent of adults |
| sleep | SLEEP | Health Risk Behaviors | Short sleep duration among adults | percent of adults |
| access2 | ACCESS2 | Prevention | Current lack of health insurance among adults aged 18-64 | percent of adults 18-64 |
| checkup | CHECKUP | Prevention | Routine doctor checkup within the past year among adults | percent of adults |
| dental | DENTAL | Prevention | Visited a dentist or dental clinic in the past year among adults | percent of adults |
| ghlth | GHLTH | Health Status | Fair or poor self-rated health among adults | percent of adults |
| mhlth | MHLTH | Health Status | Frequent mental distress among adults | percent of adults |
| phlth | PHLTH | Health Status | Frequent physical distress among adults | percent of adults |
| cognition | COGNITION | Disability | Cognitive disability among adults | percent of adults |
| mobility | MOBILITY | Disability | Mobility disability among adults | percent of adults |
| selfcare | SELFCARE | Disability | Self-care disability among adults | percent of adults |
| emotionspt | EMOTIONSPT | Health-Related Social Needs | Lack of social and emotional support among adults | percent of adults |
| foodinsecu | FOODINSECU | Health-Related Social Needs | Food insecurity in the past 12 months among adults | percent of adults |
| foodstamp | FOODSTAMP | Health-Related Social Needs | Received food stamps in the past 12 months among adults | percent of adults |
| housinsecu | HOUSINSECU | Health-Related Social Needs | Housing insecurity in the past 12 months among adults | percent of adults |
| lacktrpt | LACKTRPT | Health-Related Social Needs | Lack of reliable transportation in the past 12 months among adults | percent of adults |
| loneliness | LONELINESS | Health-Related Social Needs | Loneliness among adults | percent of adults |
| shututility | SHUTUTILITY | Health-Related Social Needs | Threat of utility shut-off in the past 12 months among adults | percent of adults |

**Notes**

- `teethlost` is missing for 3 tracts (9,067 of 9,070 have values).
- `access2` and `teethlost` use age-restricted populations (18-64 and 65+), so their denominators differ from the other measures.
- The social needs measures stay in the file but are not used as predictors or outcomes.
- `teethlost`, `sleep`, and `dental` use 2022 BRFSS data. All other measures use 2023. (Source: the `year` column in the raw PLACES file.)