---
name: db-migrate
description: Safe database migration — review SQL, apply, verify
allowed-tools: Bash, Read, Write, Edit, Glob, Grep, Agent
---

Run a safe database migration:

1. Launch `prisma-expert` agent to review current schema
2. Generate migration: `npx prisma migrate dev --name $ARGUMENTS --create-only`
3. Show generated SQL for review
4. Ask user to approve before applying
5. Apply migration: `npx prisma migrate dev`
6. Verify: `npx prisma validate` + `npx prisma db pull` to check sync
7. Update seed data if needed

For Supabase projects, use Supabase CLI instead of Prisma.