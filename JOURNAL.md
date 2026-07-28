## Week 7 - Issue selection

**Issue link:** https://github.com/ascherj/pathreview/issues/147

**Issue title:** Resume section detection fails on text with leading whitespace

**Tier:** [x] Tier 1  [ ] Tier 2  [ ] Tier 3

**Problem summary:**
The resume parser currently misses section headers when extracted text contains leading spaces before headings like Education or Skills. This matters because PDF text extraction often preserves indentation, so valid resumes can produce an empty `detected_sections` list even though the sections are present. The affected code is in `ingestion/parsers/resume_parser.py`, specifically the `_detect_sections()` logic. A successful fix should allow section headers to be detected whether or not they are indented, while keeping the existing resume parser behavior intact.

**Selection notes:**
This issue is a good fit because it is Tier 1, has a focused scope, and affects one parser module with existing unit tests. The expected behavior is clear from the issue reproduction: indented section headers should be detected the same way as unindented headers. The fix can be verified with a targeted regression test in `tests/unit/test_resume_parser.py`.

**Branch name:** fix/147-resume-section-leading-whitespace

**Setup confirmation:** [x] App runs locally at localhost:5173

**Cohort ledger:** [ ] Issue added to cohort ledger

## Week 8 — Reproduction & solution planning

**Reproduction commit link:** https://github.com/PrishaTHE-PRO/pathreview/commit/9b883cef99bd1eae6b8cb9be8eb4fefa67472df9

**Reproduction summary:**
I reproduced issue 147 with a focused resume parser regression test using indented `Education:` and `Skills:` headings. The affected behavior lives in `ResumeParser._detect_sections()`, where section headings need to be detected even when PDF or Markdown extraction preserves leading whitespace.

**PLAN.md link:** https://github.com/PrishaTHE-PRO/pathreview/blob/fix/147-resume-section-leading-whitespace/PLAN.md

**Walkthrough video (recommended):** Not recorded.

**Blockers or open questions:**
None right now. The main follow-up risk is ensuring the section detection regex stays anchored to heading-like lines so it does not over-detect normal body text.
