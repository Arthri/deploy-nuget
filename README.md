# deploy-nuget
A reusable workflow for deploying to NuGet.

## Installation
1. Add a new workflow under .github/workflows/ with the following contents.
    ```yml
    name: Deploy

    on:
      push:
        branches:
          - release/nuget

    jobs:
      deploy:
        uses: Arthri/deploy-nuget/.github/workflows/deploy.yml@v1
        secrets:
          NUGET_API_KEY: ${{ secrets.NUGET_API_KEY }}
    ```
2. Create a new environment named `NuGet (Stable)` with a secret named `NUGET_API_KEY` containing the API key used to publish packages to NuGet.

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

### Set Release Notes or Changelog
```yml
jobs:
  deploy:
    uses: Arthri/deploy-nuget/.github/workflows/deploy.yml@v1
    with:
      changelog: |
        - Added this
        - Removed that
```

### Specify Environment Name
By default, the workflow acquires `NUGET_API_KEY` from an environment named `NuGet (Stable)`. The environment name can be changed using the `environment_name` parameter.
```yml
jobs:
  deploy:
    uses: Arthri/deploy-nuget/.github/workflows/deploy.yml@v1
    with:
      environment_name: Custom Environment Name
```

### Specify Project
By default, the workflow builds the singular solution or csproj in the repository's root. If there is more than one solution or project in the root, a project must be specified manually using the `project_path` parameter.
```yml
jobs:
  deploy:
    uses: Arthri/deploy-nuget/.github/workflows/deploy.yml@v1
    with:
      project_path: ./src/Test.App/Test.App.csproj
```

### Disable Version Sanitization
By default, the inputted version will be sanitized to remove the `v` prefix and any directories. For example, `a/b/c/v1.0.0` will turn into `1.0.0`, and `v1.2.3` will turn into `1.2.3`. Sanitization is configurable. The following example demonstrates disabling version sanitization.
```yml
jobs:
  deploy:
    uses: Arthri/deploy-nuget/.github/workflows/deploy.yml@v1
    with:
      sanitize_version: false
```

### Set Version
By default, the package's version will be set to the `$(Version)` property of a project. It can be overriden using configuration options.
```yml
jobs:
  deploy:
    uses: Arthri/deploy-nuget/.github/workflows/deploy.yml@v1
    with:
      version: v1.0.0
```
