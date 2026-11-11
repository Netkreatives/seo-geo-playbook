# Prompt: foundation audit

Works best with an agent that can open the site's repository. Fill in the three lines and paste the rest unchanged.

```
Site: <URL>
Product: <one sentence>
Competitors: <2 or 3 names>

Audit this site against seo/foundation.md from the SEO/GEO playbook.
Work in this order and stop after each step.

1. Audit only; change nothing. Fetch the live robots.txt, the raw HTML of
   the homepage, the sitemap, and the http/https/www variants. For each
   check give pass or fail with proof: the line or the status code.
2. List fixes, smallest first. For each: the file, the change, and the
   check that proves it worked.
3. Wait for my approval before each change. Show the diff first for
   anything touching robots.txt, canonicals, redirects or noindex.
   Never delete a page.
4. After each change, rerun its check and show the result.
5. List what only I can do (Search Console, Bing Webmaster Tools,
   directories, outreach), in order.
6. Draft 20 buyer questions. Mark the ones you guessed.
7. Propose 5 decision pages. For each: the query, what the current top 10
   looks like, and the one thing my page would add. Write nothing until I
   pick one.

Rules:
- A number comes from a tool or a page you fetched, never from memory.
  If you cannot check something, write "not checked".
- Never invent a search volume.
- No review stars, FAQ markup or HowTo markup.
- Install no third-party skill or repo without showing me its files first.
```

Structure adapted from the audit prompt in the article listed first in [resources](../resources.md).
