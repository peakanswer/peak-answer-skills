# Contributing

Corrections are welcome, particularly to anything that has gone stale: a crawler user agent that
changed, a claim about an engine that is no longer true, a tool URL that moved.

## A skill

One directory under `skills/`, one `SKILL.md` in it, YAML front matter with `name` and
`description` and nothing else.

The `description` is how an agent decides to load the skill, so write it as the situations it
applies to, not as a summary. "Use when someone asks why ChatGPT does not cite their site" beats
"A skill about AI search".

## What belongs in the body

- Checks in the order they depend on each other, so nothing below a blocking failure is reported.
- The failure modes that look fine: the `Disallow:` with no path, the empty `<div id="root">`, the
  valid-looking JSON-LD that does not parse.
- The caveat. If something is contested, say it is. `llms.txt` is a proposal, a blocked crawler is
  sometimes deliberate, and presence in an answer is not traffic.
- What the agent should report, with the fix beside each finding.

## What does not

- Claims that cannot be checked. No invented percentages, no "studies show".
- Anything presented as a ranking factor that no engine has confirmed.
- Product pitches. A skill may name the tools that do the same job with measured data, in one
  section at the end, after the skill stands on its own without them.

## Before opening a pull request

Read the skill back as an agent would with no other context. If a step needs something the skill
did not say, it is missing. Keep line length reasonable and use plain markdown.
