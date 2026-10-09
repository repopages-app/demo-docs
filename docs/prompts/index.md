---
title: Prompts
---

## Purpose

The system prompts behind the assistants the RepoPages team runs every day. Each page is one prompt, kept as a Markdown file in `docs/prompts/` and published here like every other page in this space.

The prompts are product text, not code. Support, product and docs people own them, so they are written to be read and changed by people who never open the repository.

## The prompts

- [Support reply drafter](https://github.com/repopages-app/demo-docs/blob/main/docs/prompts/support-reply-drafter.md): drafts the first answer to a support ticket. Owned by support.
- [Release notes writer](https://github.com/repopages-app/demo-docs/blob/main/docs/prompts/release-notes-writer.md): turns merged pull requests into the changelog. Owned by product.
- [Stale docs reviewer](https://github.com/repopages-app/demo-docs/blob/main/docs/prompts/stale-docs-reviewer.md): finds statements in a page that the code no longer supports. Owned by docs.

## How a prompt changes

You can change a prompt in two ways, and both end in the same review:

1. **In Git.** Open a pull request against `docs/prompts/`. The owner reviews it, the merge publishes it.
2. **Here in Confluence.** Edit the page as you would any other. RepoPages marks it _pending review_ and, within the hour, opens a pull request with your change and your name on it.
   - Until that pull request is merged, the running assistant keeps using the reviewed version.
   - If the reviewer closes it, the page goes back to the reviewed text. Your edit stays in the page history.

Either way, nothing reaches the assistants without a reviewer from the owning team.

## What every prompt page contains

- **Purpose**: what the assistant is for, in two or three sentences.
- **Owner and reviewer**: who approves a change.
- **Model and parameters**: the model setting and the sampling values the service uses.
- **The prompt**: the exact system prompt, in one code block.
- **Inputs** and **Output format**: the contract with the service that calls it.
- **Known failure modes**: what goes wrong, so a change can be checked against it.

> A prompt page that does not say who owns it is a page nobody can approve. Add the owner first.

Keep the formatting simple: headings, paragraphs, lists and one code block. Tables, images and panels cannot be sent back from Confluence to Git yet, so an edit that adds one stays on the page and is not proposed.

---

Change history: see the byline on this page.
