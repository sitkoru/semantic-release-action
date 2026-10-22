# semantic-release-action
Action to run semantic-release with deps for semantic-release-config preinstalled

## Требования

Действие устанавливает Node.js 24 и требует Actions Runner v2.327.1 или новее.
Версии пакетов semantic-release 19 и @semantic-release/github 8 сохранены.
В примере замените `<commit-sha>` на полный SHA проверенного коммита с этим обновлением.

## Usage

```yml
name: Main

on:
  push:
    branches:
      - "main"
  pull_request:

jobs:
  build:
    name: Build
    runs-on: ubuntu-latest
    steps:
      - run: echo "Add build steps here"
  release:
    name: Release
    runs-on: ubuntu-latest
    needs: [build]
    if: ${{ github.event_name == 'push' && github.ref == 'refs/heads/main' }}
    steps:
      - name: Checkout
        uses: actions/checkout@v7.0.1
        with:
          fetch-depth: 0
          persist-credentials: false
      - name: Semantic Release
        uses: sitkoru/semantic-release-action@<commit-sha>
        env:
          GH_TOKEN: # GH TOKEN
          # other semantic-release env variables
```
