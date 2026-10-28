# AI Data Quality Checker

A lightweight, browser-based tool that audits a CSV dataset for data quality issues using Google's Gemini 2.5 Flash model. It produces a health score, a summary of the problems it finds, and a practical suggested fix for each one.

![Screenshot of the Data Quality Analyzer](screenshot.png)

## Why I built it

Over 18 years in performance and MI reporting across local government and financial services, much of my time has gone on finding and fixing data quality problems before figures reach senior stakeholders. Missing values, duplicates, inconsistent formats and outliers cause unreliable reporting and slow down statutory returns.

I built this tool to explore how AI can speed up the first pass of a data quality check. It turns a raw extract into a prioritised list of issues an analyst can act on, so less time is spent hunting for problems and more on fixing them.

## What it does

- **Upload or paste a CSV.** Load a file, or paste rows straight into the preview box.
- **Runs an AI-driven data quality audit.** It checks for:
  - Missing values
  - Duplicate records
  - Inconsistent formatting (dates, codes, text case and so on)
  - Outliers and anomalies
- **Produces a summary dashboard** showing:
  - Total records
  - A data quality health score (0–100%, colour-coded green, amber or red)
  - Total number of issues found
  - An overall cleanliness rating
- **Lists every issue** with its severity (High, Medium or Low), the affected column, a plain-English description and a suggested fix.

## How it works

1. The CSV content is sent to the Gemini 2.5 Flash API with a system prompt instructing the model to act as a data quality engineer.
2. The model must return a fixed JSON structure (a summary plus a list of issues). JSON output is enforced through the API's `responseMimeType` setting, and a low temperature (0.1) keeps results consistent between runs.
3. The page reads the JSON and renders the dashboard and issue list.

## Tech stack

- HTML and vanilla JavaScript (single file, no build step)
- Tailwind CSS (via CDN) for styling
- Google Gemini API (`gemini-2.5-flash`)

## Getting started

1. Get a free Gemini API key from [Google AI Studio](https://aistudio.google.com/).
2. Download `index.html` and open it in any modern browser.
3. Paste your API key into the **Gemini API Key** field.
4. Upload a CSV file or paste CSV data into the preview box.
5. Click **Analyze Dataset**.

## Data privacy and limitations

- **Use only test or anonymised data.** The dataset is sent to Google's Gemini API for analysis. Never upload personal, sensitive or confidential data.
- **Your API key is stored locally** in your browser (`localStorage`) for convenience. It is sent only to Google's API.
- **Best suited to small and medium-sized samples.** Very large files may exceed the model's input limits. A representative sample usually works well.
- **AI output should be reviewed.** Treat the results as a fast first pass, not a replacement for proper validation rules. Counts and scores are the model's assessment and should be checked against the data.

## Possible next steps

- Run rule-based checks (null counts, duplicate detection) locally in JavaScript and use the AI only to interpret and prioritise the findings
- Export the issue list to CSV or Excel for tracking
- Automatically sample large files before sending them for analysis
- Add column-level profiling (data types, distinct values, min and max)

## About

Built by **Moez Adamjee**, Senior Data, Performance & Insight Analyst, designed and developed with AI-assisted coding tools.

[LinkedIn](https://www.linkedin.com/in/moez-adamjee-06723b217/)

