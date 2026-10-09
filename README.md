# RepoPages demo docs

A small documentation set that [RepoPages for Confluence](https://github.com/repopages-app/ci) publishes to Confluence on every push to `main`. The `docs/` folder is mapped to a Confluence space; the workflow in `.github/workflows/repopages.yml` is the whole integration.

Edit anything under `docs/`, push, and the matching Confluence page is updated within seconds. Rename a file and its page moves; delete a file and its page is archived.

The `docs/prompts/` folder holds the system prompts of the team's assistants, one page per prompt. Those pages may also be edited in Confluence: RepoPages marks an edited page as pending review and the edit comes back to this repository as a pull request, so nothing changes without a review here.
