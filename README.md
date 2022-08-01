This repo is a guide for myself on how to setup Dynamic Readme, but if you are interested in doing something similar feel free to take a look

# JaxCore ReadME-Template
Uses [Dynamic Readme](https://github.com/marketplace/actions/dynamic-readme) github action.

## Use template in module repo
Create a workflow file `Dynamic-Readme.yml` with the following contents

```yml
name: "📄  Dynamic ReadME"

env:
  VS_WORKFLOW_TYPE: "dynamic-readme"

on:
  workflow_dispatch:
  push:
    branches:
      - main
    paths:
      - README.md

jobs:
  update_readme:
    name: "Render & Update ReadME"
    runs-on: ubuntu-latest
    steps:
      - name: "📥  Fetching Repository Contents"
        uses: actions/checkout@main

      - name: "💾  Github Repository Metadata"
        uses: varunsridharan/action-repository-meta@main
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

      - name: "💫  Update README.md"
        uses: "varunsridharan/action-dynamic-readme@main"
        with:
          GLOBAL_TEMPLATE_REPOSITORY: Jax-Core/ReadME-Template/Templates
          commit_message: ⏩ File Rebuilt by Github Actions - Dynamic ReadME
          files: |
            README.md
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

```

## Creating ReadME
Use `<!-- START name_of_part.mustache -->` and `<!-- END name_of_part.mustache -->` to include a part into the readme
Assets can be found in this repo

```
<!-- START Header.mustache -->
<!-- END Header.mustache -->
```
