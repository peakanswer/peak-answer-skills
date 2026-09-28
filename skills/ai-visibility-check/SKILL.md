---
name: ai-visibility-check
description: Measure whether AI engines recommend a brand for its buying questions, and where competitors win instead. Use when someone asks if ChatGPT recommends them, wants to track AI search visibility, asks how they compare to a competitor in AI answers, or wants to know which questions to track.
---

# AI visibility check

Whether a brand is named when a buyer asks an engine for a recommendation. This is a measurement task, and almost everything that makes it useful is in how the questions are chosen and how the results are read.

## The questions are the measurement

A visibility number is only as good as the question set behind it. Get this wrong and the rest is noise.

**Ask what a buyer asks, not what a brand wants to rank for.** "Best session replay tool for B2B SaaS" is a buying question. "Acme Analytics" is a branded lookup and tells you nothing: the engine will name them because they were named.

**Cover the shapes buyers actually use:**

| Shape | Example |
| --- | --- |
| Category best | best CRM for a two person agency |
| Constrained | CRM with a free tier and Gmail sync |
| Alternative | alternatives to HubSpot for a small team |
| Comparison | Pipedrive vs Close for outbound sales |
| Job to be done | how do I stop leads going cold after a demo |
| Risk | which CRMs are SOC 2 and store data in the EU |

**Twenty to fifty questions.** Below twenty, a single answer swings the number. Above fifty, the tail is questions nobody asks.

**Fix the set before measuring.** Changing questions between runs makes movement unreadable. Add to the set, keep the old ones, and note the date each was added.

## Running it

- **Several engines, separately.** ChatGPT, Claude, Perplexity, Gemini, Google AI Mode and Copilot answer the same question differently and draw on different sources. A blended score hides where the problem is.
- **Repeat each question.** These are sampled, not deterministic. The same question asked three times can name three different sets. Three runs per question per engine is the floor, and the variance is itself a finding: a brand named in one run of three is in a different position from one named in three of three.
- **No personalisation.** A logged-in account with history is measuring itself.
- **Record the whole answer,** not a yes or no. Position in the list, what it was credited with, and every source cited are the parts that tell you what to do next.

## Reading the result

Four things, in this order:

1. **Presence.** In what share of runs is the brand named at all. This is the headline.
2. **Position.** Named first, in a list of five, or in a footnote. First is worth several times the rest.
3. **Who wins instead.** For every question where the brand is absent, which brands are named. This list, sorted by frequency, is the real competitor set, and it is often not the one the company believes it has.
4. **What is cited.** The URLs the engine leans on. These are almost never the brand's own site. They are listicles, comparison posts, forum threads and review pages, and they are the lever: a citation source that names competitors and not the brand is a specific, fixable gap.

## What to do with a gap

A question where a competitor wins has exactly three causes, and they need different work:

- **The engine cannot read the site.** Crawler blocks, client-rendered content. See the `geo-audit` skill.
- **Nothing on the site answers that question.** The content gap. See the `answer-gap-content` skill.
- **The sources the engine trusts do not mention the brand.** The hardest and usually the largest: the fix is getting into those specific pages, not writing another blog post.

Diagnose which before recommending anything. Most reporting in this space skips straight to "write more content", which fixes only the middle one.

## Honest caveats

- **Answers move on their own.** Model updates change results with no change on the site. One run is a snapshot, and a trend needs weeks of the same questions.
- **Presence is not traffic.** Being named is upstream of a visit and is not measurable in analytics the way a click is. Do not promise attribution that does not exist.
- **Do not report a single blended score** without the question set beside it. It is unfalsifiable otherwise.

## With the Peak Answer MCP connected

`my_visibility` returns measured history for the connected brand rather than a fresh one-off check, and `my_questions` with `only_losing` gives exactly the gap list above, with the winner named. `my_brand` says which domain the connection is scoped to; ask it rather than guessing. `geo_audit` runs ten real buying questions against a real model for any domain, but it is a background run: call it once and collect the result later, never block on it.

Free, no signup: https://peakanswer.com/tools/ai-visibility-audit
