# semantic-release-action
Action to run semantic-release with deps for semantic-release-config preinstalled

## Usage

```yml
name: Main

on:
  push:
    branches:
      - "*"
  pull_request:

jobs:
  build:
    name: Build
    runs-on: ubuntu-latest
    steps:
        # some build steps
  release:
    name: Release
    runs-on: ubuntu-latest
    needs: [build]
    if: ${{ github.event_name == 'push' }}
    steps:
      - name: Checkout
        uses: actions/checkout@v2
        with:
          fetch-depth: 0
          persist-credentials: false
      - name: Semantic Release
        uses: sitkoru/semantic-release-action@v1
        env:
          GH_TOKEN: # GH TOKEN
          # other semantic-release env variables
```