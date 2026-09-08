# Feedback video script

**Target length:** 4–5 minutes. Screen recording with voiceover.

Open these tabs first: the live site on mobile view, Search Console Performance,
Search Console URL Inspection, the analysis workbook on *Page Analysis*, and the
repository showing `site-v1` and `site-v2` side by side.

---

## 0:00 — 0:30 · Lead with the finding

> "This is a Search Console audit of The First Lakh, a 19-page personal finance content site
> I built and deployed. The headline finding is that the site's problem was never
> ranking. It ranked fine. Nobody clicked the results."

Do not open with your name. Open with the finding.

## 0:30 — 1:20 · Explain the method

Switch to the repository, show both build folders.

> "Search Console needs a real site, but a correctly-built new site gives an audit
> nothing to find. So I built two versions from one content file. v1 carries the
> faults a hobby site normally accumulates. v2 fixes all thirteen. The content is
> identical, so any change I measure is attributable to the SEO work and not to
> rewriting the pages."

Say plainly that v1 is a deliberate control condition. Claiming you discovered
these problems by accident would be the wrong story and an examiner may well ask.

## 1:20 — 2:30 · The CTR opportunity model

This is the strongest part. Switch to the workbook, *Page Analysis*.

> "Search Console gives you clicks, impressions, CTR and average position. Most
> people sort by clicks, which only tells you what is already working.
>
> Instead I compared each page's actual CTR against the CTR you would normally
> expect at that position. The SIP guide ranks at 6.2 and earns 2.42%. The benchmark
> at that position is about 4.9%. On 1,820 impressions, that gap is 41 clicks a
> month — lost to a title tag that just said 'The First Lakh'.
>
> Multiply the gap by impressions across every page and you get 171 recoverable
> clicks a month. Roughly double the traffic, without improving a single ranking."

Then point at the sort order:

> "That last column is the whole value of this. It turns an export into a ranked
> list of what to fix first."

## 2:30 — 3:10 · Indexing and the orphan pages

Switch to URL Inspection.

> "Two pages showed 'Discovered – currently not indexed'. Both had full content
> and nothing linked to them, and with no sitemap Google had no route in. Linking
> them from the hub pages and submitting a sitemap fixed it."

Mention the 404s: one broken link repeated across fourteen pages.

## 3:10 — 3:45 · The tooling problem

> "The brief asks for a Mobile Usability assessment in Search Console. That report
> doesn't exist any more — Google retired it, the Mobile-Friendly Test tool and
> the API in December 2023 and pointed everyone at Lighthouse. So I used Lighthouse
> instead and documented why."

Show the v1 site on a phone viewport, content running off screen.

> "v1 had no viewport tag and a fixed 980-pixel container. Since Google indexes
> mobile-first, that's the version being crawled."

## 3:45 — 4:30 · What you learned

Two or three, specific:

- **Ranking and traffic are different problems.** A page at position 6 with a bad
  title loses more traffic than one at position 8 with a good one.
- **Sequence matters more than severity.** No point rewriting titles on pages
  Google cannot reach. Discoverability first, then mobile, then CTR.
- **Small sites make percentages lie.** A page going from 3 clicks to 6 is a 100%
  improvement and almost certainly noise. Direction across many pages is the only
  trustworthy signal at this scale.
- **Four weeks moves CTR, not position.** Claiming ranking gains in a month on a
  new site would not be credible, which is why CTR was the target.

## 4:30 — 5:00 · Close

> "Everything's in the repository — both builds, the audit with thirteen findings,
> the analysis workbook, and the optimisation log. The CTR before-and-after columns
> are deliberately blank until 28 days of data exist either side of the change.
> Thanks for watching."

---

## Recording notes

- Talk from the bullets. Do not read this aloud verbatim.
- Move the cursor slowly. Fast scrolling is unwatchable.
- Upload to **YouTube as Unlisted**, not Private — reviewers cannot open Private
  links. Test in an incognito window before submitting.
