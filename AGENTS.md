---
framework_version: 1.1.0
---

# Agent Guidelines: AI Job Search IL

This is a Codex-first workspace for high-tech job search in Israel, with possible relocation to the United Kingdom, New York City, or San Francisco. Research, evaluation, and local drafting are the default scope. Sending applications, contacting people, changing LinkedIn, and publishing personal data require explicit user instructions.

## Read first: private profile and source boundaries

Read `.local/profile.md` when present. It is the source of truth for this candidate's facts, preferences, open questions, and search status. LinkedIn evidence belongs in `documents/linkedin/`; CV sources belong in `documents/cv/`. Both are Git-ignored. Facts must have a source and observation date; distinguish user-confirmed preferences, profile statements, and provisional interpretations.

**This fork uses private profile mode.** The tracked `CLAUDE.md`, `01-candidate-profile.md`, other numbered reference files, and `cv/main_example.tex` remain reusable templates. Never populate those files with personal details. For every workflow, including setup, expand, apply, interview, and outcome:

- Read/write personal facts, languages, behavioral preferences, career goals, salary expectations, and STAR examples in `.local/profile.md`, in place of the personal sections in the tracked templates.
- Continue reading the numbered `.claude/skills/job-application-assistant/` files for methodology, scoring, style, and document rules. Placeholder tokens and example claims are not candidate evidence.
- Use a verified CV in `documents/cv/` as a factual source if one exists. Otherwise use the private profile; the stock master CV is a layout reference only. Tailored drafts never become evidence of new accomplishments.
- When a workflow says to write a new confirmed fact back to `01-candidate-profile.md` or `CLAUDE.md`, update `.local/profile.md` instead. Put personalized search refinements and wording preferences there too.
- If the private profile is missing, collect available evidence and create it locally; do not fill gaps from the upstream examples. Ask only for information needed for the next decision. Do not invent metrics, technical proficiency, team size, citizenship, or work authorization from titles or location.
- Verify ignore coverage before writing personal files with `git check-ignore <path>`. Never force-add private files. Git ignore is not encryption or a backup; check the staged diff before any publication. Do not commit or push unless requested.

These path substitutions take precedence over the upstream profile-generation instructions, including their tracked-file onboarding path. Preserve the workflow's factual checks, posting integrity checks, and submission boundaries.

## Codex workflow routing

Use plain-language requests in Codex. The slash names below are aliases in these instructions, not a claim that Claude's command registration or permissions work in Codex. Read only the specification needed for the requested task; keep `.claude/` as the shared workflow source.

| Request / alias | Specification |
|---|---|
| Set up or refresh my profile / `/setup` | `.claude/commands/setup.md`, with private profile mode above |
| Find jobs / `/scrape` | `.claude/skills/job-scraper/SKILL.md` and its `search-queries.md` |
| Rank saved jobs / `/rank` | `.claude/commands/rank.md` |
| Evaluate a posting | `.claude/skills/job-application-assistant/SKILL.md`, Step 1 only |
| Draft an application / `/apply` | `.claude/commands/apply.md`; draft is not submission |
| Prepare an interview / `/interview` | `.claude/commands/interview.md` |
| Record an outcome / `/outcome` | `.claude/commands/outcome.md`; use actual user-confirmed status |
| Other upstream workflow | Matching `.claude/commands/<name>.md` or `.claude/skills/<name>/SKILL.md`; if absent, say so |

Translate tool names by capability: Read/Glob/Grep to filesystem reads and `rg`; Write/Edit to file edits; Bash to the available shell; WebSearch/WebFetch to the available search/fetch tools or authenticated Chrome when needed. Use existing connected tools first. Claude's `allowed-tools`, `settings.json`, model names, `$ARGUMENTS`, and `$SCRATCHPAD` are not Codex configuration: interpret arguments from the request and use a verified writable session/system temporary directory **outside the repository** for raw downloads and scratch files. `tools/fetch_page.py` intentionally refuses in-repository outputs; do not bypass that guard. Curated profile facts and approved archives can then be saved to the ignored paths above. Run helper scripts from the repository root so relative state paths remain consistent. On Windows use a verified Python executable and PowerShell syntax, not Bash heredocs.

Run workflows sequentially by default. When a specification calls for an Agent/reviewer, perform a separate critical review against the saved source evidence yourself and identify it as a self-review. Do not claim an independent agent review; delegate only when explicitly requested. Optional connectors, Bun, and PDF compilers are capabilities to check, not assumed prerequisites for research. Missing Bun uses the documented web fallback; missing PDF tooling means a document stays a draft until compilation, rendering, and inspection succeed.

## Search and evaluation

- Use `.claude/skills/job-scraper/search-queries.md` for market scope and `.local/profile.md` for candidate-specific targeting. Search Israel and each relocation destination separately; preserve source coverage and unknowns.
- High-tech is the industry focus, not a requirement to search only engineering jobs. Match the candidate's function and actual scope. Do not treat a management title as proof of people-management scale.
- Read the eligibility and location gates in `04-job-evaluation.md`. Relocation within the agreed destinations is allowed; sponsorship and remote-work eligibility still need role-level evidence. Unknown is FLAG, not PASS or automatic rejection.
- Compare compensation only with currency, period, base/bonus/equity, and source stated. No salary floor or immigration eligibility is assumed.
- English is the provisional document default unless the private profile says otherwise. Hebrew documents require RTL/bidi support and rendered verification; do not claim a Latin-only stock template supports them.
- LinkedIn profile reading is read-only through the connected Chrome session. Save relevant professional evidence only; do not save cookies, tokens, messages, unrelated contacts, or analytics. Report which sections were actually read.

## Checks for framework changes

Use a verified Python 3.10+ executable. Run `python tools/lint_skills.py`, `python tools/security_guards.py`, and relevant `unittest` tests. Run the full Python suite for shared framework changes. Keep test TEMP/TMP outside the repository so fetch tests exercise the intended trust boundary; local HTTP fixtures also require loopback networking. Check the staged or working diff for personal-data leaks. Only run Bun checks if portal code changes. Report unavailable checks honestly.

## Thin-Pointer Design (Single Source of Truth)

To prevent duplication and configuration drift across different AI agent frameworks (Claude Code, Google Antigravity, Codex, Cursor, Gemini CLI, etc.), this workspace uses a unified thin-pointer design. All agent runtimes should load the canonical specifications and candidate profiles from the files and directories below:

1. **Personal Candidate Profile:**
   - Candidate facts and preferences live in `.local/profile.md`. [CLAUDE.md](CLAUDE.md) and [.claude/skills/job-application-assistant/](.claude/skills/job-application-assistant/) retain reusable templates and methodology, subject to private profile mode above.
2. **Canonical Workflow Specifications:**
   - The step-by-step instructions and triggers for tasks (setup, scrape, rank, apply, upskill, interview) are defined in the [.claude/](.claude/) directory (specifically under `.claude/skills/` and `.claude/commands/`).
   - Do not duplicate these rules or specifications. Treat `.claude/` files as the single source of truth.
3. **Portal Search Skills:**
   - Job-portal search CLIs live under [.agents/skills/](.agents/skills/) in the portable Agent Skills format (with a `SKILL.md` per portal). Codex and Antigravity discover these automatically; the `/scrape` workflow in [.claude/skills/job-scraper/](.claude/skills/job-scraper/) orchestrates them.
