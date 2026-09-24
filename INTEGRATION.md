# Supabase Toolkit for JetBrains IDEs

Supabase Toolkit is a plugin for IntelliJ IDEA, WebStorm, PyCharm, PhpStorm, GoLand, Rider, RustRover, CLion, DataGrip, Android Studio and the other JetBrains IDEs. It brings your Supabase project into the IDE: schemas, Row Level Security policies, migrations, edge functions, the local stack, table data, SQL and Supabase Cloud projects.

- Marketplace page: https://plugins.jetbrains.com/plugin/34135-supabase-toolkit
- Demo video: https://www.youtube.com/watch?v=hcryc4eb47Y
- Issues and feature requests: this repository's Issues tab

Supabase Toolkit is an independent product and is not affiliated with or endorsed by Supabase Inc.

## Install

1. In your IDE open **Settings | Plugins | Marketplace**, search for **Supabase Toolkit** and click **Install**.
2. Restart the IDE if asked. A **Supabase** tool window appears in the right-hand sidebar.

Requirements: a JetBrains IDE 2024.3 or newer. For local development, the [Supabase CLI](https://supabase.com/docs/guides/local-development/cli/getting-started) and Docker, as usual for `supabase start`.

## How it integrates with Supabase

### Local projects
- **Project detection.** The plugin looks for `supabase/config.toml` in the project root (or one folder below, for monorepos). The path can also be set in **Settings | Tools | Supabase Toolkit**. It reads `project_id`, the API, database and Studio ports, the exposed API schemas, and edge function settings such as `verify_jwt`.
- **Supabase CLI.** Buttons in the tool window run the CLI in the project folder and stream its output to a console tab: `supabase init`, `start`, `stop`, `status`, `db reset`, `db push`, `migration new`, `functions new`, `functions serve`, `functions deploy`, `link --project-ref` and `gen types typescript --local`. The CLI is found on `PATH` or at a path set in the settings.
- **Local database.** The explorer connects to the local stack's Postgres on the port from `config.toml` (default `postgresql://postgres:postgres@127.0.0.1:54322/postgres`) and reads the Postgres catalog: schemas, tables and views, columns, keys, indexes, triggers, functions, enums, extensions, RLS status and `pg_policy` policies, `storage.buckets`, the `auth.users` count and `supabase_migrations.schema_migrations` to mark each migration file as applied or pending.

### Supabase Cloud
- Paste a **personal access token** (https://supabase.com/dashboard/account/tokens) into **Settings | Tools | Supabase Toolkit**. It is stored in the IDE's password safe.
- The plugin calls the **Supabase Management API** (`https://api.supabase.com/v1`): organizations, projects, `database/query` for SQL and schema browsing, `types/typescript`, `functions`, `secrets` (names only), `database/migrations` and `health`.
- **Link local project to this cloud project** runs `supabase link --project-ref <ref>`.

## Features

**Free**
- Explorer: schemas, tables, views, columns (types, keys, defaults), indexes, triggers, enums, extensions
- Row Level Security at a glance: RLS on or off per table, every policy with its command, roles, USING and WITH CHECK expressions; open a policy or function as SQL
- Storage buckets and object counts, auth user count
- Migrations with applied or pending status; create a migration
- Edge functions: create, serve, deploy
- Local stack: start, stop, status, database reset and push

**Pro** (7-day free trial, sold through the JetBrains Marketplace)
- Table data browser with paging, WHERE filters, inline editing, row deletion and copy as INSERT
- SQL console with Ctrl+Enter, EXPLAIN and multi-statement results
- Supabase Cloud projects through the Management API
- TypeScript type generation from the local stack or a cloud project, optionally after every push or reset

## Quick start

1. Open a project that contains `supabase/config.toml`, or click **Initialize project** in the Supabase tool window.
2. Start the local stack with the play button, or run `supabase start` yourself.
3. Expand **Database** to browse schemas, tables and policies; double-click a table to open its data (Pro).
4. Use the **SQL** tab to run queries against the local stack or a cloud project (Pro).
5. For cloud projects, add a personal access token in the settings and expand **Supabase Cloud**.

## Privacy

Everything runs inside your IDE. Credentials stay on your machine. The plugin connects only to the databases, the Supabase CLI and the Supabase Management API that you configure. It has no analytics or telemetry. Full policy: https://raw.githubusercontent.com/renhyl/supabase-toolkit-legal/refs/heads/main/PRIVACY.md
