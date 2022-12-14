# QuantCDN Search

Manage a Quant Search index using Github Actions.

## Getting Started

To get started using the action make sure you have the standard workflow structure set up (.github/workflows) create a file called `search.yml` with the following contents.

```
name: Add/update search records in QuantCDN
on:
  push:
    branches:
      - master
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      # Build the artefact or restore a cached copy.
      # - name: Build the deploy artefact
      #   run: npm run build
      - uses: quantcdn/search-action@v2
        with:
          customer: <quant-customer-id>
          project: <quant-project-id>
          token: $({ secrets.QUANT_TOKEN })
          operation: [status|index|unindex|clear]
          index-path: <path-to-json-files>
          unindex-path: <url-path>

```

Replace the placeholders with values for your project, these can be found in the [Quant dashboard](https://docs.quantcdn.io/docs/dashboard).

## Adding secrets

Navigate to your repositories Settings page and find **Secrets**. Once there click on new secret, enter **QUANT_TOKEN** as the secret name and paste your provided Quant API token.

You can learn more about [secrets](https://docs.github.com/en/actions/reference/encrypted-secrets) and [actions](https://docs.github.com/en/actions).

## Inputs

```
endpoint:
  description: 'Specify the QuantCDN API endpoint'
  required: false
  default: 'https://api.quantcdn.io'
customer:
  description: 'Your customer account name'
  required: true
project:
  description: 'Your project name'
  required: true
token:
  description: 'Your API token'
  required: true
operation:
  description: 'The search operation to perform'
  required: true
index-path:
  description: 'The path on disk to json files containing search records'
  required: false
unindex-path
  description: 'The URL path (e.g /about) to remove from the search index'
  required: false
```
