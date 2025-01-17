# Github Actions

This repo contains my personal github actions.
Just copy the .github/workflows/\* into the /.github/workflows directory and push.

Note that this repo has actions disabled so they don't run.

## Generate README

This action generates a README.md file from a template.
It also counts the number of lines of code in the repo.
If no template yet exists, it copies the output file as the template.
This means that the first time you run this action, it will generate a README.md file.
All inputs are optional.

The write permission is needed to commit the README.md file.

### Example usage

```yaml
name: Generate README
on:
  push:
  pull_request:
    paths:
      - "README.md" # This isn't needed, but it's a good sanity check
      - "README.tmpl.md"
  workflow_dispatch:
jobs:
  generate-readme:
    permissions:
      contents: write
    uses: aarondill/github-actions/.github/workflows/gen-readme.yml@main
    with:
      template-file: README.tmpl.md
      output-file: README.md
      wait-for-commits: 10
      header: Lines of code
```

### Short version

```yaml
name: Generate README
on:
  push:
  pull_request: { paths: ["README.md", "README.tmpl.md"] }
  workflow_dispatch:
jobs:
  generate-readme:
    permissions: { contents: write }
    uses: aarondill/github-actions/.github/workflows/gen-readme.yml@main
```
