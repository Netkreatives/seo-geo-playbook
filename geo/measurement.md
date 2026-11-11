# Measuring AI visibility

## By hand

1. Write 15–30 real buyer questions. Take them from support mail, reviews and sales conversations. Mark any you invented.
2. Run each at least twice per engine, logged out, with web search on.
3. Log per answer: which products were named, which URLs were cited, and whether your product was recommended or only mentioned.
4. Keep the prompt list fixed so runs can be compared.
5. Add "How did you hear about us?" at signup. Referrer data over-credits search. *(sourced)*

## Automated

The same loop as a script:

```
prompts ──> each engine's API with web search ──> raw answers + citations
                                                        │
                    judge model with a fixed rubric <───┘
                                                        │
              per-run report: mention rate, citation rate, most-cited domains
```

Design notes from building one: *(observed)*

- **Report only.** The tool never edits a site.
- **Separate asking from judging.** One cheap, consistent judge model scores every answer (intent, mentions, page type) against a written rubric. In our runs the judging was well under 1% of the cost; the engine calls were the rest.
- **The useful output is the "most-cited domains" table.** It is the outreach list.
- **Budget per run** and print the cost. Fifty prompts across four engines cost a few dollars.
- **Distrust a result that looks implausible.** One of our secondary data sources produced numbers that made no sense; it was excluded until checked.

## Free stack

Google Search Console, Bing Webmaster Tools, a free backlink checker from one of the large SEO vendors, and a desktop crawler's free tier.

## Reading Search Console honestly

- Mark known algorithm-update windows on the daily chart before blaming a deploy.
- A new page often gets a short trial spike and then decays. That is not a ranking you lost.
- An impression in Search Console is not an "AI mention", whatever a headline says.
