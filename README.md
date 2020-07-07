# azure-pipelines-templates

Azure Pipelines tempaltes for my repos here at github.

**Note:** this is created for my personal use so not necessary a stable repository.

## Setup

Add a service connection to Azure DevOps and name it `github`:

``` yaml
Project settings
  - Service connections
    - New service connection
      - GitHub
```

Then add this at the beginning of the pipeline configurations for the diffrent pipelines:

``` yaml
resources:
  repositories:
    - repository: templates
      type: github
      endpoint: github
      name: eossu/azure-pipelines-templates
      ref: refs/tags/1.0
```

Then reference themplates as `path-to-tempalte/template.yaml@templates`

## Python

Python templates for Azure pipelines

### Jobs

Templates for Azure Pipelines jobs.

#### `python/jobs/sdk-check.yaml`

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

#### `python/jobs/sdk-test.yaml`

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

#### `python/jobs/sdk-publish.yaml`

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

### Steps

Templates for Azure Pipelines steps.

#### `python/steps/provision.yaml`

Setup a Python runtime and a cache for poetry dependencies (pip).

Example:

``` yaml
steps:
  - template: python/steps/provision.yaml@templates
    parameters:
      pythonVersion: "3.8"
```

#### `python/steps/install.yaml`

Install the poetry packages by using the lock file.

Example:

``` yaml
steps:
  - template: python/steps/install.yaml@templates
    parameters:
      pythonVersion: "3.8"
```

#### `python/steps/test.yaml`

Run tests by using pytest

``` yaml
steps:
  - template: python/steps/test.yaml@templates
    parameters:
      pythonVersion: "3.8"
      coverage: true # optional
```
