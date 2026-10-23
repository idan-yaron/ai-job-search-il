# Search strategy: high-tech in Israel and selected relocation markets

The default scope is Israel, plus the United Kingdom, New York City, and San Francisco. Read `.local/profile.md` for the candidate's actual role targets, sponsorship needs, language proficiency, and confirmed preferences. This tracked file contains reusable market strategy, not personal résumé details.

## Market coverage

Run each market separately and label results by market. A default search samples the top three function categories in every requested market, keeping Israel first in the presentation. A focus request can narrow this. A low-volume sample is not an exhaustive market search; list queries, sources, dates, and coverage limits.

| Market | Search location | Treatment |
|---|---|---|
| Israel | Israel; optionally Tel Aviv and other Israeli tech hubs | Primary market. Verify actual office and commute constraints; do not silently restrict all Israel to Tel Aviv. |
| United Kingdom | United Kingdom; London as an additional focused query | Relocation market. Do not reduce the UK to London only. |
| New York City | New York, United States | Relocation market. Check city/metro location; do not accept statewide results as NYC automatically. |
| San Francisco | San Francisco, California, United States | Relocation market. Flag wider Bay Area results separately pending geographic approval. |

Remote roles qualify only when the employer permits employment from Israel or an agreed relocation destination. US-only remote is not work-from-Israel eligibility. A relocation package is not visa sponsorship. Apply `04-job-evaluation.md` before treating any match as feasible.

## Sources and access

- Employer careers pages and their linked ATS postings are the final source for requirements, live status, location, and sponsorship.
- LinkedIn provides discovery across all four markets, through connected Chrome or the existing `linkedin-search` CLI.
- The existing `freehire-search` CLI can provide additional discovery, subject to verifying its geography and employer source.
- Web search over employer careers pages and ATS domains provides a fallback and another discovery channel. Do not label a search snippet as a verified opening.
- Danish demo skills remain disabled. Do not install a new portal adapter just to begin this search.

Read each enabled portal's `SKILL.md` for actual flags. Missing Bun or a failing source triggers the existing web fallback, with the failure reported. Never report a timeout, login wall, or dropped location filter as zero jobs.

For LinkedIn, pass each market explicitly through `--location`; combine with the candidate's title/function query and `--jobage 14 --limit 20 --format json`.
For Freehire, use country facets for Israel/UK and city facets for NYC/SF after checking the live facet vocabulary. Its region/country/city facets form an **OR group**: combining US country and NYC city broadens to the whole US, so never use that combination to claim a city-only search. Verify the returned location in all cases.

## Function categories

For this product-focused starting strategy, use the candidate's approved seniority range. Keep management and individual-contributor tracks separate; role scope matters more than title. Do not add VP/CPO, junior, engineering, or legal-only roles solely because the candidate has adjacent experience.

### Priority 1: Product leadership and strategy

Title variants: Director of Product, Director of Product Management, Head of Product, Group Product Manager. Add AI, data platform, SaaS, or enterprise software when relevant to the candidate profile. Assess team, strategy, roadmap, commercial ownership, and decision scope from the posting rather than title alone.

### Priority 2: AI and data product ownership

Title variants: Senior Product Manager, Staff Product Manager, Principal Product Manager, Technical Product Manager. Function variants: AI products, GenAI, AI agents, data products, data platforms, APIs, analytics. An AI label does not establish an ML engineering requirement or candidate coding proficiency.

### Priority 3: Broader high-tech product roles

Senior product leadership and senior IC work in B2B SaaS, developer/platform products, fintech, insurtech, cybersecurity, or other technology companies where the actual responsibilities fit. These are discovery categories, not claims that the candidate has expertise in every sector.

English is the initial query language in all markets. Add Hebrew title variants for Israel when supported by the private profile: מנהל מוצר בכיר, מנהלת מוצר בכירה, ראש תחום מוצר, דירקטור מוצר, מוצרי נתונים, בינה מלאכותית. Search keywords do not declare a language proficiency.

## Web fallback examples

Substitute the role and one market at a time; verify real posting pages after discovery:

```text
site:linkedin.com/jobs/view "Director of Product" "Israel"
site:linkedin.com/jobs/view "Senior Product Manager" "United Kingdom"
site:job-boards.greenhouse.io "Product" "New York"
site:jobs.lever.co "Product" "San Francisco"
site:jobs.ashbyhq.com "Product" "Israel"
```

Use the employer's own careers site to resolve missing details. A broad company sponsorship statement is a lead, not proof for an individual role. Search without the word sponsorship too, to avoid silently discarding promising roles whose policies need verification.

## Freshness, fit, and reporting

Prefer postings from the last 14 days. Older postings with future stated deadlines may be retained. Unknown posting dates stay visibly unknown. A live source check is required before recommending a role; preserve exact URL, title, company, location, observed date, stated posting date/deadline, and evidence excerpt.

Separate confirmed matches, conditional leads, exclusions, and unreachable pages. Show skill/experience fit separately from work-authorization feasibility. Every relocation lead must show sponsorship as role-confirmed / unknown / explicitly unavailable, with the source and date. Exclude an explicit no-sponsorship role when the candidate needs sponsorship; keep unknowns conditional, never verified.

Use existing deduplication, tracker, posting-integrity, and state helpers. Keep personal evidence in ignored local files. Never apply, contact an employer, or change LinkedIn as part of a search.
