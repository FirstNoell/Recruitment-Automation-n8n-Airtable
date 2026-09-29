# Architecture and mapping

**Flow:** Manual Trigger → Remotive HTTP GET → Split Out `jobs` → Edit Fields → Filter → Airtable upsert.

**Airtable job table mapping:**

| Airtable field | Source |
| --- | --- |
| External Job ID | `id` |
| Job Title | `title` |
| Company Name | `company_name` |
| Job Source | constant `Remotive` |
| Job URL | `url` |
| Job Type. | `job_type` |
| Publication Date | `publication_date` |
| Required Location | `candidate_required_location` |
| Salary | `salary`, fallback `Not specified` |

The export uses **External Job ID** as its upsert match column. Its configured filter checks required job title, company, URL, and a positive external job ID. The source file contains references to other Airtable fields/tables as cached schema metadata, but it does not include a complete five-table Airtable schema export.
