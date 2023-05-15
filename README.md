# team-approval-action

This action will determine if a pull request has been approved by relevant teams in the calling repo's organization.
By including the provided template and adding names of teams, those teams will become required to merge pull requests moving forward.

## Example

```yaml
# This template is intended to be incorporated as a workflow in another repository for pull request gating
name: team-approval-check

on:
  pull_request:
    types: [opened, edited, synchronize, reopened]
  pull_request_review:
    types: [submitted, edited, dismissed]

jobs:
  call-workflow:
    name: Run the team approval check workflow
    runs-on: ubuntu-latest
    steps:
      - uses: open-reading-frame/team-approval-action@main
        with:
          # Teams with spaces should have double quotes around them or spaces replaced with a '-' or '_',
          # casing does not matter. i.e. Developer Experience could be listed as "developer experience"
          # or as developer-experience.
          teams: '<team 1> "<team 2>" ... <team n>'
          token: ${{ secrets.GH_REST_API_TOKEN }}
```
