# azure-pipelines-templates

Azure Pipelines templates for my repos here at github.

**Note:** this is created for my personal use so its not necessary a stable repository.

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

Then reference templates as `<language>/<template-type>/<template>.yaml@templates`

## Languages

- [Python](docs/python.md)
