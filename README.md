# Recruitment Job Import Automation — n8n + Airtable

Portfolio demonstration of a recruitment job-import workflow built with **n8n**, the **Remotive public jobs API**, and **Airtable**. This repository is an independent portfolio example; it is **not an official VA Masters product or endorsement**.

## What the exported workflow does

Manual Trigger → HTTP Request (Remotive) → Split Out `jobs` → Edit Fields → Filter → Airtable upsert.

- Fetches job listings from the public Remotive API (`limit=10` in the exported configuration).
- Maps external job ID, title, company, job URL, type, required location, salary, and publication date.
- Filters for populated title, company and URL and a positive external job ID.
- Uses Airtable **upsert matching on External Job ID** to avoid creating a new row for the same ID on reruns.

## Setup

1. Import `workflows/remotive_job_import.template.json` into your own n8n instance.
2. Create or select an Airtable base and a job-openings table with the mapped columns listed in `docs/Architecture.md`.
3. Open the Airtable node, choose **your own Airtable credential**, and select **your own base and table**. The template deliberately contains nonfunctional placeholder IDs.
4. Review field mapping against your Airtable schema and run a small manual test. Do not activate or schedule the workflow until verified.

**Security:** Never commit live credentials, API tokens, Airtable base/table identifiers, applicant records, or n8n execution data. The original export is intentionally excluded from this repository.

## Validation status

Previous local testing reported a successful 18-record import and duplicate-prevention rerun. Those results describe the user's original environment; **this sanitized template has not been re-imported and execution-tested**. See `docs/QA_Report.md`.

## Scope

The attached workflow export demonstrates the **job-import portion** of a broader five-table recruitment Airtable design. It does not export the entire Airtable base, other tables' automations, or any candidate/application data.
