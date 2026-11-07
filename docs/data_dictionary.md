# Data Dictionary - Steady Steps Falls-Prevention Programme

12-week exercise class for older adults at 3 community centres. File: `falls_prevention_raw.csv` (200 rows).

| Column | Description | Valid values / range |
|---|---|---|
| participant_id | Participant identifier | `P001` to `P200` (letter P + 3 digits) |
| centre | Community centre attended | `A`, `B`, `C` |
| age_group | Age group as of 2026-01-01 | `65-74`, `75-84` |
| sex | Sex of participant | `F`, `M` |
| date_of_birth | Date of birth | `YYYY-MM-DD`; must give an age on 2026-01-01 that matches `age_group` (65-74 or 75-84) |
| enrolled | Enrolled in the Steady Steps class | `Yes`, `No` (No = comparison group) |
| balance_score | Balance score | Numeric, 0 to 10 inclusive, one decimal place; higher = better balance |
