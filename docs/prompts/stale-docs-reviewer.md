---
title: Stale docs reviewer
---

## Purpose

Reviews one documentation page against the current code and lists what is out of date. It runs weekly on every page whose Markdown file has not changed in **90 days** while the code it describes has, using the mapping in `AGENTS.md`.

## Owner and reviewer

- Owner: Documentation, Ivana Kovač
- Reviewer for every change: one engineer from the area the page describes

## Model and parameters

- Model: the `review` tier from the prompt service configuration
- Temperature `0`, maximum output 1,500 tokens
- One call per page; pages over 400 lines are split at level-two headings

## The prompt

```text
You review one documentation page of RepoPages against the code it describes.
You receive the page as it is in Git, the code diff since the page last changed, and
the product glossary.

List every statement in the page that the diff contradicts. For each one, quote the
sentence exactly and say in one sentence what the code does now. Quote at most two
lines of code. Never guess about behaviour the diff does not show.
Flag every term the glossary marks as renamed or removed.
Say nothing about style, grammar or structure; another review covers those.
Rate each finding high (a reader following the page will fail), medium or low (the page
is incomplete but not wrong). Use medium sparingly.
A page with no contradictions gets an empty list. That is a good result, not a failure.
```

## Inputs

- `page_markdown`: the page as it is in Git
- `diff_since_page_changed`: the code diff since the page's last commit
- `glossary`: product terms with their current names
  - Renamed terms carry their old name in `formerly`.
  - Removed terms carry `removed: true`.

## Output format

YAML with one key, `findings`: a list of entries with `quote`, `now` and `severity`. An empty list bumps the page's freshness date; any finding opens an issue assigned to the page's owner.

## Known failure modes

- Reports a contradiction for code that was added behind a feature flag and is not live yet.
- Treats the diagram source in a Mermaid fence as prose and quotes node labels as statements.
- On a split page, misses a statement whose context is in the other half. The issue lists both halves for that reason.

> **High** means a reader following the page will fail. **Low** means the page is merely incomplete.

---

Change history: see the byline on this page.
