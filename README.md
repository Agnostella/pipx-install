# pipx-install

Install and cache Python packages with `pipx` in your GitHub Actions workflows.

## Description
The `pipx-install` GitHub Action sets up a `pipx` environment, caches it, and installs specified Python packages using `pipx`. This action helps to speed up your workflows by caching the pipx environment and reusing it in subsequent runs.

## Inputs

- `package-specs` (required): The specifications of the package(s) to install with `pipx`.

## Outputs

- `cache-hit`: Indicates whether the cache was hit or not.

The following environment variables are set:

- `PIPX_HOME`
- `PIPX_MAN_DIR`
- `PIPX_BIN_DIR`

The `PIPX_BIN_DIR` is added to the PATH for later steps.

## Usage

Here is an example of how to use the `pipx-install` action in your workflow:

```yaml
name: Example Workflow

on: [push, pull_request]

permissions:
  contents: read

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Use Python 3.12
        uses: actions/setup-python@v5
        with:
          python-version: '3.12'

      - name: Install and cache packages with pipx
        uses: agnostella/pipx-install@<sha>
        with:
          package-specs: >-
            'package-1==1.0.0'
            'package-2>=2.0.0<3.0.0'

      - name: Run your application
        run: your-command
```
