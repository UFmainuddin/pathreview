## Week 7 — Issue selection

**Issue link:** https://github.com/ascherj/pathreview/issues/147

**Issue title:** Resume section detection fails on text with leading whitespace

**Tier:** [x] Tier 1 [ ] Tier 2 [ ] Tier 3

**Problem summary:**
The `_detect_sections()` method in `ingestion/parsers/resume_parser.py` uses regex patterns that require section headers (like "Education" or "Experience") to begin at the very start of a line (`^Experience`) or immediately after a newline (`\nExperience`). Text extracted from PDFs commonly preserves leading indentation — spaces or tabs before content — which means none of those patterns ever match, and `detected_sections` always comes back empty. As a result, the ingestion pipeline has no structural information about the resume even when well-known sections like Education or Skills are clearly present. A successful fix would update the four patterns inside `_detect_sections()` to tolerate optional leading whitespace (e.g., `^\s*Experience`) so that section detection works regardless of indentation level.

**Selection notes ("Is this right for me?" reasoning):**
I chose Tier 1 because this is my first time contributing to a large multi-module codebase. The fix is tightly scoped: it touches exactly one method (`_detect_sections`) in one file (`ingestion/parsers/resume_parser.py`), and the issue body already identifies the root cause (regex anchoring) and the three failing tests to use for verification. There are no external API calls, no schema changes, and no frontend involvement — I can reproduce the bug in a Python shell in under a minute, confirm my fix with the existing tests, and move on. That tight feedback loop made this a confident Tier 1 pick.

**Branch name:** fix/147-resume-section-whitespace

**Setup confirmation:** [x] App runs locally at localhost:5173

**Cohort ledger:** [x] Issue added to cohort ledger
