# Manuel - Morales | Clean Architecture Template

## Tools and Technologies Needed

- [Dotnet 9.0 SDK](https://dotnet.microsoft.com/download)
- [node.js](https://nodejs.org/en/)
- [pnpm](https://pnpm.io/)
- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)

## Pending Implementations

```csharp
// TODO: Add API title for Swagger
builder.Services.AddSwaggerGenWithAuth("Clean Architecture API");
```

In the `Presentation` project, you'll find the `Program`. You can add the API
title and description to the Swagger documentation.

```json
{
  "name": "api",
  "version": "3.11.0",
  "private": false,
  "description": "A template for building clean, testable APIs with ASP.NET Core",
  "scripts": {
    "dev": "dotnet watch --project ./src/Presentation/ run",
    "restore": "dotnet restore",
    "build": "dotnet build --configuration Release --no-restore",
    "publish": "dotnet publish --configuration Release --no-restore --no-build",
    "migrate:add": "dotnet ef migrations --project ./src/Infrastructure/ --startup-project ./src/Presentation/ add",
    "ef:install": "dotnet tool install --global dotnet-ef",
    "ef:bundle": "dotnet ef migrations bundle --configuration HealthChecks__Enabled=false --force --project ./src/Infrastructure/ --startup-project ./src/Presentation/ --output efbundle",
    "prepare": "husky"
  },
  "devDependencies": {
    "@commitlint/cli": "^19.5.0",
    "@semantic-release/changelog": "^6.0.3",
    "@semantic-release/commit-analyzer": "^12.0.0",
    "@semantic-release/git": "^10.0.1",
    "@semantic-release/github": "^10.0.5",
    "@semantic-release/npm": "^12.0.1",
    "@semantic-release/release-notes-generator": "^13.0.0",
    "commitizen": "^4.3.1",
    "cz-conventional-changelog": "^3.3.0",
    "husky": "^9.1.6",
    "semantic-release": "^23.1.1"
  },
  "config": {
    "commitizen": {
      "path": "./node_modules/cz-conventional-changelog"
    }
  }
}
```

Update the version of the API in the `package.json` file to 0.1.0. to reset the
version of the API. Update the description of the API in the `package.json` with
your own description. Update any other fields in the `package.json` file as
needed.

Remove `CHANGELOG.md` file to reset the changelog record.

Remove `LICENSE` file to reset the license, use your own license.

## Set Production Migrations

For production, you can use the `ef:bundle` command to bundle the migrations
into a single migration. This will allow you to deploy the application with a
single migration file. To execute the command, run the following:

```sh
pnpm ef:bundle
```

To execute this in a CI/CD pipeline, only uncomment this:

```yaml
# TODO: If you are going to Deploy your API, you can run the migrations here for your production database
# Only you need to add the connection string to your secrets
# - name: Run EF Migrations
#   run: ./efbundle --connection "${{ secrets.DB_CONNECTION_STRING }}"
```

In the `.github/workflows/release.yml` file, uncomment the section that runs the
migrations and set you DB_CONNECTION_STRING in your GitHub Secrets.

### Commands

- **dev**: Initializes the .NET project in Development configuration.

  ```sh
  pnpm dev
  ```

- **restore**: Restores the .NET project dependencies.

  ```sh
  pnpm restore
  ```

- **build**: Builds the .NET project in Release configuration without restoring
  dependencies.

  ```sh
  pnpm build
  ```

- **publish**: Publishes the .NET project in Release configuration without
  restoring or building.

  ```sh
  pnpm publish
  ```

- **migrate:add**: Adds a new migration to the `Infrastructure` project.

  ```sh
  pnpm migrate:add <MigrationName>
  ```

- **ef:install**: Installs the Entity Framework CLI tool.

  ```sh
  pnpm ef:install
  ```

- **ef:bundle**: Bundles the migrations into a single migration.

  ```sh
  pnpm ef:bundle
  ```

- **prepare**: Sets up Husky for managing Git hooks.

  ```sh
  pnpm prepare
  ```

## Ports - localhost

- **API**: 5001
  - **Swagger**: /swagger/index.html
- **Postgres**: 5432
- **Redis**: 6379
- **Papercut**: 8080
- **Seq**: 8081
