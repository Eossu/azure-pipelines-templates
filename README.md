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

## Stages

## Jobs

## Steps
