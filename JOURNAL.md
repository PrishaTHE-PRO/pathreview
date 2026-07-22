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
