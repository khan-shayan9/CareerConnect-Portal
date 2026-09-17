# CareerConnect

A desktop job-application portal built with Python (Tkinter) and SQLite, modeling a real campus placement system: students apply to jobs, recruiters post openings and manage candidates, and admins oversee the platform — all on top of a normalized relational schema.

![ER Diagram](ER%20Diagram.png)

## Overview

CareerConnect was built as a database-design project: the focus is a clean, constraint-enforced relational schema (see `db_structure.sql`, `ER Diagram.png`) driving a working multi-role GUI application, not just a mockup.

## Roles

- **Student** — registers with a university email, builds a profile (program, semester, CGPA, skills, certifications, resume upload), browses/searches jobs, and tracks application status.
- **Recruiter** — registers a company profile, posts job openings, and manages applicants (shortlist / accept / reject).
- **Admin** — signs in with a seeded admin account, reviews hiring activity and portal-wide stats via SQL aggregation.

## Schema

Core tables (see `db_structure.sql` / individual `.sql` files):

| Table | Purpose |
|---|---|
| `users` | Shared credentials + role (Student / Recruiter / Admin) |
| `students` | Student profile, linked 1:1 to `users` |
| `recruiters` | Company profile, linked 1:1 to `users` |
| `jobs` | Job postings, linked to `recruiters` |
| `applications` | Many-to-many junction between `students` and `jobs`, with status tracking |
| `job_fairs` | Standalone event listings |

Foreign keys enforce referential integrity throughout (e.g. an application can't reference a nonexistent job or student).

## Tech stack

- **Language:** Python 3
- **GUI:** Tkinter / ttk
- **Database:** SQLite (`careerconnect.db`), accessed via `sqlite3`
- **Concepts:** relational schema design, 3NF normalization, role-based access, parameterized SQL (no string-built queries)

## Run it

```bash
python code.py
```

No extra dependencies — Tkinter and sqlite3 ship with standard Python. The database file and tables are created automatically on first run, along with a seeded admin login.

> Default admin login is hardcoded in `code.py` (`admin` / `1234`) — change it before using this beyond a local demo.

## Files

- `code.py` — application entry point and full Tkinter UI
- `db_structure.sql`, `applications.sql`, `companies_jobfair.sql`, `interviews.sql`, `jobposting.sql`, `recruiters.sql` — schema and seed data
- `ER Diagram.png` — entity-relationship diagram
