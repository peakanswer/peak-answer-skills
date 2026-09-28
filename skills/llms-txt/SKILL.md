---
name: llms-txt
description: Write or review an llms.txt file for a site. Use when someone asks what llms.txt is, wants one written, wants theirs checked, or asks whether it is worth having.
---

# llms.txt

A markdown file at `https://<domain>/llms.txt` that tells a model what a site is and points it at the pages worth reading. It is a proposal, not a standard, and no engine has committed to reading it.

## Say the honest thing first

Adoption is contested. No major engine has confirmed it uses `llms.txt` for retrieval or ranking, and there is no measured evidence that adding one lifts citations. It costs an hour and it cannot hurt, which is the whole case for it. If someone is choosing between writing `llms.txt` and fixing a `Disallow: /` on `GPTBot`, the robots file wins by a distance.

Do not describe it as required, as a ranking factor, or as something engines expect. That claim is everywhere and it is not true.

## The format

Plain markdown, no front matter. One `#` heading, a `>` blockquote summary, then `##` sections of links with a short description after each.

```markdown
# Acme Analytics

> Session replay and funnel analysis for B2B SaaS teams. Self-serve from $49 a month, SOC 2 Type II, EU data residency available.

Acme records what users do in a product and shows where they drop out. Used by product and growth teams, typically 10 to 200 seats.

## Docs

- [Quickstart](https://acme.com/docs/quickstart): install the snippet and see a first session in about five minutes.
- [Funnels](https://acme.com/docs/funnels): defining a funnel, and how drop-off is attributed between steps.
- [Data retention](https://acme.com/docs/retention): what is stored, for how long, and how to shorten it.

## Product

- [Pricing](https://acme.com/pricing): plans, seat counts and what each tier includes.
- [Security](https://acme.com/security): SOC 2, subprocessors, data residency.

## Optional

- [Changelog](https://acme.com/changelog): releases, newest first.
```

Rules that matter:

- **Absolute URLs.** The file may be read far from its origin.
- **A description after every link,** separated by a colon. A bare list of URLs is the most common failure and it carries almost no information.
- **`## Optional` is special.** Its contents are what a model can skip when short of context. Everything else is what you want read.
- **Keep it under about 50 links.** A dump of the sitemap is a sitemap, not this.

## What goes in the summary

The blockquote is the piece most likely to be read in isolation. It should answer what this is, who it is for, and the two or three facts a buyer needs: price shape, deployment model, compliance, region. Specifics, not adjectives. "Leading platform for modern teams" tells a model nothing it can quote.

## Reviewing an existing one

1. Does it exist and return 200 as `text/markdown` or `text/plain`, not an HTML 404 page?
2. Is there a single `#` heading and a `>` summary under it?
3. Do the links have descriptions, and are they absolute?
4. Do the links resolve? A dead link here is worse than a missing one.
5. Is it current? A file listing last year's product names dates the site to whatever reads it.
6. Is it consistent with the site itself? Contradicting the pricing page is worse than having no file.

## `llms-full.txt`

The same idea with the page contents inlined rather than linked. Only worth generating if the docs are small and genuinely stable, because it goes stale silently and nothing tells you.

## With the Peak Answer MCP connected

`generate` with `llms_txt` writes one from the site's own pages, in this format, with the descriptions drawn from the pages rather than invented. Read it before publishing: it is a draft that knows the site's structure, not the positioning.

Free, no signup: https://peakanswer.com/tools/llms-txt-generator
