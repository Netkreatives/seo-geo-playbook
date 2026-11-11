# Foundation: can crawlers read the site?

Run these on the **live** site, not on the project files. A CDN or host can change what is served.

## Checks

| # | Check | How | Pass |
| --- | --- | --- | --- |
| 1 | Main content is in the raw HTML | `curl -s https://example.com/ \| grep -i "<h1"` | Headline and body text present without JavaScript |
| 2 | Search crawlers are allowed | Read live `/robots.txt` | No disallow for the search bots below |
| 3 | The CDN did not add rules | Compare live `/robots.txt` with the file in the repo | Identical, or differences understood |
| 4 | Bots get a 200 | `curl -A "OAI-SearchBot" -s -o /dev/null -w "%{http_code}" https://example.com/` | `200` |
| 5 | One canonical host | Request `http://`, `https://`, `www.` and bare domain | All redirect to one, in a single hop |
| 6 | Sitemap lists only indexable pages | Fetch every URL in the sitemap | All `200`, self-canonical, no `noindex` |
| 7 | Canonical on every page | Inspect `<link rel="canonical">` | Present, absolute, points to itself |
| 8 | Structured data | Validate with a schema testing tool | `Organization`, `WebSite`, plus `Product` or `SoftwareApplication` |
| 9 | hreflang, if multilingual | In HTML or in per-locale sitemaps (either works) | Reciprocal, with `x-default` |

## Training bots and search bots are different

Blocking a training bot does not remove you from AI search. Blocking a search bot does. *(sourced: each vendor's crawler documentation; names change, so check them)*

| Purpose | Examples |
| --- | --- |
| Model training | `GPTBot`, `ClaudeBot`, `Google-Extended`, `CCBot` |
| Live answers and search | `OAI-SearchBot`, `Claude-SearchBot`, `PerplexityBot`, `Bingbot`, `Googlebot` |
| Fetch on behalf of a user | `ChatGPT-User`, `Claude-User`, `Perplexity-User` |

If you run bot protection, check its security log after launch: aggressive modes can challenge legitimate crawlers. *(sourced)*

## Structured data: what to leave out

- No review stars or `AggregateRating` without real, visible reviews.
- No `FAQPage` or `HowTo` markup added for rich results. Google restricted FAQ results to a small set of sites and stopped showing HowTo results in 2023. *(sourced: Google Search Central)*

## Publisher identity

An anonymous site is easier to classify as scaled content. *(observed: the one site in our portfolio with a named person behind it kept growing through a spam update that demoted the others.)*

- An About page naming the organisation and the people who write.
- `Organization` with `sameAs` pointing to real profiles.
- `Article.author` as a `Person`, not the organisation.
- A named reviewer on health, money or legal topics.

## Bing

Set up Bing Webmaster Tools: import from Search Console, submit the sitemap, enable IndexNow. Bing feeds Copilot and other assistants, and its AI reporting is the nearest thing to free first-party citation data. *(sourced)*

## Titles

- Primary query near the front; title, H1 and URL about the same thing.
- Unique per page. Roughly 40–55 characters keeps the important words visible. *(rule of thumb)*
- Look at the current results for the query before writing. Do not change a URL to match a year or a number.
