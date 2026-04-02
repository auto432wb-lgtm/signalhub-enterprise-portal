# SignalHub — Day-by-Day Build Plan v1
## 30-Day Enterprise Project Build Plan

## Goal
Turn the SignalHub blueprint into a realistic portfolio project that trains:
- enterprise application development
- cloud and Terraform fundamentals
- API integrations
- CI/CD and delivery
- architecture documentation
- operational thinking

This plan assumes a focused solo build with AI assistance.

---

# WEEK 1 — FOUNDATION

## Day 1 — Project framing
### Goals
- read the blueprint fully
- define the exact MVP scope
- decide database choice
- decide whether auth starts simple or with full identity integration later

### Deliverables
- scope notes
- chosen stack decisions
- first ADR draft: why Razor Pages, why this domain

## Day 2 — Repo and solution structure
### Goals
- create .NET solution
- create planned projects under `src/`
- wire references cleanly
- create first placeholder app run

### Deliverables
- solution file
- project structure
- app runs locally

## Day 3 — Domain model draft
### Goals
- define entities
- define enums/statuses
- define key workflows

### Deliverables
- domain classes or design draft
- status model
- first ER/data notes

## Day 4 — Database and persistence setup
### Goals
- configure DB provider
- create initial schema/migrations
- seed sample data approach

### Deliverables
- DB connection setup
- first migration
- seed strategy note

## Day 5 — Authentication and roles
### Goals
- set up login/auth
- seed roles
- define route/page access rules

### Deliverables
- login flow
- seeded users
- role policy skeleton

## Day 6 — Base UI shell
### Goals
- layout
- navigation
- role-aware menu
- dashboard placeholder

### Deliverables
- main layout
- nav structure
- placeholder dashboard page

## Day 7 — README + checkpoint
### Goals
- update README
- write what works / what is missing
- clean up repo after week 1

### Deliverables
- improved README
- week 1 checkpoint notes

---

# WEEK 2 — CORE BUSINESS APP

## Day 8 — Partnership records list page
### Goals
- build listing page
- filter/search basics
- status display

### Deliverables
- partnership index page
- table/list UI

## Day 9 — Partnership detail page
### Goals
- build detail page
- show all key business fields
- show related records section

### Deliverables
- partnership detail view

## Day 10 — Partnership create/edit flow
### Goals
- forms
- validation
- create/update behavior

### Deliverables
- edit page
- validation rules

## Day 11 — Approval workflow states
### Goals
- status transitions
- role restrictions
- action buttons

### Deliverables
- workflow action logic
- approval transition rules

## Day 12 — Audit trail basics
### Goals
- log record changes and status updates
- show activity history

### Deliverables
- activity history model
- activity section on detail page

## Day 13 — Dashboard first real version
### Goals
- counts and summary cards
- pending approvals
- issue totals
- active partnerships

### Deliverables
- useful dashboard widgets

## Day 14 — Week 2 review
### Goals
- clean code
- trim rough edges
- update docs

### Deliverables
- week 2 checkpoint
- screenshots or notes

---

# WEEK 3 — INTEGRATIONS + DELIVERY

## Day 15 — Mock SaaS A
### Goals
- create Creator Profile mock API shape
- define payloads
- decide whether it lives as separate lightweight service or mocked in-app

### Deliverables
- mock API endpoints or stub service

## Day 16 — Mock SaaS B
### Goals
- create Campaign API shape
- define payloads and test data

### Deliverables
- campaign mock endpoints/stubs

## Day 17 — Integration service layer
### Goals
- external client abstraction
- data mapping logic
- sync service skeleton

### Deliverables
- integration clients
- mapping logic

## Day 18 — Sync logging and failures
### Goals
- log sync jobs
- capture failures
- show last success/failure

### Deliverables
- IntegrationJobLog model
- integration status page basics

## Day 19 — Issue resolution queue
### Goals
- generate operational issues from bad data or failed syncs
- build issue list

### Deliverables
- issue queue page
- issue model and status logic

## Day 20 — Dockerization
### Goals
- Dockerfile
- docker-compose if useful
- local consistent startup

### Deliverables
- app container setup

## Day 21 — CI/CD first pass
### Goals
- GitHub Actions workflow
- build and test pipeline
- maybe lint or validation steps

### Deliverables
- pipeline YAML

---

# WEEK 4 — TERRAFORM + ENTERPRISE POLISH

## Day 22 — Terraform structure
### Goals
- define infra folder structure
- variables and environment assumptions
- first main.tf structure

### Deliverables
- terraform scaffold
- provider and module outline

## Day 23 — Deployment design
### Goals
- define app hosting model
- define DB infra assumptions
- define config/secrets approach

### Deliverables
- deployment architecture draft
- infra README update

## Day 24 — Architecture diagrams
### Goals
- system context diagram
- container/component diagram
- integration flow diagram

### Deliverables
- diagrams in docs/architecture

## Day 25 — Technical design doc
### Goals
- write design doc
- explain architecture choices
- explain workflows and integrations

### Deliverables
- technical design document

## Day 26 — Runbooks
### Goals
- local startup
- failed sync troubleshooting
- deployment validation
- common support actions

### Deliverables
- runbook docs

## Day 27 — DR / resiliency notes
### Goals
- identify likely failure modes
- document recovery assumptions
- document critical dependencies

### Deliverables
- resiliency / DR note

## Day 28 — Change management / enterprise polish
### Goals
- change request template
- rollout steps
- rollback steps
- validation checklist

### Deliverables
- change plan template

## Day 29 — Resume + portfolio packaging
### Goals
- write resume bullets
- write project summary
- collect screenshots
- list technologies and outcomes

### Deliverables
- resume-ready project bullets
- short case-study summary

## Day 30 — Final review
### Goals
- review repo structure
- check docs completeness
- identify next-phase improvements
- mark MVP complete

### Deliverables
- final checkpoint
- backlog for v2 improvements

---

# MVP DEFINITION
By day 30, MVP should include:
- running app
- auth and roles
- partnership records
- approval workflow
- dashboard
- at least 2 mock integrations
- issue queue
- basic audit log
- Docker
- CI/CD starter pipeline
- Terraform scaffold
- architecture docs
- runbooks

If all of that is done, this is already a strong portfolio project.

---

# IF YOU FALL BEHIND
If time gets tight, prioritize in this order:
1. running app with auth
2. partnership records
3. approval workflow
4. dashboard
5. at least 1 mock integration
6. issue queue
7. docs
8. CI/CD
9. Terraform polish

The point is to finish something real, not keep perfecting theory.
