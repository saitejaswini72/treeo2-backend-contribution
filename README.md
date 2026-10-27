# TreeO2: Backend API and Database Contribution

**Role:** Database Co-Lead and Backend Developer
**Client:** xpand Foundation (NGO)
**Project type:** Real-world client project, delivered in a multidisciplinary team
**Duration:** March 2026 to June 2026

> This repository summarises my contribution to the TreeO2 backend. The source code belongs to the project and is held in a private repository, so no project code or data is included here.

## About the project

TreeO2 is a platform used by xpand Foundation to track trees planted by smallholder farmers in Timor-Leste, supporting reforestation and carbon accounting. The backend manages users, roles, projects, partners, tree scans, scan audits, and reports.

**Tech stack:** Node.js, TypeScript, Express.js, Prisma ORM, PostgreSQL, Docker, JWT authentication, Swagger / OpenAPI, Jest, GitHub

The backend follows a modular, layered architecture:

```
Routes  ->  Controllers  ->  Services  ->  Prisma (PostgreSQL)
```

## My contribution

### 1. Database design with Prisma and PostgreSQL

- Translated the project ER diagram into Prisma models, implementing core models including User, Role, Project, UserRoleAssignment, and UserProject.
- Defined one-to-many and many-to-many relationships between users, roles, and projects using `@relation`, composite keys, and field mappings (`@map`, `@@map`).
- Identified and added missing foreign key relations, applied appropriate delete strategies, and configured cascade delete behaviour on junction tables.
- Added indexes to improve schema consistency and query performance.
- Validated every schema change locally with `prisma validate`, `prisma generate`, and `prisma db push` before raising a pull request.

### 2. Partners API module

Built the complete Partners API module, used to manage partner organisations, following the project's modular structure.

- Implemented all five CRUD endpoints, with routes, controllers, and a service layer.
- Secured endpoints with JWT authentication and role-based authorisation, so only authorised roles (such as Admin and Manager) can create, update, or delete partners.
- Added validation and structured error handling for edge cases such as invalid IDs, empty payloads, duplicate entries, and missing resources.
- Wrote **unit and integration tests** covering CRUD behaviour, authentication, authorisation, validation, and error conditions.
- Documented every endpoint in Swagger / OpenAPI and in the project's API.md, including request and response examples, validation rules, access control, and testing steps.

### 3. Code reviews and quality checks

As Database Co-Lead, I reviewed pull requests covering Prisma schema updates, relationships, seed scripts, and backend changes.

- Tested pull requests locally rather than reviewing code visually only. While reviewing a seed data update, I found that the seed command failed when run more than once because of a transaction timeout. I requested changes, re-tested the fix, and approved the pull request once it was resolved.
- Identified issues such as missing relationships, incorrect mappings, and schema inconsistencies, and followed up with authors until fixes were complete.
- Resolved merge conflicts in shared documentation when several contributors updated the same file.

### 4. Documentation and team support

- Wrote backend documentation covering project setup, the Prisma workflow, relationship implementation, debugging steps, and the API architecture, written so future students could onboard quickly.
- Supported team members with Prisma concepts and relationship implementation, and worked with other team leads to apply new database requirements consistently across modules.
- Tracked tasks in Microsoft Planner and took part in weekly team and mentor meetings.

## Challenges I solved

- **Local environment setup:** fixed database authentication failures, Docker configuration problems, occupied ports, and Prisma validation errors by checking environment variables, container status, and schema files.
- **Relationship validation errors:** worked through foreign key and relationship errors in Prisma by breaking the problem down, testing different approaches, and validating locally before integration.

## What I learned

- How database design decisions, such as relationships and delete behaviour, affect the rest of a backend system.
- How to structure a backend module so it is easy to test, review, and maintain.
- Why testing both normal and failure scenarios matters before code reaches the main branch.
- How to give and act on code review feedback within a shared Git workflow.
