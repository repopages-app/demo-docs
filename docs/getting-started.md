# Getting started

Three steps connect a repository to a Confluence space.

## 1. Map the repository

Open **Confluence settings → RepoPages** and add a mapping: the repository name as your CI reports it (`owner/name`), the target space, and the folder to publish (`docs/` here). RepoPages shows the sync URL and, once, a signing secret.

## 2. Store the two secrets

In the repository, add `REPOPAGES_URL` and `REPOPAGES_SECRET` as Actions secrets. The secret never appears in the workflow file or in Confluence again.

## 3. Add the workflow

```yaml
name: RepoPages
on:
  push:
    branches: [main]
    paths: ['**/*.md']
jobs:
  sync:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 2
      - uses: repopages-app/ci@v1
        with:
          url: ${{ secrets.REPOPAGES_URL }}
          secret: ${{ secrets.REPOPAGES_SECRET }}
          prefix: docs/
```

Run the workflow once by hand with `full_import` ticked to create pages for everything that already exists. From then on every merge to `main` sends only the files the commit changed.

> **Note.** The first import of a large folder takes a minute or two. Later pushes finish in seconds because only changed files travel.
