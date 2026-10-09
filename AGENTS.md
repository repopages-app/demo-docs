# Agent instructions

## Documentation lives in docs/ and is published to Confluence from main
Pages are Markdown files. Diagrams are Mermaid fences. Do not edit Confluence directly:
the RepoPages workflow rewrites a page from its file on the next push.

## Code areas and the pages that describe them
- src/sync/        → docs/how-it-works.md (sequence diagram and the "What a push contains" table)
- src/settings/    → docs/getting-started.md
- src/render/      → docs/guides/diagrams.md

## Rule for every change
Before finishing a change under src/, open the pages listed for that area and check
whether they still describe the behaviour. If not, update them in the same change:
text, tables and the Mermaid diagram. If no page needs a change, say so in the PR
description with one sentence of reasoning.
