# deploy_nuget
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
    uses: Arthri/deploy_nuget/.github/workflows/deploy.yml@v1
```

## Usage
1. Create a pull request from `master` to `release/nuget`.
1. Merge pull request.
1. Expect workflow to build project and upload NuGet package to NuGet.

### Creating the NuGet Environment
1. Head to your repository's settings tab.
1. Go to `Code and automation > Environments`.
1. Create a new environment named `NuGet (Stable)`.
1. Configure environment.
1. Add a secret named `NUGET_API_KEY`

### Specify Environment Name
By default, the workflow acquires `NUGET_API_KEY` from an environment named `NuGet (Stable)`. The environment name can be changed using the `environment_name` parameter.
```yml
jobs:
  deploy:
    uses: Arthri/deploy_nuget/.github/workflows/deploy.yml@v1
    with:
      environment_name: Custom Environment Name
```

### Specify Project
By default, the workflow builds the singular solution or csproj in the repository's root. If there is more than one solution or project in the root, a project must be specified manually using the `project_path` parameter.
```yml
jobs:
  deploy:
    uses: Arthri/deploy_nuget/.github/workflows/deploy.yml@v1
    with:
      project_path: ./src/Test.App/Test.App.csproj
```
