# DataMatrix

## What the project does
DataMatrix is an Umbraco CMS website project (branded "DataMatrix") that runs on .NET 10. The project stores its content and configuration using a SQLite database (see `appsettings.json` for the default connection string) and includes configuration for Serilog logging. It provides a typical Umbraco-backed site and administrative UI for content editors.

## Why this project is useful
- Provides a lightweight, local-ready Umbraco site that is easy to run for development, demos, or small production sites.
- Uses SQLite for a zero-ops data store (good for development and small deployments).
- Configured for sensible defaults (logging via Serilog, content cleanup policy, email templates) so contributors can focus on features and content.

## How to get started

Prerequisites
- .NET 10 SDK
- Visual Studio 2026 (or `dotnet` CLI)
- (Optional) A browser to access the site and Umbraco backoffice

Quick start (CLI)
1. Clone the repository
   - `git clone https://github.com/PawanJangid01/DataMatrix.git`
2. Change directory
   - `cd DataMatrix`
3. Inspect configuration
   - Review `appsettings.json` and update the `ConnectionStrings:umbracoDbDSN` path if you want the SQLite DB stored elsewhere: `./appsettings.json`
4. Restore and build
   - `dotnet restore`
   - `dotnet build`
5. Run the site
   - `dotnet run --project <your-webproject>.csproj`
   - Or open the solution in Visual Studio 2026 and run (F5).
6. Complete Umbraco setup
   - If this is the first run, visit the site in a browser and follow Umbraco setup steps (you will create an admin user and accept the DB connection).

Notes
- The default SQLite DB referenced in `appsettings.json` lives under `umbraco/Data/DataMatrix.sqlite.db` in this repository layout; update the path if required.
- Logging levels are configured under the `Serilog` section in `appsettings.json`.
- Common files:
  - `appsettings.json` — runtime configuration
  - `.gitignore` — ignored files for the repo

## Where to get help
- Open an issue in this repository: https://github.com/PawanJangid01/DataMatrix/issues
- For Umbraco-specific questions:
  - Umbraco docs: https://our.umbraco.com/documentation/
  - Community: https://our.umbraco.com/
- For .NET questions:
  - https://docs.microsoft.com/dotnet

## Who maintains and contributes
- Maintainer: Repository owner at https://github.com/PawanJangid01
- Contributing
  - Please open issues for bugs and feature requests.
  - Submit pull requests against `main`. Keep changes focused and include a short description of what and why.
  - Follow .NET 10 coding conventions; prefer consistent formatting and meaningful commit messages.
  - If you plan a larger change, open an issue first to discuss the approach.

## Project structure (high level)
- `umbraco/` — Umbraco site files and local DB (referenced in `appsettings.json`)
- `appsettings.json` — application settings (logging, Umbraco settings, connection strings)
- `.gitignore` — repository ignore rules

If you want, I can:
- Add a `CONTRIBUTING.md` with recommended workflow and pre-commit checks.
- Add a simple developer script (`scripts/run-dev.ps1` or `run-dev.sh`) to standardize starting the site.
