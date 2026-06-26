# Search Log — LLM-based REST API Test Generation and Testing

**Member:** [Le Van Lam]  
**Date:** 2026-06-04  

---

## Query Strings

### String A

**Verbatim Query:** `(REST API OR Web API) AND (OpenAPI OR Swagger) AND (LLM OR GPT OR Large Language Model) AND (API test generation OR test case generation)`

**Databases & Results:**
- **OpenAlex:** 12 papers
- **Semantic Scholar:** 5 papers
- **Google Scholar:** 8 papers

**Filters:**
- Year: 2020–2026
- English only
- Conference + Journal

**Search Date:** 2026-06-04

---

### String B

**Verbatim Query:**
`(REST API) AND (LLM OR GPT) AND (endpoint coverage OR test coverage) AND (bug detection OR fault detection)`

**Databases & Results:**
- **OpenAlex:** 6 papers
- **Semantic Scholar:** 4 papers
- **Google Scholar:** 4 papers

**Filters:**
- Year: 2020–2026
- English only
- Conference + Journal

**Search Date:** 2026-06-04

---

### String C

**Verbatim Query:**
`(API test generation OR API testing OR automated test generation) AND (LLM OR Large Language Model OR generative AI OR GPT) AND (manual testing OR human OR baseline OR ground truth) AND (coverage OR bug detection OR mutation score OR effectiveness)`

**Databases & Results:**
- **OpenAlex:** 7 papers
- **Semantic Scholar:** 5 papers
- **Google Scholar:** 6 papers

**Filters:**
- Year: 2020–2026
- English only
- Conference + Journal

**Search Date:** 2026-06-04

---

## Summary Before De-duplication

| Database | String | Results |
|-----------|-----------|-----------|
| OpenAlex | String A | 12 |
| Semantic Scholar | String A | 5 |
| Google Scholar | String A | 8 |
| OpenAlex | String B | 6 |
| Semantic Scholar | String B | 4 |
| Google Scholar | String B | 4 |
| OpenAlex | String C | 7 |
| Semantic Scholar | String C | 5 |
| Google Scholar | String C | 6 |
| **Total Before De-duplication** | | **57** |

---

## De-duplication (Dedup)

| Item | Quantity |
|------|------|
| Total before de-duplication | 57 |
| After de-duplication | 33 |
| Removed due to duplicates | 24 |

---

## Section S — Cross-reference Search (Snowballing)

> Snowballing is only conducted after completing V2 screening.

**Methodology:** Backward snowballing

**Execution:**
- Review the reference lists of papers in `03_final_included.csv`
- Find relevant papers using CrossRef and Google Scholar

**Execution Date:** YYYY-MM-DD

**Scanned Included Papers:** [N]

**Newly Discovered Papers:** [X]

**Papers Passing IC/EC:** [Y]

---

## Notes

- De-duplication was performed using Zotero.
- Metadata was exported from Zotero in CSV format.
- Screening was conducted based on the criteria in `ie_criteria.md`.
- Final included papers are saved in `03_final_included.csv`.