# Letting an AI agent do SEO work

## Permission tiers

| Tier | Actions |
| --- | --- |
| Allowed | Read data, crawl, write drafts and reports |
| Needs approval, diff shown first | Publish a page, change a title, add a redirect |
| Never on its own | Delete a page; change `robots.txt`, canonicals or `noindex` |

Enforce the last tier in a hook or CI check, not in a prompt.

## Guard the four quiet killers

Snapshot key pages before each deploy and compare after:

1. A page turns `noindex`.
2. A canonical points somewhere else.
3. A `200` becomes a `404`.
4. `robots.txt` blocks everything.

## Data discipline

- Numbers come from a tool. Test the agent: ask for the top five pages by clicks and compare with Search Console.
- If something cannot be checked, the report says "not checked".
- State lives in files in the repo (context, keyword map, backlog, change log), not in the agent's memory. Each fact carries the file or URL it came from.
- A verification result names the commit it ran against.

## Review

- Grade every draft against a written rubric before it ships, with a pass mark and a floor per category.
- Use a second model as an adversarial reviewer of recommendations. In one of our runs it kept 14 of 43, demoted 21 and vetoed 8. *(observed)*
- A weekly tracker that produces no recommendations is a valid result. Do not tune it until it always finds something.

## Pipeline shape that worked *(observed)*

```
collect (Search Console, crawl, SERP data) -> bundle per site -> analyse
   -> adversarial review -> score -> report -> plan (accept / schedule / done)
```

- One local database as the source of truth; reports are generated from it.
- A budget flag per run, with paid lookups (search volume is usually the largest cost) behind it.
- With concurrent collectors on SQLite: WAL mode, short transactions, never hold a write transaction across a network call.
- Forcing a JSON schema on a model's first turn can make it answer before reading the files. Let it analyse in free text first, convert to the schema in a second step.
- Large exports go from tool to disk, never through the model's context.

## What not to automate

- "Merge when the build passes" for content.
- Link buying or exchanges.
- Publishing on a daily quota.

## Installing third-party skills

Read the files first. Check for: a hosted connector your data passes through, promotional links added to output, install scripts piped from a remote branch, and outdated guidance. A quick test: ask the skill which crawler decides whether you appear in ChatGPT search. See [resources](../resources.md).
