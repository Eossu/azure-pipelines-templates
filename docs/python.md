# Python

Python templates for Azure pipelines

## Stages

Templates for Azure Pipelines stages.

### `python/stages/sdk-test.yaml`

Preconfigured stage that do `check` and `test` jobs.

``` yaml
stages:
  - template: python/stages/sdk-test.yaml@templates
    parameters:
      PythonVersion: "3.8"
```

### `python/stages/sdk-publish.yaml`

Preconfigured stage that do `publish` job based on tag.

``` yaml
stages:
  - template: python/stages/sdk-publish.yaml@templates
    parameters:
      PythonVersion: "3.8"
```

## Jobs

Templates for Azure Pipelines jobs.

### `python/jobs/sdk-check.yaml`

Checks your files with:

- black
- flake8
- mypy
- isort

Example:

``` yaml
jobs:
  - template: python/jobs/sdk-check.yaml@templates
    parameters:
      pythonVersion: "3.8"
```

### `python/jobs/sdk-test.yaml`

Runs tests by using pytest.

Example:

``` yaml
jobs:
  - template: python/jobs/sdk-test.yaml@templates
    parameters:
      jobs:
        # Minimal definition:
        py37: null

        # Complete definition:
        py38:
          coverage: true
          os: linux
          services:
            postgres: pg11
          variables:
            SOME_VARIABLE: "1.0"
```

### `python/jobs/sdk-publish.yaml`

Publish a package to pypi.

Example:
Assumes you publish on tags.

 ``` yaml
 trigger:
  - master
  - refs/tags/*

stages:
  - stage: test
    jobs: # ...
  - stage: publish
    condition: startsWith(variables['Build.SourceBranch'], 'refs/tags/')
    jobs:
      - template: python/jobs/sdk-publish.yaml@templates
        parameters:
          pypiRemote: pypi-token
 ```

## Steps

Templates for Azure Pipelines steps.

### `python/steps/provision.yaml`

Setup a Python runtime and a cache for poetry dependencies (pip).

Example:

``` yaml
steps:
  - template: python/steps/provision.yaml@templates
    parameters:
      pythonVersion: "3.8"
```

### `python/steps/install.yaml`

Install the poetry packages by using the lock file.

Example:

``` yaml
steps:
  - template: python/steps/install.yaml@templates
    parameters:
      pythonVersion: "3.8"
```

### `python/steps/test.yaml`

Run tests by using pytest

``` yaml
steps:
  - template: python/steps/test.yaml@templates
    parameters:
      pythonVersion: "3.8"
      coverage: true # optional
```
