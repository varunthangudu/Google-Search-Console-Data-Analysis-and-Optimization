# Technical SEO audit — Phase 1

Audit of `site-v1`, the baseline build, using Google Search Console, Lighthouse
and manual source inspection.

---

## A note on method

`site-v1` is a control condition, built deliberately with the SEO faults a hobby
site normally accumulates over time. It is not an existing site whose problems
were discovered by accident, and this report does not claim otherwise.

The reason for building it this way is that a brand-new, correctly-built site
gives an audit nothing to find. Constructing a known-bad baseline, auditing it,
fixing it and measuring the difference produces a genuine before-and-after where
the changes are isolated and the effect is attributable. The content is identical
in both builds; only the SEO layer differs.

---

## Summary

| Severity | Findings | Effect |
|---|---|---|
| Critical | 4 | Pages not discoverable or not indexable |
| High | 5 | Pages indexed but under-performing in results |
| Medium | 4 | Degraded experience, weaker relevance signals |
| **Total** | **13** | |

---

## Critical

### C1 — No XML sitemap

Nothing at `/sitemap.xml`, and nothing submitted in Search Console. Google has to
discover all 19 pages by following internal links, which is slower and misses
anything not linked.

**Fix:** generate `sitemap.xml` covering all 19 URLs, reference it in
`robots.txt`, submit it in Search Console.

### C2 — No robots.txt

Absent entirely. Not fatal on its own, since a missing robots.txt is treated as
permission to crawl, but it removes the standard place to declare the sitemap.

**Fix:** add `robots.txt` with an `Allow` directive and the sitemap reference.

### C3 — Two orphaned pages

`/nps-basics/` and `/ppf-explained/` exist and carry full content, but no page on
the site links to them. Combined with the missing sitemap, Google has no reliable
route to either. Both show **Discovered – currently not indexed** in URL
Inspection.

**Fix:** link both from the relevant hub pages and from the homepage grid, and
include them in the sitemap. Then request indexing for each.

### C4 — Broken internal link producing 404s

Every article page links to `/budgeting-guide/`, which was never built. That is 14
internal links to a non-existent URL, appearing in Search Console's **Not found
(404)** report and wasting crawl budget.

**Fix:** remove the link. Add a proper `404.html` so genuine mistakes land
somewhere useful rather than on a blank page.

---

## High

### H1 — Every page has the same title tag

All 19 pages are titled `The First Lakh`. Title is among the strongest on-page
relevance signals and it is the headline of the search result, so this loses both
ranking relevance and click-through at once. It also makes Search Console's page
data nearly unreadable, since results cannot be told apart.

**Fix:** a unique, query-led title per page, front-loading the term the page is
written for and staying under about 60 characters so it is not truncated.

### H2 — No meta descriptions

Not present on any page. Google generates a snippet from body text instead, which
is often an awkward mid-paragraph fragment. Meta description is not a ranking
factor, but the snippet is most of what determines whether a result gets clicked.

**Fix:** a written description per page, 140–158 characters, naming the problem
the page solves.

### H3 — No canonical tags

With the site served at both `/what-is-sip/` and `/what-is-sip/index.html`, and
potentially with tracking parameters appended, there is no declared canonical
version. This is how duplicate-content dilution starts.

**Fix:** self-referencing `<link rel="canonical">` on every page.

### H4 — CTR far below benchmark on high-impression pages

The clearest finding in the Search Console data. `/what-is-sip/` ranks at an
average position of 6.2 and earns a 2.42% CTR, against roughly 4.9% expected at
that position. On 1,820 impressions that gap is about 45 clicks a month lost.

Across the site the same pattern accounts for roughly 229 recoverable clicks a
month — close to a doubling of current organic traffic, with no ranking
improvement required.

This is a direct consequence of H1 and H2. A result titled `The First Lakh` with
an auto-generated snippet is not competitive against results whose titles restate
the searcher's question.

**Fix:** rewrite titles and descriptions in descending order of the Opportunity
column in `03-gsc-analysis-workbook.xlsx`.

### H5 — No structured data

No schema markup anywhere. The common-questions sections on every article page are a
natural fit for FAQ markup, which can produce expanded results.

**Fix:** `FAQPage` JSON-LD on each article page, generated from the existing
FAQ content so the markup and the visible page always agree.

---

## Medium

### M1 — No viewport meta tag, fixed-width layout

The container is fixed at 980px and there is no `<meta name="viewport">`. On a
390px phone the content runs off-screen and requires horizontal scrolling. Body
text is set at 12px, well below comfortable reading size.

Since Google indexes mobile-first, this is the version of the site that gets
crawled and assessed.

**Note on tooling:** Google sunset the Search Console Mobile Usability report, the
Mobile-Friendly Test tool and the Mobile-Friendly Test API on 4 December 2023, and
now points to Lighthouse instead. The project brief asks for a mobile usability
assessment via a report that no longer exists, so Lighthouse in Chrome DevTools
was used for this section.

**Fix:** add the viewport tag, replace the fixed width with a fluid `max-width`,
raise base font size to 17px, and add responsive breakpoints.

### M2 — Tap targets too close together

Navigation links sit 6px apart at 11px font size. Well below the ~48px touch
target that Lighthouse expects.

**Fix:** minimum 44px touch height and adequate spacing on all navigation links.

### M3 — Non-descriptive anchor text

Internal links read `Click here` and `Read more`. These tell neither users nor
Google anything about the destination, and they are an accessibility problem for
anyone navigating by link list.

**Fix:** descriptive anchor text naming the destination, e.g. *What is an SIP*.

### M4 — No 404 page

A missing URL returns the host's default error page, with no route back into the
site.

**Fix:** a branded `404.html` linking back to the guides.

---

## What was checked and found acceptable

Worth recording, so the audit does not read as though everything was broken:

- **HTTPS** — GitHub Pages serves over HTTPS by default, with no mixed content.
- **Page speed** — the pages are static HTML with no images and one web font
  request. Core Web Vitals pass comfortably.
- **Content depth** — guides run 600–900 words with genuine specificity.
  Thin content was not a finding.
- **URL structure** — clean, lowercase, hyphenated, keyword-relevant. No changes
  needed, which matters because changing URLs later costs the ranking history
  attached to them.
- **Crawl budget** — at 19 pages this is a non-issue. Worth stating explicitly,
  because crawl budget is widely worried about on sites far too small for it to
  apply.

---

## Priority order for Phase 2

Sequenced by dependency, not by severity. There is no point rewriting titles on
pages Google cannot reach.

1. **Make everything discoverable** — sitemap, robots.txt, fix orphans, remove
   the broken link. (C1–C4)
2. **Make the mobile version usable** — viewport, fluid layout, type size, tap
   targets. This is the version being indexed. (M1, M2)
3. **Make results worth clicking** — titles and meta descriptions, highest
   Opportunity first. (H1, H2, H4)
4. **Strengthen the signals** — canonicals, structured data, anchor text. (H3,
   H5, M3)
5. **Then wait.** Changes need 28 days before the comparison means anything.
