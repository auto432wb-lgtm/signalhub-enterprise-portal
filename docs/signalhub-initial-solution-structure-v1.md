# SignalHub — Initial Solution Structure v1

## Goal
Provide the initial .NET solution and project layout for implementation.

This structure is designed to feel enterprise-friendly without being over-engineered.

---

## Recommended Stack Decisions
### Application framework
- **ASP.NET Core Razor Pages**

### Database
- **PostgreSQL** for speed and accessibility

### Why Postgres first
- easy local setup
- widely used
- good enough for enterprise-style portfolio work
- avoids unnecessary Microsoft-specific friction early

If later you want stronger Microsoft-stack alignment, the project can be adapted to SQL Server.

### ORM / data access
- **Entity Framework Core**

### Auth
- ASP.NET Core Identity or simplified role-based local auth to start

### Testing
- xUnit

---

## Solution Layout

```text
signalhub-enterprise-portal/
  src/
    SignalHub.Web/
    SignalHub.Application/
    SignalHub.Domain/
    SignalHub.Infrastructure/
    SignalHub.Integrations/
  tests/
    SignalHub.UnitTests/
    SignalHub.IntegrationTests/
  infra/
    terraform/
  docs/
  scripts/
```

---

## Project Responsibilities

## 1. SignalHub.Web
### Purpose
UI layer and web entry point.

### Responsibilities
- Razor Pages
- page models
- routing
- auth/login pages
- role-based navigation
- dashboard and management screens
- view models / UI mapping

### Keep out of this project
- heavy business rules
- integration logic
- persistence details

---

## 2. SignalHub.Application
### Purpose
Application services and use-case orchestration.

### Responsibilities
- workflow logic
- business use cases
- service interfaces
- DTOs
- command/query style methods if helpful
- application-level validation

### Example services
- PartnershipService
- DashboardService
- ApprovalWorkflowService
- IssueQueueService
- IntegrationStatusService

---

## 3. SignalHub.Domain
### Purpose
Core business model.

### Responsibilities
- entities
- enums
- core business rules
- value objects if needed

### Example contents
- PartnershipRecord
- CreatorProfile
- CampaignRecord
- PaymentRecord
- ApprovalHistory
- OperationalIssue
- status enums

This project should stay clean and business-focused.

---

## 4. SignalHub.Infrastructure
### Purpose
Persistence and implementation details.

### Responsibilities
- EF Core DbContext
- entity configurations
- repository implementations if used
- data seeding
- auth persistence support
- logging support

### Example contents
- SignalHubDbContext
- migrations
- seed data services
- configuration extensions

---

## 5. SignalHub.Integrations
### Purpose
External system client logic.

### Responsibilities
- mock SaaS clients
- external DTOs
- mapping logic from external to internal models
- sync service helpers
- retry/error translation

### Example clients
- CreatorProfileApiClient
- CampaignApiClient
- PaymentsApiClient

---

## Test Projects

## SignalHub.UnitTests
### Purpose
Fast tests for:
- workflow logic
- validation rules
- status transitions
- mapping logic

## SignalHub.IntegrationTests
### Purpose
Broader tests for:
- DB interactions
- integration flows
- page/request behavior if desired

---

# Initial Entities

## PartnershipRecord
Fields:
- Id
- CreatorName
- ExternalCreatorId
- ExternalCampaignId
- Category
- SchoolOrTeam
- SponsorName
- Status
- ContractStartDate
- ContractEndDate
- ProjectedValue
- PaymentStatus
- LastSyncAt
- Notes

## CreatorProfile
- Id
- ExternalId
- Name
- Category
- SchoolOrTeam
- ReachMetric
- VerificationStatus

## CampaignRecord
- Id
- ExternalId
- CampaignName
- SponsorName
- Budget
- CampaignStatus

## PaymentRecord
- Id
- PartnershipRecordId
- Amount
- PaymentStatus
- DueDate
- PaidDate

## ApprovalHistory
- Id
- PartnershipRecordId
- PreviousStatus
- NewStatus
- ChangedBy
- ChangedAt
- Reason

## OperationalIssue
- Id
- IssueType
- Severity
- Status
- AssignedTo
- RelatedEntityType
- RelatedEntityId
- CreatedAt
- ClosedAt
- Notes

## IntegrationJobLog
- Id
- IntegrationName
- StartedAt
- EndedAt
- Success
- RecordsProcessed
- ErrorMessage

---

# Initial Enums

## PartnershipStatus
- Draft
- PendingOperationsReview
- PendingBusinessApproval
- Approved
- Rejected
- OnHold
- NeedsDataFix

## PaymentStatus
- NotStarted
- Pending
- Paid
- Overdue
- Failed

## IssueSeverity
- Low
- Medium
- High
- Critical

## IssueStatus
- Open
- InProgress
- Blocked
- Resolved
- Closed

---

# Initial Razor Pages to Build

## Authentication / access
- /Account/Login
- /Account/AccessDenied

## Core pages
- /
- /Dashboard
- /Partnerships/Index
- /Partnerships/Details
- /Partnerships/Create
- /Partnerships/Edit
- /Approvals/Index
- /Issues/Index
- /Integrations/Index
- /Reports/Index

### First milestone pages
Build these first:
1. Dashboard
2. Partnerships/Index
3. Partnerships/Details
4. Partnerships/Edit
5. Approvals/Index

---

# Initial Services to Create

## Application services
- IPartnershipService
- IDashboardService
- IApprovalWorkflowService
- IIssueQueueService
- IIntegrationStatusService

## Integration services
- ICreatorProfileClient
- ICampaignClient
- IPaymentsClient

---

# Initial Development Milestones

## Milestone 1 — App boots
- solution created
- projects wired
- Razor app runs
- basic layout works

## Milestone 2 — Data model exists
- entities added
- DbContext created
- first migration built
- sample seed data available

## Milestone 3 — Core pages work
- partnerships list/detail/edit
- dashboard summary
- auth and roles skeleton

## Milestone 4 — Workflow exists
- approval status changes
- issue tracking basics
- audit entries for updates

## Milestone 5 — Integration layer exists
- one mock API client
- one sync flow
- integration status view

---

# Recommended Implementation Order
1. create solution + projects
2. wire references
3. create domain entities/enums
4. create infrastructure DbContext
5. configure EF Core + Postgres
6. make first migration
7. seed data
8. create dashboard and partnerships pages
9. add auth/roles
10. add workflow actions
11. add first mock integration

---

# Notes on Architecture Style
Do not overcomplicate this at the start.

This should be:
- layered
- cleanly separated
- understandable
- realistic

It does **not** need to become a giant microservices architecture.
A clean modular monolith is better for this portfolio project.

---

# Final Recommendation
Start with:
- Razor Pages
- Postgres
- EF Core
- modular monolith structure
- one mock integration first

That gets you moving fast while still looking enterprise-ready.
