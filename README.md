# action-poetry-run-command
GitHub Action for python projects using poetry

## Description
With this action you can easily test your code using poetry and pytest with the right dependencies based of the pyproject.toml

## Action Inputs
| Input name | Description | Required | Default Value |
| --- | --- | --- | --- |
| run-command | Command to run via 'poetry run' | true | - |
| python-version | Version of python to install | false | "3.10" |
| poetry-version | Version of poetry to install | false | "1.1.14" |

## Action Outputs
| Output name | Description |
| --- | --- |
| project-version | Current project version of pyproject.toml |

## Example

#### Notes
- No code checkout is needed
- All project dependencies will be installed via 'poetry install' (may take a while)

```yml
name: Run poetry command

on:
  pull_request:
    branches: 
      - main

jobs:
  run_tests_poetry:
    runs-on: ubuntu-latest

    steps:
      - name: Test code
        id: test-code
        uses: henningwoehr/actions/poetry/run-pytest@main
        with:
          run-command: pytest
          python-version: "3.10"
          poetry-version: "1.1.14"

      - name: Project Version
        run: echo ${{ steps.test-code.outputs.project-version }}
```