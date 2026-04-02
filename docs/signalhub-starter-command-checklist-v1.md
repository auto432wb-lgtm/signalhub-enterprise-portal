# SignalHub — Starter Command Checklist v1
## Copy-Paste Commands for Initial .NET Solution Setup

## Purpose
This file is the fastest path from planning docs to a real local project scaffold.

Use these commands inside the root of:
- `signalhub-enterprise-portal`

Assumption:
- .NET SDK is installed
- Git is installed
- you are using PowerShell on Windows

---

# 1. Go to repo root
```powershell
cd path\to\signalhub-enterprise-portal
```

---

# 2. Create the solution file
```powershell
dotnet new sln -n SignalHub
```

---

# 3. Create application projects
## Web project
```powershell
dotnet new webapp -n SignalHub.Web -o .\src\SignalHub.Web
```

## Class libraries
```powershell
dotnet new classlib -n SignalHub.Application -o .\src\SignalHub.Application
dotnet new classlib -n SignalHub.Domain -o .\src\SignalHub.Domain
dotnet new classlib -n SignalHub.Infrastructure -o .\src\SignalHub.Infrastructure
dotnet new classlib -n SignalHub.Integrations -o .\src\SignalHub.Integrations
```

## Test projects
```powershell
dotnet new xunit -n SignalHub.UnitTests -o .\tests\SignalHub.UnitTests
dotnet new xunit -n SignalHub.IntegrationTests -o .\tests\SignalHub.IntegrationTests
```

---

# 4. Add projects to the solution
```powershell
dotnet sln .\SignalHub.sln add .\src\SignalHub.Web\SignalHub.Web.csproj
dotnet sln .\SignalHub.sln add .\src\SignalHub.Application\SignalHub.Application.csproj
dotnet sln .\SignalHub.sln add .\src\SignalHub.Domain\SignalHub.Domain.csproj
dotnet sln .\SignalHub.sln add .\src\SignalHub.Infrastructure\SignalHub.Infrastructure.csproj
dotnet sln .\SignalHub.sln add .\src\SignalHub.Integrations\SignalHub.Integrations.csproj
dotnet sln .\SignalHub.sln add .\tests\SignalHub.UnitTests\SignalHub.UnitTests.csproj
dotnet sln .\SignalHub.sln add .\tests\SignalHub.IntegrationTests\SignalHub.IntegrationTests.csproj
```

---

# 5. Add project references
## Web references
```powershell
dotnet add .\src\SignalHub.Web\SignalHub.Web.csproj reference .\src\SignalHub.Application\SignalHub.Application.csproj
dotnet add .\src\SignalHub.Web\SignalHub.Web.csproj reference .\src\SignalHub.Infrastructure\SignalHub.Infrastructure.csproj
```

## Application references
```powershell
dotnet add .\src\SignalHub.Application\SignalHub.Application.csproj reference .\src\SignalHub.Domain\SignalHub.Domain.csproj
```

## Infrastructure references
```powershell
dotnet add .\src\SignalHub.Infrastructure\SignalHub.Infrastructure.csproj reference .\src\SignalHub.Application\SignalHub.Application.csproj
dotnet add .\src\SignalHub.Infrastructure\SignalHub.Infrastructure.csproj reference .\src\SignalHub.Domain\SignalHub.Domain.csproj
```

## Integrations references
```powershell
dotnet add .\src\SignalHub.Integrations\SignalHub.Integrations.csproj reference .\src\SignalHub.Application\SignalHub.Application.csproj
dotnet add .\src\SignalHub.Integrations\SignalHub.Integrations.csproj reference .\src\SignalHub.Domain\SignalHub.Domain.csproj
```

## Unit test references
```powershell
dotnet add .\tests\SignalHub.UnitTests\SignalHub.UnitTests.csproj reference .\src\SignalHub.Application\SignalHub.Application.csproj
dotnet add .\tests\SignalHub.UnitTests\SignalHub.UnitTests.csproj reference .\src\SignalHub.Domain\SignalHub.Domain.csproj
```

## Integration test references
```powershell
dotnet add .\tests\SignalHub.IntegrationTests\SignalHub.IntegrationTests.csproj reference .\src\SignalHub.Web\SignalHub.Web.csproj
dotnet add .\tests\SignalHub.IntegrationTests\SignalHub.IntegrationTests.csproj reference .\src\SignalHub.Infrastructure\SignalHub.Infrastructure.csproj
```

---

# 6. Initial NuGet packages
## Infrastructure packages
```powershell
dotnet add .\src\SignalHub.Infrastructure\SignalHub.Infrastructure.csproj package Microsoft.EntityFrameworkCore
dotnet add .\src\SignalHub.Infrastructure\SignalHub.Infrastructure.csproj package Microsoft.EntityFrameworkCore.Design
dotnet add .\src\SignalHub.Infrastructure\SignalHub.Infrastructure.csproj package Npgsql.EntityFrameworkCore.PostgreSQL
```

## Web packages (only if needed later for Identity or other features)
```powershell
# add packages here later as needed
```

## Tooling package for EF CLI if needed
```powershell
dotnet tool install --global dotnet-ef
```

---

# 7. Build everything
```powershell
dotnet build .\SignalHub.sln
```

Expected result:
- solution builds successfully
- no broken references

---

# 8. Run the web app
```powershell
dotnet run --project .\src\SignalHub.Web\SignalHub.Web.csproj
```

Expected result:
- Razor Pages starter app launches locally

---

# 9. First commit suggestion
```powershell
git add .
git commit -m "Bootstrap SignalHub .NET solution structure"
```

---

# 10. Immediate next coding tasks
After the project boots, move to:
1. create domain entities in `SignalHub.Domain`
2. create `SignalHubDbContext` in `SignalHub.Infrastructure`
3. configure Postgres connection in the web app
4. create initial migration
5. seed sample data
6. build partnerships list page
7. build dashboard cards

---

# Optional: PostgreSQL local setup note
If Postgres is not already running locally, you can:
- install it locally
- run it via Docker

### Example docker run
```powershell
docker run --name signalhub-postgres -e POSTGRES_PASSWORD=postgres -e POSTGRES_USER=postgres -e POSTGRES_DB=signalhub -p 5432:5432 -d postgres
```

Then use a connection string like:
```text
Host=localhost;Port=5432;Database=signalhub;Username=postgres;Password=postgres
```

---

# Recommended First Milestone Definition
You are done with setup when:
- solution exists
- projects exist
- references are correct
- solution builds
- web app runs
- Postgres decision is made
- EF packages are installed

At that point, the project has officially moved from planning into implementation.
