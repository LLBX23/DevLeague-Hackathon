# OrgTimeline — People-Centric Tech & Collaboration

## Mapping How Roles and People Evolve Over Time

A solution for the **Setel Lab 2 Challenge**: reconstructing and visualising organisational change over time, letting someone trace both how a role has evolved and how a person has moved through the organisation — and how those two journeys connect.

---

## Quick Start

1. Open `OrgTimeline_fixed.html` in a browser (or visit the deployed URL)
2. Click **"Load Sample Data"** to load the pre-built Engineering department dataset
3. Explore the five tabs: Overview, Role History, People Journey, Connected View, Data Quality

## Uploading Your Own Data

Click **"Upload CSV"** and provide a file with these columns:

| Column | Description |
|--------|-------------|
| `record_type` | `ROLE` or `MOVE` |
| `record_id` | Unique ID for this record |
| `date` | ISO date (YYYY-MM-DD) |
| `role_id` | Role identifier (e.g. ENG-001) |
| `role_title` | Job title at this point in time |
| `department` | Department name |
| `reports_to_role_id` | ID of the parent role |
| `reports_to_name` | Name/title of the person/role they report to |
| `grade` | Salary band or grade level |
| `headcount` | Number of people in this role (for ROLE records) |
| `person_id` | Person identifier (for MOVE records) |
| `person_name` | Person's name |
| `action` | `JOIN`, `PROMOTION`, `TRANSFER`, `LEAVE` |
| `notes` | Free-text notes |

See `sample-data.csv` for a working example.

## Five Views

### 1. Overview
- High-level insights: total roles, people, promotions, transfers, hires, departures
- **Org Snapshot**: a live org chart at the date selected by the timeline scrubber — drag the scrubber to watch the organisation morph in real time

### 2. Role History
- Select any role and see its full evolution: title changes, redesignations, reporting-line shifts, headcount changes
- Each event shows who occupied the role at that time (clickable to jump to that person)
- Ordered timeline with colour-coded markers by change type

### 3. People Journey
- Select any person and see their complete trajectory: joins, promotions, transfers, departures
- Each event links back to the role it relates to (clickable to jump to role history)
- Shows when a person's move coincides with a structural change in their role

### 4. Connected View
- Side-by-side role timeline and person journey
- **Intersection panel**: shows exactly where and when the selected person was in the selected role
- Flags role changes that happened while a specific person occupied the role
- The heart of the solution — not two separate trackers, but one view of a shared history

### 5. Data Quality
- Automatically detects and flags:
  - Roles with no person ever assigned
  - People with no departure record (especially when their role was made redundant)
  - Roles with missing reporting lines
  - Person moves referencing unknown roles
- Issues are flagged, not hidden — the system handles messy data gracefully

## Sample Data Story

The dataset covers the **Engineering department** from January 2023 to July 2025:

- **9 people** tracked across **7 distinct roles**
- Roles include: Junior/Software Engineer (I, II, III), Senior SE → Staff Engineer, Engineering Manager, Engineering Manager II, Engineering Director, VP of Engineering
- Key events: role redesignations, department reorganization (new VP role), reporting line shifts, promotions, transfers, departures, and a role made redundant
- **Intentionally messy data**: missing reporting lines, a person departure not recorded for a redundant role — these are flagged in the Data Quality tab

## Architecture

- Single-page application, pure HTML/CSS/JavaScript (no dependencies)
- CSV parsing with proper quote handling
- Client-side data processing — no server required
- Responsive design with light theme

## CSV Format

The application accepts a single CSV file containing both `ROLE` and `MOVE` records. Two record types:

- **ROLE**: snapshots of a role's state at a point in time (title, reporting line, headcount)
- **MOVE**: records of a person joining, being promoted, transferring, or leaving

This mirrors how real HR data is scattered: some records come from position management systems, others from employee movement logs.
