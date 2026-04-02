# SignalHub — First Implementation Sprint v1

## Goal
Turn planning into code immediately.
This sprint is the shortest path from zero to a running enterprise-shaped app skeleton.

---

# Sprint Outcome
By the end of this first sprint, you should have:
- .NET solution created
- project references wired
- Razor app running
- domain entities created
- EF Core configured
- Postgres connection working
- first migration created
- seed data loaded
- dashboard and partnerships list page stubbed

If those exist, the project is real.

---

# Sprint Tasks

## Task 1 — Create the .NET solution
Create:
- solution file
- web project
- application project
- domain project
- infrastructure project
- integrations project
- unit test project
- integration test project

### Done when
- all projects exist
- solution opens cleanly
- references are valid

---

## Task 2 — Wire project references
Recommended direction:
- Web -> Application, Infrastructure
- Application -> Domain
- Infrastructure -> Application, Domain
- Integrations -> Application, Domain
- Tests -> relevant projects

### Done when
- solution builds

---

## Task 3 — Create domain entities
Start with:
- PartnershipRecord
- ApprovalHistory
- OperationalIssue
- IntegrationJobLog
- enums

### Done when
- classes compile
- status enums exist

---

## Task 4 — Set up Infrastructure and DbContext
Create:
- SignalHubDbContext
- DbSets
- entity config or fluent config

### Done when
- app can connect to DB
- migration can be generated

---

## Task 5 — Configure Postgres
Add:
- EF Core provider
- connection string config
- local environment config

### Done when
- `dotnet ef migrations add InitialCreate` works
- `dotnet ef database update` works

---

## Task 6 — Seed sample data
Seed:
- sample users/roles
- sample partnerships
- sample statuses
- sample issues

### Done when
- list page has meaningful demo data

---

## Task 7 — Create the base Razor layout
Build:
- nav menu
- dashboard placeholder
- partnerships section link
- issues/integrations/report placeholders

### Done when
- app feels like an internal portal, not a blank template

---

## Task 8 — Build first real page: Partnerships Index
Show:
- creator name
- sponsor
- status
- projected value
- last sync

### Done when
- table renders seeded records cleanly

---

## Task 9 — Build simple dashboard summary
Show cards for:
- active partnerships
- pending approvals
- unresolved issues
- failed syncs

### Done when
- dashboard displays calculated values

---

# Suggested Branch / Commit Rhythm
Make small commits like:
- scaffold solution structure
- add domain entities and enums
- configure EF Core and Postgres
- add initial migration
- seed sample data
- add partnerships index page
- add dashboard summary cards

This helps you tell the build story later.

---

# What to Ignore in Sprint 1
Do **not** get stuck on these yet:
- perfect auth
- production hosting
- advanced CI/CD
- Terraform polish
- fancy CSS
- mock SaaS implementation depth
- perfect tests

Sprint 1 is about reality, not polish.

---

# What to Do Right After Sprint 1
Once sprint 1 is done, move to:
1. partnership detail page
2. edit/create flow
3. approval workflow
4. audit history
5. first mock integration

---

# Final Reminder
The project becomes valuable the moment it:
- runs
- has real entities
- uses a real DB
- shows business data in a believable internal UI

Do not wait for elegance before getting to running software.
