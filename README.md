# deploy-nuget
A reusable workflow for deploying to NuGet.

## Installation
Add a new workflow under .github/workflows/ with the following contents.
```yml
name: Deploy

on:
  push:
    branches:
      - release/nuget

jobs:
  deploy:
    uses: Arthri/deploy-nuget/.github/workflows/deploy.yml@v1
```

## Usage
1. Create a pull request from `master` to `release/nuget`.
1. Merge pull request.
1. Expect workflow to build project and upload NuGet package to NuGet.
