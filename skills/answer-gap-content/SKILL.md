---
name: answer-gap-content
description: Decide what to write when an AI engine recommends a competitor instead of you, and brief the piece. Use when someone has a list of questions they lose, asks what content to write for AI search, or wants a content plan aimed at getting cited.
---

# Answer gap content

You know a question where an engine names a competitor and not you. This is how to decide whether content fixes it, and what to write if so.

## First, check content is the answer

Three causes, one fix each. Writing is the answer to one of them.

| What you find | The fix |
| --- | --- |
| The engine cannot fetch or parse the site | Crawler access, server rendering. `geo-audit` skill |
| The site has no page that answers the question | Write it. This skill |
| The pages the engine cites do not mention you | Get into those pages. Below |

Check the citations before writing anything. If the engine answered that question out of three listicles and a forum thread, a new page on your own domain is unlikely to displace them in the short term, and the work is outreach to those four pages instead. Writing is the default recommendation in this field and it is frequently the wrong one.

## Choosing what to write

Rank candidate pieces by three things, in this order:

1. **Does the question have commercial intent?** Someone choosing a tool beats someone learning a definition, every time.
2. **Is the answer contested?** A question where four different brands win across runs is winnable. One where the same incumbent wins every run, on their own comparison page, is not, and the effort belongs elsewhere.
3. **Can you say something first-hand?** A page that restates the same five bullets as the pages already cited gives a model no reason to switch. Your own numbers, your own test, your own product's behaviour, is the reason.

Write for one question per page. A page covering six questions is beaten on all six by six pages.

## The brief

For each piece, fix these before writing:

- **The exact question,** as a buyer types it. Not a keyword.
- **The answer, in one sentence.** If you cannot write it, the page is not ready. This sentence opens the page.
- **The pages currently cited** for that question, and what each is missing. That gap is the page's reason to exist.
- **The proof:** the number, test, dataset or product behaviour only you can state.
- **The liftable block:** the comparison table, the FAQ, the procedure. See `answer-readiness`.
- **Who is named.** Including competitors. A comparison page that only names you is not a comparison, and models notice.

## Writing it so it gets quoted

The shape rules live in `answer-readiness`; the short version is answer first, headings that match questions, something liftable in the middle, and an attributable claim. Beyond shape:

- **Name competitors honestly,** including where they are the better fit. Pages that engines quote in comparison answers are the ones that read as evaluations rather than as pitches. A page that says a rival wins on one axis is more quotable, not less.
- **Be specific enough to be wrong.** "Most teams see faster onboarding" cannot be cited. "In our 69-question test across 14 niches, 42% of answers named no vendor at all" can.
- **Date it and keep it dated.** Engines discount undated pages in fast-moving categories, and this is one.
- **One page per question, updated, not a new page each quarter.** Three near-duplicate posts split whatever authority the topic earns.

## After it ships

Give it two to six weeks before judging. Then re-ask the same question, in the same engines, the same number of times, and check three things: is the brand named now, is the new page cited, and did the previously cited pages change. A page that is cited but does not move presence is usually a positioning problem, not a content one.

If the page is not picked up at all, the likeliest causes in order are: it is not indexed, the site blocks a crawler, the question was not contested in the first place, or the page says nothing the cited pages do not.

## With the Peak Answer MCP connected

`my_questions` with `only_losing` gives the gap list with the winner named, and `my_visibility` gives the measured before-and-after rather than an impression of one. `generate` with `content_brief` produces a brief in the shape above for a specific question, and with `faq_schema` produces valid `FAQPage` JSON-LD from a page's real questions.

Free, no signup: https://peakanswer.com/tools/prompt-gap-checker
