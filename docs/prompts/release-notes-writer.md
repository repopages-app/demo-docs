---
title: Release notes writer
---

## Purpose

Turns the pull requests merged since the last tag into release notes for the changelog page. The notes are read by Confluence admins, not developers, so they say **what changed for the reader**, not how it was built.

## Owner and reviewer

- Owner: Product, Luka Babić
- Reviewer for every change: the engineer who cuts the next release

## Model and parameters

- Model: the `writing` tier from the prompt service configuration
- Temperature `0.2`, maximum output 1,200 tokens
- Runs once per release, after the tag is pushed and before the changelog page is merged

## The prompt

```text
You write release notes for RepoPages, a Confluence app that publishes Markdown from Git.
The readers are Confluence administrators. Describe what changed for them, never how it
was implemented.

Group the changes under "Added", "Changed" and "Fixed", in that order, and leave out a
group that would be empty. Put a breaking change first and mark it "Breaking".
Skip pull requests labelled internal or chore. Dependency updates are chores unless they
fix a security advisory; test-only changes are always chores.
Write one line per change, starting with a verb in the past tense, under 120 characters,
with the pull request number at the end as (#123).
Say "page" rather than "document" and "space" rather than "workspace".
Avoid the words simply, just and easily.
If no pull request qualifies, return the single line: No user-facing changes.
```

## Inputs

- `version`: the release version, for example `5.10.0`
- `pull_requests`: title, body and labels of every pull request merged since the last tag
- `previous_notes`: the notes of the last two releases, for tone and format

## Output format

Markdown: a level-two heading with the version, then one level-three heading per group and a bulleted list under each. The result is pasted into the changelog page by the release script without edits.

## Known failure modes

- Copies the pull request title verbatim when the body is empty, which leaks internal names. The reviewer rewrites those lines.
- Counts a change twice when it was reverted and merged again in the same release.
- Misses a breaking change that is only described in a code comment. Label breaking pull requests `breaking` so the input says so.

> Readers skim. The first three words of a line should tell them whether it concerns them.

---

Change history: see the byline on this page.
