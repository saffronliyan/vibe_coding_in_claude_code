---
name: Project — AI Learn Site
description: Single-page HTML/CSS/JS educational site about AI concepts; reviewed for security/quality on 2026-05-01
type: project
---

File: /Users/yanli/Desktop/Study/Vibe_Coding_Claude/index.html (422 lines)
Stack: pure HTML + inline CSS + vanilla JS — no build tooling, no external dependencies.
Sections: nav, hero, concept cards, interactive 5-question quiz, milestone timeline, footer.
Quiz architecture: quiz data is a hardcoded JS array; DOM is built entirely with createElement + textContent (XSS-safe); score/answered state are module-level variables reset on retry.

**Key findings from 2026-05-01 review:**
- No XSS risk — all user-visible dynamic content uses textContent, never innerHTML.
- One correctness bug: buildQuiz() calls observer.observe() on ALL .fade-in elements (including already-observed static ones), causing redundant re-observation on retry. Harmless but wasteful.
- One UX bug: the quiz result panel does not scroll into view on first load because it is appended after buildQuiz() runs but display:none; the scrollIntoView in showResult() works correctly at result time.
- Nav hides on mobile (<640px) with no hamburger menu — accessibility gap.
- No CSP header / meta tag.
- No external network calls, no user input fields, no backend — attack surface is minimal.

**Why:** This is a static learning site with no backend, so security risks are low. Primary improvement areas are correctness/robustness and accessibility.
**How to apply:** Future changes should stay in the same no-dependency, inline-everything style. Keep edits small and targeted per CLAUDE.md workflow.
