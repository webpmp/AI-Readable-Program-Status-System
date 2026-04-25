# Program-Template

## Overview

This template is designed to be used with an AI assistant as the primary interface for program tracking. It structures all project information so it can be stored in one place and queried directly using natural language.

It consolidates projects, milestones, deliverables, resources, and risks into a single structured view that both humans and AI can interpret consistently.

The goal is operational clarity through a shared system:

* one place to update
* one place to review
* one source of truth for both people and AI

Instead of manually scanning sections, users ask the AI questions like:

* what’s at risk
* what’s due next
* who owns what

The structure is optimized so the AI can reliably interpret relationships across the entire document without additional configuration.


## ID SYSTEM

All entities use short IDs for reference. IDs replace repeated names.

Rules:

* Use `ID` in every table
* One ID = one entity (no reuse)
* IDs are stable (do not rename)

Prefixes:

* P- = Project → `P-A`
* M- = Milestone → `M-A1`
* D- = Deliverable → `D-A1`
* T- = Task → `T-A1`
* R- = Risk → `R-A1`
* DEP- = Dependency → `DEP-A1`
* ACT- = Action → `ACT-01`

Resource IDs are role-based:

* Design Lead → `DL-01`
* UX Designer → `UXD-01`
* Product Designer → `PD-01`

Format:

* `[TYPE]-[PROJECT][#]` for scoped items → `M-A1`, `D-B2`
* Global items use `G` → `R-G1`, `DEP-G1`

Use IDs for all references:

* Milestones → `M-A1`
* Owners → `DL-01`
* Risks → `R-A1`

Names are for readability. IDs are the source of truth.

```
---
## PROGRAM STATUS SUMMARY 
---
PROGRAM STATUS SUMMARY (Exec View)

| Project ID | Project   | Status   | Health | % Complete | Next Milestone | Critical Blocker |
|------------|-----------|----------|--------|------------|----------------|------------------|
| P-A        | Project A | [STATUS] | [🟢🟡🔴] | [X%]       | M-A1           | [Short note]     |
| P-B        | Project B | [STATUS] | [🟢🟡🔴] | [X%]       | M-B1           | [Short note]     |


### GLOBAL RISKS / DEPENDENCIES

| ID    | Type        | Description / Name | Impact | Owner / Action |
|-------|-------------|--------------------|--------|----------------|
| R-G1  | Risk        | [Shared risk]      | [H/M/L]| DL-01          |
| DEP-G1| Dependency  | [External/API]     | [—]    | UXD-01         |

<br>

---
## PROJECT TEMPLATE (COPY PER PROJECT)
---

# PROJECT: [Name]  
### PROJECT ID: [P-A]


| Field            | Value |
|------------------|------|
| Status           | [Not Started | In Progress | Complete | Blocked] |
| Health           | [🟢🟡🔴] |
| Progress         | [X%] |
| Start / End      | [YYYY-MM-DD → YYYY-MM-DD] |
| Next Milestone   | [M-A1] |
| Key Risk         | [R-A1] |


### STATUS NOTES
- Summary: [1–2 lines]
- Changes: [Recent updates]
- Blockers: [R-A1, DL-01]
- Decisions: [DEC-A1, UXD-01, YYYY-MM-DD]


### MILESTONES

| ID   | Name            | Date       | Status |
|------|-----------------|------------|--------|
| M-A1 | Kickoff         | 2026-05-01 | [...]  |
| M-A2 | Design Complete | 2026-06-01 | [...]  |


### DELIVERABLES

| ID   | Name              | Milestone | Owner  | Status | Due       | Type  | Link |
|------|-------------------|-----------|--------|--------|-----------|-------|------|
| D-A1 | Wireframes        | M-A1      | DL-01  | [...]  | 2026-05-05| Figma | ...  |
| D-A2 | Final Designs     | M-A2      | UXD-01 | [...]  | 2026-06-01| Figma | ...  |


### RESOURCES

| ID    | Name        | Role        | Allocation | Status | Notes |
|-------|-------------|-------------|------------|--------|-------|
| DL-01 | Jane Doe    | Design Lead | 50%        | [...]  | [...] |
| UXD-01| John Smith  | UX Designer | 75%        | [...]  | [...] |


### TASKS

| ID   | Task              | Resource | Milestone | Status | Due       | Notes |
|------|-------------------|----------|-----------|--------|-----------|-------|
| T-A1 | Create wireframes | DL-01    | M-A1      | [...]  | 2026-05-03| [...] |
| T-A2 | Review designs    | UXD-01   | M-A2      | [...]  | 2026-05-20| [...] |


### RISKS

| ID   | Description        | Impact | Status |
|------|--------------------|--------|--------|
| R-A1 | Design delay       | High   | Open   |
| R-A2 | Resource bandwidth | Medium | Open   |


### DEPENDENCIES

| ID     | Type      | Name     | Owner  | Notes |
|--------|-----------|----------|--------|-------|
| DEP-A1 | Resource  | UXD-01   | DL-01  | Blocks M-A2 until wireframes approved |
| DEP-A2 | External  | API Team | UXD-01 | Waiting on endpoint spec v2 |


### NEXT ACTIONS (Cross-Project)

| ID     | Priority | Owner  | Action                 | Due       |
|--------|----------|--------|------------------------|-----------|
| ACT-01 | P1       | DL-01  | Resolve R-A1           | 2026-05-02|
| ACT-02 | P2       | UXD-01 | Align on M-A2          | 2026-05-10|

```
## Constraints

* Do not rename headers
* One row = one item
* Do not merge cells
* Use defined status values only


## AI ASSISTANT USAGE

Users interact with this document using natural language. The AI interprets intent, identifies the relevant project context, and maps queries to internal IDs automatically.

---

### How to ask questions (natural language)

- When is the next milestone for Project A due and who is working on it?
- What is blocking Project B’s current milestone?
- Who owns the deliverables in Project A?
- What work is UX Designer John Smith doing in Project B?
- What risks are currently affecting Project A and what is their impact?

---

### Multi-project comparisons

- Which is more at risk: Project A or Project B, and why?
- Which project has more overdue deliverables, Project A or Project B?
- What resources are shared between Project A and Project B, and are there conflicts?
- Which project has the highest workload on DL-01?

---

### What the AI does automatically

When processing a request, the AI will:

- Identify relevant projects from natural language
- Map milestones, tasks, deliverables, risks, and dependencies internally using IDs
- Cross-reference across all sections without requiring user-visible IDs
- Resolve ambiguous terms like “design milestone” or “final deliverable”
- Aggregate information across tables when needed

---

### Example interpretation flow

User:
- What is blocking Project B’s design milestone?

AI internally:
- Locate Project B
- Identify relevant milestone
- Pull linked deliverables
- Check risks and dependencies
- Identify responsible owners
- Return blockers and impact

---

### Validation-level queries

- Are any milestones missing deliverables?
- Are any deliverables missing owners or links?
- Which resources are over-allocated across projects?
- Which dependencies are currently creating downstream risk?

---

### Key principle

- Interaction is fully natural language
- Internal IDs are never exposed or required
- The AI handles all mapping, cross-referencing, and resolution
