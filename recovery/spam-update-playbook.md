# Spam-update playbook

## Case: seven small sites, one update *(observed)*

A portfolio of small product sites, each with a marketing page plus a large set of generated guide pages in several languages.

- Within days of a Google spam update that named scaled and AI content, the largest site went from about 1,400 impressions a day to under 10. Pages with impressions fell from about 390 to under 30.
- Three more sites followed within the week. One went to zero.
- **Every page was still indexed.** URL inspection passed. This is what an algorithmic demotion looks like; it is not a manual action and not a technical fault.
- Three sites that never had stable rankings showed only a new-page spike and decay.
- One site roughly doubled its impressions through the same update. It had a named author with an About page and `sameAs` links, fewer pages, and pages that worked as tools rather than articles.
- Authority on the demoted sites was near zero: between 1 and 29 referring domains, mostly scraper junk.

**Two months later** the site that had grown fell too: about 73,000 impressions one day, about 1,300 the next, about 100 a day after two weeks. Every country, device and page family fell together. Queries went from over a thousand to twenty and the remaining average position was about 3, which means the site was shown almost only for its own name. There was no manual action, pages stayed indexed, and the crawler kept fetching them successfully. No update was confirmed for that day. Roughly four in five of its URLs were one family of data-driven list pages with no author, date or image.

A first investigation concluded "no portfolio-wide penalty" because it never laid the update dates over the daily chart. Timing remains a correlation, but it changed the diagnosis.

## Diagnosis steps

1. Plot daily impressions per site and mark the update's rollout window.
2. Check Search Console for a manual action.
3. Inspect a sample of URLs. Indexed but invisible means demotion.
4. Count pages with impressions before and after, not only totals.
5. Compare sites that fell with sites that held. What differs: page count, templating, authorship, authority?
6. Rule out your own deploys only after steps 1–5.

## A one-day cliff: first hour

A gradual decline and an overnight collapse need different first steps. For a collapse, rule out the cheap causes before theorising:

1. Manual actions and security issues in Search Console.
2. Your own deploys and CDN or firewall rule changes on that date.
3. URL inspection on three pages: indexed, last crawl date, fetch status, robots state, canonical match.
4. Daily data split by country, device and page family. Everything falling together points to a site-wide classification; one family or one country points elsewhere.
5. Query count and average position before and after. Far fewer queries with a *better* average position means only brand queries are left.

If all five are clean, it is algorithmic. Go to the recovery order below.

## What not to do

- Publish another wave of content.
- Add more languages.
- Move to a new domain.
- Mass-`noindex` in a hurry. Our first clean-up removed the pages that had been earning impressions.
- Buy links.

## Recovery order

1. **Freeze churn.** Stop publishing and stop restructuring.
2. **Identity.** Named organisation and author, About page, `sameAs`, author as `Person`. See [foundation](../seo/foundation.md).
3. **Prune to a small product-tied core.** Withdraw generated pages with `410`. Keep pages with first-party evidence.
4. **Named reviewers** on health, money or legal content before re-indexing it.
5. **Rewrite by hand**, one site at a time, against the four tests in [principles](../principles.md).
6. **Mentions and links.** See [links](../links/mentions-and-links.md).
7. **Wait.** Recovery tends to arrive with later updates, months out.

Put effort where there is still momentum: a site that held through the update is a better investment than the one that fell furthest.
