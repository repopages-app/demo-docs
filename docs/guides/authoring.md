# Writing pages

Write ordinary Markdown. These conventions make the Confluence result predictable.

## Titles

The page title is, in order: the `title` field in front matter, the first level-one heading, the file name. Keep one level-one heading per file and let it be the title.

## Links and images

Link to other pages with relative paths, `[Diagrams](diagrams.md)` or `[Getting started](../getting-started.md)`. They become Confluence page links, so they survive page moves. Images referenced with relative paths are uploaded as attachments.

## What converts

| Markdown | Confluence |
|---|---|
| Headings, paragraphs, emphasis, lists | The same |
| Tables | Tables |
| Fenced code with a language | Code block with syntax highlighting |
| Blockquotes starting with **Note** or **Warning** | Info and warning panels |
| Task lists | Task lists |
| `mermaid` and `plantuml` fences | Rendered images, see [Diagrams](diagrams.md) |

## What to avoid

- Raw HTML. It is dropped.
- Headings as the only content of a file. An empty page is still a page.
- Two files with the same title in one folder. The second gets the path appended to stay unique.
