# Jio CareOps — Network Issue Analyzer

An internal Customer Experience and Network Operations tool built for the AlmaBetter capstone project. The project repairs an unfinished internal notebook into a working pipeline that connects customer complaints with network issues, recharge failures, service requests, and customer history — so support and operations teams can see the full picture of a complaint in one place instead of five separate files.

## Problem

Jio CareOps handles thousands of customer complaints, but the signals that explain WHY a complaint is serious — an active network outage, a failed recharge, a breached service SLA, a repeat-complaining customer — lived in separate files with no connection between them. A high-impact complaint could be reviewed late simply because nothing linked the evidence together.

## What this notebook does

1. **Loads** 7 source files (CSV, Excel, JSON, TXT) from a dataset ZIP.
2. **Validates and cleans** the raw data — flags data-quality issues (duplicate and malformed IDs) rather than silently deleting them.
3. **Classifies** every complaint into an issue category, an owner team (Network Ops / Recharge Ops / Service Desk / Field Support), and a priority level (Critical/High/Medium/Low) based on a 5-signal weighted score.
4. **Links** aggregated network, recharge, and service-request signals onto each complaint — safely, without multiplying rows.
5. **Scores** locations (city/circle/cell site) and customers for operational risk and repeat-complaint impact.
6. **Recommends** a specific next action per complaint, tied to the owning team and the complaint's real signals.
7. **Generates** an AI-ready support prompt per complaint (text only — no external API calls).
8. **Provides** a live, interactive filter/search panel (ipywidgets) so a non-technical agent can find cases without writing code.
9. **Exports** a final report matching the PRD's exact 21-column schema, with a validation table proving the report's completeness.

## Key results

- 5,000 complaints processed: 538 Critical / 2,314 High / 1,017 Medium / 1,131 Low.
- 866 complaints linked to a site with an active network issue.
- 769 complaints from repeat, high-impact customers escalated to Retention.
- Final report validated against the PRD's schema — all 7 validation checks passed.

## Repository contents

- `Jio_CareOps_Network_Issue_Analyzer_Student_Colab_Problem_Statement.ipynb` — the completed notebook (all 19 sections + final deliverables)
- `README.md` — this file

## How to run

1. Open the notebook in Google Colab.
2. Run the dataset upload cell and upload `jio_careops_network_issue_analyzer_dataset.zip` when prompted.
3. Run all cells in order (Runtime → Restart session and run all).

## Notes and limitations

- Several thresholds (signal strength, capacity utilization, SLA windows, score cutoffs) are documented judgment calls, made where the PRD did not specify an exact number — see the notebook's Assumption and Limitation Log for the full list and reasoning.
- 99 duplicate complaint IDs and 3 malformed service-request IDs exist in the source data and are flagged, not deleted, per the project's data-integrity rule (BR-08).
- This is a capstone project built on fully synthetic data, for educational use only.
