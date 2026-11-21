# TODO

## Analysis (03_EDA)
- [ ] Build no_hs_rate, unemployment_rate, vacancy_rate with .where(denominator > 0)
- [ ] One correlation table: outcomes vs. all five rates (.loc[outcomes, rate_cols])
- [ ] Decide minimum-denominator cutoff, apply to all rates
- [ ] Check vacancy_rate distribution: are high-vacancy tracts mostly resort/seasonal areas? If so, consider pulling B25004_006E (seasonal units) and excluding them
- [ ] Investigate the 8 tracts with rent burden 1.0 and 100+ computed renters
- [ ] Revisit tract 06071012202 (San Bernardino)
- [ ] Yuba 410.02: 190 of 225 renter households not computed. Cause unverified (Beale AFB is a guess)

## Data / extraction
- [ ] Optionally pull B25070_011E to verify the rent "not computed" gap directly

## Documentation
- [ ] 02_cleaning: disability drop reasoning is inconsistent (drops 4 disability measures, keeps cognition, mobility, selfcare). Drop those too or reword
- [ ] Data dictionary: rent_topcoded row, derived 03_EDA columns, renter_hh_total correction, median_gross_rent 3,500+ note
- [x] README: Data Dictionary section still says it covers ACS only. Update now that PLACES is in

## Housekeeping
- [ ] requirements.txt (pinned, done?), README setup, .gitignore for data/raw and .env

## Later
- [ ] Random forest with county-grouped train/test split, SHAP, circularity caution
