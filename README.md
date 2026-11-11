# SDOH_Predictive_Hotspotting_CA
Census-tract level predictive hotspotting model for housing stress and health outcomes in California using XGBoost and SHAP


## Data Dictionary

Source: U.S. Census Bureau, American Community Survey 5-year estimates (2023), California census tracts. One row per tract. Variable labels: https://api.census.gov/data/2023/acs/acs5/variables.html

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
- 140 tracts have median household income capped at $250,001 and are flagged in `income_topcoded` column.
