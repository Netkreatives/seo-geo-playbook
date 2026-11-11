# Foundation: can crawlers read the site?

Run these on the **live** site, not on the project files. A CDN or host can change what is served.

## Checks

| # | Check | How | Pass |
| --- | --- | --- | --- |
| 1 | Main content is in the raw HTML | `curl -s https://example.com/ \| grep -i "<h1"` | Headline and body text present without JavaScript |
| 2 | Search crawlers are allowed | Read live `/robots.txt` | No disallow for the search bots below |
| 3 | The CDN did not add rules | Compare live `/robots.txt` with the file in the repo | Identical, or differences understood |
| 4 | Each search bot gets a 200 | Repeat for every bot in the table below, against a final URL, not one that redirects: `curl -A "OAI-SearchBot" -s -o /dev/null -w "%{http_code}" https://example.com/en` | `200` for every search and user-fetch bot |
| 5 | One canonical host | Request `http://`, `https://`, `www.` and bare domain | All reach the final URL in one hop. A root-to-locale redirect (`/` to `/en`) counts as a hop; fold it into the host redirect |
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

**`robots.txt` is not the whole answer.** A CDN or firewall can return `403` to a bot that `robots.txt` allows. On three of our sites the CDN blocked two AI bots by user agent while `robots.txt` said they were welcome, and it had also prepended its own managed block of rules to the live file. *(observed)* So test each bot by status code, and compare the live file with your source.

A `curl` with a bot's user agent is a first signal only: bot protection often treats a spoofed user agent differently from the real crawler coming from its published addresses. Confirm in the CDN's own security log before concluding either way.

When a CDN-managed block contradicts your own rules, decide deliberately: blocking training bots is a legitimate choice, blocking search and user-fetch bots removes you from AI answers.

## Structured data: what to leave out

- No review stars or `AggregateRating` without real, visible reviews.
- No `FAQPage` or `HowTo` markup added for rich results. Google restricted FAQ results to a small set of sites and stopped showing HowTo results in 2023. *(sourced: Google Search Central)*

## Publisher identity

An anonymous site gives readers and search engines nothing to verify. Treat identity as a baseline, not a shield: in our portfolio a site with a named person behind it grew through one spam update, and was suppressed site-wide two months later, after the person had been replaced by the organisation. We cannot show that either event was caused by identity. *(observed)*

- An About page naming the organisation and the people who write.
- `Organization` with `sameAs` pointing to real profiles.
- `Article.author` as a `Person`, not the organisation.
- A named reviewer on health, money or legal topics, with their qualification and the date of review.

If the owner will not publish a personal name, use a fully described organisation instead: legal name, country, registration, a working contact route, and reciprocal links between each product site and the organisation's own site and profiles. For regulated topics, add a named external reviewer.

## Bing

Set up Bing Webmaster Tools: import from Search Console, submit the sitemap, enable IndexNow. Bing feeds Copilot and other assistants, and its AI reporting is the nearest thing to free first-party citation data. *(sourced)*

## Titles

- Primary query near the front; title, H1 and URL about the same thing.
- Unique per page. Roughly 40–55 characters keeps the important words visible. *(rule of thumb)*
- Look at the current results for the query before writing. Do not change a URL to match a year or a number.
