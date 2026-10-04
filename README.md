# Backend API add-in (`rulebook-backend`)

An Effortless **add-in seed** (kind `child`), mounted at `backend/`. It has no
rulebook of its own: every step reads the project's
`../../effortless-rulebook/effortless-rulebook.json`.

## What the build produces

| Folder | From | What it is |
|---|---|---|
| `postgres/` | rulebook-to-postgres | Schema, `vw_*` views, calc functions, seed data, `init-db.sh` |
| `api/` | rulebook-to-node-postgres-api | Node + Express API over the views (`npm install && npm start`, port 42441, `PG*` env for the database) |
| `typescript/` | rulebook-to-typescript | TypeScript types and SDK for every table and derived field |
| `gold-answer-key/` | rulebook-to-gold-answer-key | Optional, **disabled by default**: every derived value computed by Postgres. Run it with `effortless build -id rulebook-to-gold-answer-key` once the published tool can reach rulebook-to-postgres. |

## Questions

| Key | Default | Used for |
|---|---|---|
| `postgresSchema` | `public` | `rulebook-to-postgres -p schema=...` |

## How it is used

```bash
effortless cloneSeed effortlessapi/erb-seed-rulebook-backend backend
rm -rf backend/.git
cd backend && effortless build
cd postgres && ./init-db.sh            # create the database
cd ../api && npm install && npm start  # the API on http://localhost:42441
```

The AuthN/AuthZ, Deploy and Native mobile add-ins require this one.
