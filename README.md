# GitHub action with python & poetry

A GitHub action that installs Python of certain version and Poetry package manager


## Usage

Use `mishaga/action-poetry@1` step in your workflow

```yaml
- uses: mishaga/action-poetry@1
  with:
    python-version: "3.12"   # a version of python; required
    poetry-version: "latest" # a version of poetry; optional, default: "latest"
    shell: "bash"            # which shell to use; optional, default: "bash"
```


### Example for `pytest`

```yaml
name: CI/CD

on:
  push

jobs:
   test:
     runs-on: ubuntu-latest
     strategy:
       matrix:
         python-version: ["3.9", "3.10", "3.11", "3.12"]
     steps:
       - name: Checkout
         uses: actions/checkout@v4

       - name: Set up Python & Poetry
         uses: mishaga/action-poetry@1
         with:
           python-version: ${{ matrix.python-version }}

       - name: Install dependencies
         run: poetry install

       - name: Testing code with pytest
         run: poetry run pytest -v
```
