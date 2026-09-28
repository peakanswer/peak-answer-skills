---
name: geo-audit
description: Audit a site for whether AI search engines can reach, read and quote it. Use when someone asks why ChatGPT or Perplexity does not cite their site, wants a GEO or AEO audit, asks about AI crawler access, or is about to start optimising for AI search and needs a baseline.
---

# GEO audit

Work out whether the AI engines can reach a site, read it, and find something quotable on it. In that order, because the later checks do not matter if the earlier ones fail.

## Run the checks in dependency order

A site that blocks GPTBot does not have a schema problem. Fix the top of this list before reporting anything below it.

### 1. Crawler access

Fetch `https://<domain>/robots.txt` and check each of these user agents by name. They are separate crawlers with separate jobs, and blocking one does not imply the others:

| Agent | Operator | What blocking it costs |
| --- | --- | --- |
| `GPTBot` | OpenAI | Training and, in practice, retrieval coverage |
| `OAI-SearchBot` | OpenAI | ChatGPT search results specifically |
| `ChatGPT-User` | OpenAI | Live fetches when a user asks about your page |
| `ClaudeBot` | Anthropic | Claude's index |
| `Claude-User` | Anthropic | Live fetches during a Claude conversation |
| `PerplexityBot` | Perplexity | Perplexity's index |
| `Perplexity-User` | Perplexity | Live fetches |
| `Google-Extended` | Google | Gemini and AI Overviews grounding |
| `Bingbot` | Microsoft | Bing and Copilot |
| `Applebot-Extended` | Apple | Apple Intelligence |

Read the rules properly. `Disallow: /` under `User-agent: *` blocks every agent that has no more specific block of its own. A more specific group wins outright — an agent named in its own group ignores the wildcard group entirely, it does not merge with it.

Also check for the mistakes that look fine:

- A `Disallow:` with no path means allow everything. A `Disallow: /` blocks everything. One character.
- `Crawl-delay` is ignored by most of these agents. It is not a block, so do not report it as one.
- A 404 on `/robots.txt` allows everything. A 500 is treated as a full block by several crawlers, which is much worse than not having the file.
- Cloudflare bot rules, a WAF, or a "verify you are human" interstitial can block a crawler while robots.txt reads permissive. Fetch a real page with each user agent string if you can, rather than trusting the file.

### 2. The page actually resolves for a crawler

Fetch the homepage and two deep pages with a plain client, no JavaScript. Check:

- Status is 200, not a redirect chain ending somewhere unexpected.
- The main content is in the HTML. If the body is an empty `<div id="root">`, the content is client-rendered and several of these agents will see nothing. This is the single most common silent failure.
- No `noindex` in a meta tag or `X-Robots-Tag` header.
- The canonical, if present, points where you expect. A canonical pointing at a different page hands the citation to that page.

### 3. What the engines look for once they can read it

- **`llms.txt`** at the root. Absent is not fatal and its adoption is genuinely contested, so report it as a small opportunity rather than a fault. See the `llms-txt` skill for what belongs in one.
- **Structured data.** `Organization` and `WebSite` on the homepage, `Article` on posts, `FAQPage` where there are real questions and answers, `Product` with `offers` on product pages. Validate it parses; invalid JSON-LD is worth less than none because it looks done.
- **Answer structure.** Whether a page states its answer near the top, has real headings, and contains anything liftable like a comparison table or an FAQ. See the `answer-readiness` skill.
- **Sitemap** at `/sitemap.xml`, referenced from robots.txt, returning 200 and listing live URLs.

## What to report

Ordered by what blocks what, with the fix beside each finding. Not a score with no instructions attached.

For each finding give: what is wrong, the evidence (the exact line of robots.txt, the URL that 404s), what it costs, and the specific change. "Add `User-agent: GPTBot` / `Allow: /` to robots.txt" is a finding. "Improve crawlability" is not.

Say what passed too. A list of only problems reads as a sales pitch and hides whether the important things are already fine.

## Two honest caveats to include

- **Blocking a crawler is sometimes deliberate.** Publishers block `GPTBot` on purpose. Ask before calling it a fault.
- **None of this makes an engine cite you.** It makes citation possible. What gets cited is usually somebody else's article about the category, so a clean audit is the floor, not the win. Say so, or the report over-promises.

## With the Peak Answer MCP connected

If the `audit_site` tool is available it runs this whole pass in one call and returns answer readiness, crawler access, robots.txt, sitemap, structured data, headings, meta description, readability and entities together. Use it for the baseline, then read the findings yourself rather than pasting them, because the ordering above is what makes a report actionable.

`geo_audit` is a different thing: it asks a real model ten real buying questions and takes minutes. It starts a background run and returns immediately, so call it once and collect the result later. Never block an audit on it.

Free, no signup: https://peakanswer.com/tools/ai-visibility-audit
