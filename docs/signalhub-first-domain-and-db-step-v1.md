# SignalHub — First Domain + DB Step v1

## Purpose
This doc tells you exactly what to build immediately after finishing the starter command checklist.

Goal:
- create the first domain entities
- create enums
- create DbContext
- prepare for the initial migration

This is the next step that turns the scaffold into an actual application.

---

# What to do first after the checklist
In this order:
1. create enums in `SignalHub.Domain`
2. create domain entity classes in `SignalHub.Domain`
3. create `SignalHubDbContext` in `SignalHub.Infrastructure`
4. register the DbContext in `SignalHub.Web`
5. add the connection string
6. run the first migration
7. update the database

---

# Recommended Folder Structure Inside Domain

Create folders like:

```text
src/SignalHub.Domain/
  Entities/
  Enums/
```

And in Infrastructure:

```text
src/SignalHub.Infrastructure/
  Persistence/
```

---

# Step 1 — Create Enums
Create these first.
They make the rest of the model much easier.

## `PartnershipStatus.cs`
Values:
- Draft
- PendingOperationsReview
- PendingBusinessApproval
- Approved
- Rejected
- OnHold
- NeedsDataFix

## `PaymentStatus.cs`
Values:
- NotStarted
- Pending
- Paid
- Overdue
- Failed

## `IssueSeverity.cs`
Values:
- Low
- Medium
- High
- Critical

## `IssueStatus.cs`
Values:
- Open
- InProgress
- Blocked
- Resolved
- Closed

---

# Step 2 — Create Domain Entities
Start with the minimum set below.

## Entity 1 — PartnershipRecord
### Why start here
This is the core business object of the whole application.

### Suggested fields
- `Guid Id`
- `string CreatorName`
- `string? ExternalCreatorId`
- `string? ExternalCampaignId`
- `string Category`
- `string SchoolOrTeam`
- `string SponsorName`
- `PartnershipStatus Status`
- `DateTime ContractStartDate`
- `DateTime ContractEndDate`
- `decimal ProjectedValue`
- `PaymentStatus PaymentStatus`
- `DateTime? LastSyncAt`
- `string? Notes`

### Notes
Keep this first version simple.
Do not over-model everything yet.

---

## Entity 2 — ApprovalHistory
### Purpose
Track workflow state changes.

### Suggested fields
- `Guid Id`
- `Guid PartnershipRecordId`
- `PartnershipStatus PreviousStatus`
- `PartnershipStatus NewStatus`
- `string ChangedBy`
- `DateTime ChangedAt`
- `string? Reason`

---

## Entity 3 — OperationalIssue
### Purpose
Represent exceptions, bad syncs, and data problems.

### Suggested fields
- `Guid Id`
- `string IssueType`
- `IssueSeverity Severity`
- `IssueStatus Status`
- `string? AssignedTo`
- `string RelatedEntityType`
- `string RelatedEntityId`
- `DateTime CreatedAt`
- `DateTime? ClosedAt`
- `string? Notes`

---

## Entity 4 — IntegrationJobLog
### Purpose
Track sync attempts and failures.

### Suggested fields
- `Guid Id`
- `string IntegrationName`
- `DateTime StartedAt`
- `DateTime? EndedAt`
- `bool Success`
- `int RecordsProcessed`
- `string? ErrorMessage`

---

# Step 3 — Example file layout

```text
src/SignalHub.Domain/
  Entities/
    PartnershipRecord.cs
    ApprovalHistory.cs
    OperationalIssue.cs
    IntegrationJobLog.cs
  Enums/
    PartnershipStatus.cs
    PaymentStatus.cs
    IssueSeverity.cs
    IssueStatus.cs
```

---

# Step 4 — Create DbContext
In:
- `src/SignalHub.Infrastructure/Persistence/SignalHubDbContext.cs`

## DbSets to add
- `DbSet<PartnershipRecord> PartnershipRecords`
- `DbSet<ApprovalHistory> ApprovalHistories`
- `DbSet<OperationalIssue> OperationalIssues`
- `DbSet<IntegrationJobLog> IntegrationJobLogs`

### Suggested constructor pattern
Use standard EF Core DbContext options constructor.

### Optional first pass
You can start without fluent configurations if needed and add them later.
That is fine for getting moving.

---

# Step 5 — Register DbContext in Web App
In `Program.cs` of `SignalHub.Web`:
- add the DbContext registration
- use Npgsql provider
- read connection string from configuration

You’ll also likely want:
- `builder.Services.AddRazorPages();`
- standard service setup

---

# Step 6 — Add Connection String
In `appsettings.json` (or `appsettings.Development.json`):

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Host=localhost;Port=5432;Database=signalhub;Username=postgres;Password=postgres"
  }
}
```

Adjust if your local setup differs.

---

# Step 7 — First Migration Commands
After entities + DbContext + registration are in place, run:

```powershell
dotnet ef migrations add InitialCreate --project .\src\SignalHub.Infrastructure\SignalHub.Infrastructure.csproj --startup-project .\src\SignalHub.Web\SignalHub.Web.csproj
```

Then:

```powershell
dotnet ef database update --project .\src\SignalHub.Infrastructure\SignalHub.Infrastructure.csproj --startup-project .\src\SignalHub.Web\SignalHub.Web.csproj
```

If that works, your app officially has a real database-backed model.

---

# Step 8 — What success looks like
You are done with this stage when:
- enums exist
- domain entities compile
- DbContext compiles
- connection string is configured
- migration is created
- database update succeeds

That is the moment the project goes from “solution shell” to “real business app foundation.”

---

# What comes next after this step
Do these next:
1. seed a few sample `PartnershipRecord` rows
2. create a `Partnerships/Index` Razor page
3. query records from the DbContext
4. display them in a table
5. create a simple dashboard count view

That should be your immediate post-database milestone.

---

# Important advice
Do not get stuck trying to make the perfect domain model on day one.
You only need enough structure to:
- create data
- store data
- display data
- evolve it later

Shipping a clean first model is better than inventing a giant perfect one.
