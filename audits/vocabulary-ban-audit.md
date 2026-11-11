# Vocabulary audit for multilingual copy

Use when certain wording must not appear on a site (a feature that does not exist, a forbidden claim) or must appear (a required section).

## The rule

**Search for word stems and their hyphen and compound variants in every locale. Never search for the noun phrases you remember writing.**

*(observed)* Four clean-up passes by two reviewers reported "clean" while searching for phrases. Switching to stems found 110 more defects.

## Where phrase searches fail

| Hole | Example |
| --- | --- |
| Bare verb forms | The phrase "earned minutes" is caught; `earn`, `earning`, `earned` on their own are not |
| Hyphens and compounds | German `Minutenkonto` matches, `Minuten-Konto` does not |
| Inflection | A Dutch plural drops a vowel (`voordeel` → `voordelen`), so the stem must be `voord` |
| Locale drift | An English-first sweep leaves the other languages behind |
| The idea in other words | "the value of one minute" describes an exchange rate without any banned word. Only reading finds this |

## False positives

The same stem can be a correct, unrelated word in another language (a verb meaning "deserves", the proper word for a locked state). List the allowed forms per locale and do not "fix" them.

## Procedure

1. Write the banned **concept** in one sentence.
2. Per locale, list stems, compounds, hyphen variants and allowed look-alikes.
3. Search every locale with the stem patterns, and confirm each locale was covered.
4. Read a sample for the concept expressed in other words.
5. Record the commit the audit ran against. Re-run at report time, not at fix time.

## Automated checks

A validator that tests copy needs per-locale stems for bans **and** for required sections. *(observed: a check demanding an English heading stem rejected every correct translation.)*

## Read the code, not the label

Before claiming a feature in copy, check how the code treats it. A name in an enum may be legacy and not shipped.
