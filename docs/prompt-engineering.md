# AI Prompt Engineering of Dataset

## Goal
The goal of the prompt was to generate an artificial dataset that could be used to practice cleaning and stratified analysis of the data in Excel and R.

## Prompt Model
**AI Used:** Claude <br>
**Model Used:** Claude Sonnet 5.5 <br>
**Date Generated:** 2026-11-07 <br>

## Final Prompt
**The signal and errors are chosen by the model and hidden from me until I finish the analysis.**

```
ROLE: You are a public health data simulator creating a synthetic, messy dataset for an analyst portfolio project.

CONTEXT: I am practicing a data cleaning and stratified analysis task. I will clean and analyze the data myself in Excel and R, so I must not know the underlying pattern or the specific data errors in advance.

SCENARIO: A public health unit runs a 12-week "Steady Steps" falls-prevention exercise class for older adults at 3 community centres (A, B, C). Participants are tracked in two age groups: 65-74 and 75-84. Outcome = Balance Score (valid range 0-10, one decimal allowed, higher = better balance).

TASK: Use Python (or R) to generate a CSV of exactly 200 rows with random seed 42. Do not type the data manually. Save the script as generate_data.py and the data as falls_prevention_raw.csv.

COLUMNS: participant_id, centre, age_group, sex, date_of_birth, enrolled, balance_score
- participant_id: P001-P200 format
- centre: A, B, C (roughly even)
- age_group: "65-74" or "75-84" (roughly even)
- sex: F or M (roughly even)
- date_of_birth: must match age_group as of 2026-01-01
- enrolled: Yes (~50%) / No (comparison group)
- balance_score: true values 0-10

HIDDEN SIGNAL (you choose; do NOT reveal it in chat or in the CSV):
- Randomly choose an overall enrolled effect between 0.3 and 0.9 points
- Randomly choose 2 subgroups (by centre, age group, or sex) with a strong benefit
- Randomly choose 1-2 subgroups with negligible or zero benefit
- Add random noise (SD ~1.5), skewed slightly so mean != median
- Keep true scores within 0-10
- Write the chosen signal ONLY inside answer_key.md

INJECT ERRORS (you choose the types and counts; do NOT reveal them in chat or in the CSV):
- Inject 8-12 different realistic data quality problems across the columns, such as: missing values, duplicate IDs, out-of-range scores, non-numeric entries, inconsistent labels or capitalization, extra spaces, mixed date formats, impossible or future dates, and values that contradict other columns
- Choose your own counts for each type (between 3 and 15 rows each)
- Include at least one error type in every column
- Apply errors after generating the clean data
- Spread errors randomly; a row can have more than one error
- Keep the original row order; do not sort

DO NOT:
- Clean, fix, or sort the raw CSV
- Reveal the hidden signal or the injected errors anywhere except answer_key.md
- Hand-type the data
- Describe the signal or errors in your chat reply

OUTPUT 4 FILES:
1. falls_prevention_raw.csv (messy data only)
2. data_dictionary.md (columns, valid values, valid ranges only; no hints about errors)
3. answer_key.md (hidden signal chosen; every injected error listed by type, column, row numbers, and count; true clean-data mean/median/IQR overall and by sex, age group, centre, enrolled, and enrolled-vs-not within each subgroup)
4. generate_data.py (the script, with seed 42)

VERIFY: Confirm the counts in answer_key.md match the CSV. In your chat reply, confirm only that the files were created and the counts match.
```

## Prompt Components
| Component | What it does | Why it's needed |
|---|---|---|
| Role | Sets the model as a data simulator | Stops it from cleaning or analyzing the data |
| Context | Explains the purpose of the project | Helps the model make good choices |
| Scenario | Defines the program, groups, and valid score range | Makes labels realistic and enables stratification |
| Task + seed | Sets exact row count and requires code | Reproducible data, no hand-typed rows |
| Columns | Fixes column names and formats | Keeps Excel and R formulas consistent |
| Hidden signal | Model secretly plants a pattern | Real discovery, no pre-known answer |
| Injected errors | Model chooses and hides data problems | Forces real profiling and cleaning |
| Do not | Blocks unwanted behaviour | Prevents leaks and auto-cleaning |
| Output files | Separates data, dictionary, key, script | Lets me check my work afterward |
| Verify | Self-check before finishing | Catches count mismatches |

## Iteration Log
v1: Chose a falls-prevention scenario to practice stratified analysis on a realistic public health topic <br>
v2: Prompt revealed the answer, so the model now chooses the signal secretly; restructured sections (Columns, Hidden Signal, Inject Errors) to hide the answer <br>
v3: Exact error list was a cleaning checklist, so the model now chooses errors secretly <br>
v4: Added a script file and seed for reproducibility <br>

## Lessons Learned 
1. I learned that specific prompts are better than vague requests and I learned a structure for prompting AI models that provides more reliable results:

| Component | What it does | Lesson |
|---|---|---|
|**Role** | Defines who the model is|Keeps the model on task (simulate data, not analyze it)|
|**Context**| Explains why I need the data|Telling the model I must not know the answer changed how it handled the signal and errors|
|**Scenario/Background** |Gives the situation, variables, and valid ranges|Realistic details make labels and ranges consistent|
|**Task** |One clear action and also giving specific quantities|"200 rows" and "seed 42" make the output measurable and reproducible|
|**Details/Specifications** |Columns and rules|Fixed names and formats keep Excel and R work consistent|
|**Do Not (constraints)** |Blocks unwanted behaviour|Needed to stop the model cleaning the data or revealing the answer|
|**Output Format** | File names and structure| Separate files (data, dictionary, key, script) keep answers hidden until I finish|
|**Examples** | Samples of desired output | Skipped on purpose; I was afraid sample errors would influence the AI and give away the answer|
|**Verify** |Self-check before finishing | New habit for me, it seems like an amazing idea to reduce avoidable mistakes|

2. **Read the prompt before running it, as the person who must not see the answer.** 
    - My first version listed the hidden pattern and exact error counts, which gave away the answer, so I had to regenerate the files a few times.
    - I fixed this by relabelling the specifications into Columns, Hidden Signal, and Inject Errors, so the model chooses the signal and errors and records them only in a file I open when I finish.
    - I learned that checking the prompt first reduces mistakes and avoids wasted regenerations.
  
## Limitations
### AI prompting limitations: 
- A major limitation with the data is that it is AI generated so it may not match real-world patterns.
- Results may vary by model and version.
- The prompt can produce different datasets for different people (I tried to limit this by using a seed).
- The model may not follow every prompt I want exactly as written.

### Potentially study design/analysis limitations to look into in the future: 
- There is no score before and after, so I will not be able to measure change over time.
- Enrolled vs. not enrolled is not randomized, so groups may differ at baseline.
- Subgroup differences are descriptive only; no significance testing.
- When stratifying data with only 200 samples, there could be groups with small numbers of participants and this would make calculations unstable.
- There may be blank/incorrect data that could affect results that will need to be decided how to clean.

## Conclusion
Structure, exact constraints, and anticipating how the AI might respond made the prompt more reliable. Next, I will clean and analyze the dataset in Excel, then reproduce the work in R.
