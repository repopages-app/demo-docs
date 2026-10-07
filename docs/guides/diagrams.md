# Diagrams

Mermaid and PlantUML blocks are rendered on the CI runner and attached to the page as SVG. The source stays on the page in a collapsed, searchable block underneath the image, so Confluence search still finds the words inside a diagram.

## Mermaid

```mermaid
flowchart LR
    A[Markdown in Git] --> B{Changed?}
    B -- yes --> C[Render diagrams]
    C --> D[Sign and send]
    D --> E[(Confluence page)]
    B -- no --> F[Skip]
```

## PlantUML

```plantuml
@startuml
skinparam shadowing false
class Mapping {
  repo: string
  prefix: string
  spaceId: string
}
class Page {
  path: string
  pageId: string
  hash: string
}
Mapping "1" o-- "many" Page : tracks
@enduml
```

## When a renderer is missing

The GitHub Action brings both renderers. On another runner without Chrome or Java, the push fails before sending anything, so a broken runner can never replace diagrams with code. Use the Docker image `ghcr.io/repopages-app/ci` there, or set `render: off` to publish the blocks as code on purpose.

## A block that does not render

Mermaid rejects this one on purpose. The page shows it as code with a note, the rest of the page is unaffected, and the push still succeeds.

```mermaid
flowchart LR
    A --> B --> ((unbalanced
```
