# Configuration reference

## Mapping (Confluence settings → RepoPages)

| Field | Required | Meaning |
|---|---|---|
| Repository | yes | `owner/name` exactly as the CI reports it |
| Confluence space | yes | Target space |
| Parent page | no | Pages go below this page; otherwise a root page named after the repository is created |
| Path prefix | no | The folder to publish, `docs/`. Empty means the whole repository |
| Include patterns | no | Globs, one per line. Default: everything under the prefix |
| Exclude patterns | no | Globs, one per line. Matching files are never published, whatever the CI sends |

## Action inputs (`repopages-app/ci@v1`)

| Input | Default | Meaning |
|---|---|---|
| `url`, `secret` | required | From the settings screen, stored as repository secrets |
| `mode` | `push` | `push` sends the commit's changes, `import` the whole folder |
| `prefix` | `''` | Must match the mapping's path prefix |
| `force` | `false` | Rewrite unchanged pages too |
| `exclude` | `''` | Comma-separated globs left out of the payload |
| `render` | `auto` | `off` sends diagram blocks as code |

## Exit codes of the client

| Code | Meaning |
|---|---|
| 0 | Everything accepted, or nothing to send |
| 1 | A call failed after one retry |
| 2 | Configuration or renderer error, nothing sent |
| 3 | Sent, but some files failed on the Confluence side. The settings screen lists them |
