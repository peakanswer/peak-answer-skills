# Peak Answer skills

Five agent skills for generative engine optimisation: getting a brand recommended when a buyer asks
ChatGPT, Claude, Perplexity, Gemini or Google AI Mode for one.

They are plain `SKILL.md` files. Claude Code, the Claude apps and anything else that reads the
[agent skills](https://code.claude.com/docs/en/skills) format can use them, and they work without
any account, key or connection. Each one names the Peak Answer MCP tools that do the same job with
measured data, at the end, in a section you can ignore.

| Skill | Use it when |
| --- | --- |
| [`geo-audit`](skills/geo-audit/SKILL.md) | Someone asks why an engine does not cite their site, or wants a GEO baseline |
| [`ai-visibility-check`](skills/ai-visibility-check/SKILL.md) | Measuring whether engines recommend a brand, and who wins instead |
| [`answer-readiness`](skills/answer-readiness/SKILL.md) | Shaping a page so a model can lift an answer out of it |
| [`answer-gap-content`](skills/answer-gap-content/SKILL.md) | Deciding what to write about a question you lose, and briefing it |
| [`llms-txt`](skills/llms-txt/SKILL.md) | Writing or reviewing an `llms.txt` |

## Install

Copy a skill into your skills directory:

```bash
git clone https://github.com/peakanswer/peak-answer-skills.git
cp -r peak-answer-skills/skills/geo-audit ~/.claude/skills/
```

Or all five:

```bash
cp -r peak-answer-skills/skills/* ~/.claude/skills/
```

Project-scoped instead of global: put them in `.claude/skills/` in the repo. The agent picks a skill
up from its `description`, so nothing else needs configuring.

## What is in them

Checks in dependency order, the failure modes that look fine, and the caveats. A site that blocks
`GPTBot` does not have a schema problem, `llms.txt` is a proposal rather than a standard, and most
questions are lost to somebody else's listicle rather than to your own pages. Each skill says which
of the three causes it treats and points at the skill that treats the others.

## With the Peak Answer MCP

Optional. Every skill works without it. Where a skill can hand work to a measured tool, it says so:
`audit_site` for the technical pass, `my_visibility` and `my_questions` for measured history rather
than a one-off check, `generate` for `llms_txt`, `faq_schema` and content briefs.

MCP endpoint: `https://peakanswer.com/api/mcp`. Included on every plan, and the free tools at
[peakanswer.com/tools](https://peakanswer.com/tools) need no account at all.

## Licence

MIT. See [LICENSE](LICENSE).
