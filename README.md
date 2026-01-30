# DataMatrix

A content-driven website built on Umbraco CMS targeting .NET 10. This repository contains the site configuration and runtime files to run, develop, and deploy the DataMatrix website.

## What the project does
`DataMatrix` is an Umbraco-based website that provides a CMS for creating and managing content. The project ships with:
- Umbraco CMS configuration and sensible defaults (see `appsettings.json`)
- Local SQLite database support for easy local development
- Serilog configuration for structured logging

## Why this project is useful
- Fast to get started for development, demos, and small production sites
- Low-ops local setup (SQLite) lets editors and developers iterate quickly
- Familiar Umbraco editing experience for content editors while remaining a modern .NET 10 codebase for developers

## How users can get started

Prerequisites
- .NET 10 SDK installed
- Visual Studio 2026 (recommended) or the `dotnet` CLI
- A browser to access the site and Umbraco backoffice

Quick start (CLI)
1. Clone the repository:
   - `git clone https://github.com/PawanJangid01/DataMatrix.git`
2. Change into the repository:
   - `cd DataMatrix_Github` (adjust to your clone path)
3. Inspect configuration:
   - Review and update `appsettings.json` (see `ConnectionStrings:umbracoDbDSN` for the SQLite file path).
4. Restore and build:
   - `dotnet restore`
   - `dotnet build`
5. Run the app:
   - `dotnet run --project <web-project>.csproj`
   - Or open the solution in Visual Studio 2026 and use the __Publish__ profile for local debugging
6. Complete Umbraco first-run setup:
   - Visit the site in your browser and follow the Umbraco setup (create admin user, confirm DB connection).

Helpful files
- `appsettings.json` — runtime configuration (logging, Umbraco settings, connection strings)
- `.gitignore` — ignores for Visual Studio and .NET artifacts
- `umbraco/Data/DataMatrix.sqlite.db` — default local SQLite DB path (relative to repo)

## Deployment process (publish file)
This project deploys using the published output (the "publish folder"). Use either the `dotnet` CLI or Visual Studio __Publish__ tooling to create the artifact, then copy or publish that folder to your target host.

Using the CLI (recommended for repeatable builds)
1. Produce the publish output:
   - Framework-dependent, folder `./publish`:
     - `dotnet publish -c Release -o ./publish`
   - If you need a specific runtime or self-contained deployment:
     - `dotnet publish -c Release -r win-x64 -o ./publish --self-contained false` (adjust `-r` as needed)
2. Package the publish folder (optional):
   - Zip: `Compress-Archive -Path ./publish/* -DestinationPath ./artifacts/datamatrix.zip` (PowerShell)
3. Deploy the publish folder to the host:
   - Copy the folder contents to the web server (IIS site physical path), container image, or cloud service.
   - For IIS: point the site physical path to the `publish` folder and ensure the app pool uses the correct .NET runtime.
   - For Azure App Service: use Zip Deploy, FTP or a deployment pipeline to push the `publish` folder contents.

Visual Studio publish
1. Open the web project in Visual Studio 2026.
2. Right-click the project → __Publish__.
3. Create or select a publish profile (Folder, IIS, Azure, etc.).
4. Click __Publish__ to produce the publish folder or push directly to the target.

Post-deployment checklist
- Ensure the SQLite DB file `umbraco/Data/DataMatrix.sqlite.db` (or the configured path) is present and writable by the web process.
- Verify `appsettings.json` contains production-appropriate settings (logging levels, connection strings).
- Set any environment-specific configuration via environment variables or a production `appsettings.Production.json`.
- If using a reverse proxy or TLS, ensure ports and certificates are configured correctly.

## Where users can get help
- Open an issue in this repository: `https://github.com/PawanJangid01/DataMatrix/issues`
- Umbraco docs & community:
  - https://our.umbraco.com/documentation/
  - https://our.umbraco.com/
- .NET docs: https://learn.microsoft.com/dotnet

## Who maintains and contributes
- Primary maintainer: repository owner on GitHub — `https://github.com/PawanJangid01`
- Contributing process:
  1. Fork the repository
  2. Create a branch: `git checkout -b feature/your-change`
  3. Commit and push your branch
  4. Open a pull request with a clear summary of the change
- Keep changes focused, include tests where appropriate, and update `appsettings.json` examples only when necessary.

## Troubleshooting
- Database connection errors: confirm the path and provider in `ConnectionStrings:umbracoDbDSN` inside `appsettings.json`.
- File permission errors writing the SQLite DB: ensure the deployed process user has write permissions to the DB folder.
- Missing runtime errors: ensure the target host has .NET 10 installed (or publish self-contained).

If you want, I can add:
- A `CONTRIBUTING.md` with PR checklist and code style rules
- A small `scripts/` folder with `run-dev.ps1` and `run-dev.sh` to standardize local dev start-up steps
