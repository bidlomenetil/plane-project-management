# Plane project management

A workspace-based project management product for issues, project cycles and collaborative planning.

## Architecture and stack

`apps/web` and related frontend apps provide the user interface; `apps/api` is Django/DRF; shared TypeScript packages contain components and state; Celery workers, PostgreSQL, Redis/Valkey, RabbitMQ and object storage support background processing and persistence.

## Requirements

Node >=22.22.0, pnpm 11.10.0 (see `packageManager`), Python 3.12 and the exact uv version in `apps/api/pyproject.toml`; Docker Compose for backend services.

## Installation and local development

```sh
./setup.sh
pnpm install --frozen-lockfile
pnpm dev
```

Review generated environment files before starting. The frontend task runner is Turbo. `docker-compose-local.yml` defines backend dependencies; its services need the root and API environment files created by setup.

## Configuration

Use the checked-in app environment examples through `setup.sh`. Configure database, queue, object storage and public application URLs consistently. Keep generated `.env` files out of commits.

## Testing

`pnpm check` runs workspace checks. The backend isolated test stack is `docker compose -f docker-compose-test.yml up --build --abort-on-container-exit --exit-code-from api-tests`; `AGENTS.md` documents focused pytest runs.

## Deployment and integrations

Review `docker-compose.yml` and `deployments/` for the source-aligned service topology. Production needs TLS, persistent databases/object storage and tested backups. API implementation and schema configuration live in `apps/api`.

## Source provenance and license

This repository imports source from [makeplane/plane](https://github.com/makeplane/plane). Original product functionality belongs to its upstream contributors. The local history begins with a November 2026 source snapshot; it does not retain upstream development history or prove the exact upstream revision. GitHub reports the upstream repository was created on 2022-11-19; that is repository-origin evidence, not the date of this contribution. Existing year folders are retained as local organization.

Preserve `LICENSE.txt` and existing third-party notices when redistributing. Missing root license text was recovered from the upstream repository during this maintenance pass; existing license files were preserved.

## Validation status

Setup and test commands above were checked against this checkout’s manifests, scripts and entry points. Full dependency installation, application builds and integration tests were not performed in this maintenance pass. The Node/pnpm workspace dependencies, Python 3.12 backend and database/queue test stack were not provisioned. These instructions identify the supported workflow without claiming a successful product build.

See [source provenance](SOURCE_PROVENANCE.md) for pinned upstream license retrieval evidence and redistribution limitations.
