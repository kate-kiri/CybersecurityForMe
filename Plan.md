# Cybersecurity Checklist API — Project Plan

## Goal
Build a beginner-friendly Python API for tracking devices you own or are authorized to manage, recording security checks, and following up on findings. This is a defensive learning project; it will not scan third-party systems or exploit vulnerabilities.

## Technology
- **Python** — application language
- **FastAPI** — HTTP API and interactive OpenAPI docs
- **Pydantic** — request validation
- **SQLite** — local development database
- **pytest** and FastAPI's test client — automated tests
- **Uvicorn** — local development server

## MVP features
1. Create, list, view, update, and delete an asset (for example, a lab computer or home router).
2. Record a checklist item for an asset (for example, updates enabled, MFA enabled, or backups verified).
3. Mark checklist items as open or resolved, with a short remediation note.
4. Filter assets and checklist items by status.
5. Validate all input and return consistent HTTP errors.

## Initial API sketch
- `GET /health` — confirm the service is running.
- `GET /assets` and `POST /assets` — list and register assets.
- `GET /assets/{asset_id}`, `PATCH /assets/{asset_id}`, and `DELETE /assets/{asset_id}` — manage an asset.
- `GET /assets/{asset_id}/checks` and `POST /assets/{asset_id}/checks` — list and add checks.
- `PATCH /checks/{check_id}` — update a check or mark it resolved.

The exact request and response models will be defined during implementation. The API should not accept passwords, private keys, or other secrets as asset metadata or remediation notes.

## Security requirements
- Bind the development server to `127.0.0.1`; do not expose it to the public internet.
- Keep the database local and exclude database files, virtual environments, and secrets from version control.
- Validate and constrain user-supplied strings and identifiers; use parameterized database operations.
- Do not store credentials or sensitive host data. Use fictional/sample asset names in demos.
- Add authentication and authorization before any multi-user or remotely accessible deployment.
- Use HTTPS, secure secret configuration, dependency updates, logging hygiene, and backups before deployment.
- Test that invalid inputs and unknown IDs fail safely without leaking internal errors.

## Build steps
1. Create a Python virtual environment and install FastAPI, Uvicorn, and pytest.
2. Implement the app and `/health`; run it locally and inspect the generated API docs.
3. Define asset and check schemas, validation rules, and tests.
4. Add persistence with SQLite and implement the asset endpoints.
5. Add checklist endpoints and status filtering.
6. Run the test suite; review validation, error handling, and accidental data exposure.
7. Add authentication only if the API needs access beyond a single local user; do not deploy publicly until the security requirements are met.

## Definition of done
- The API starts locally using the documented command.
- The core endpoints work through the interactive docs and automated tests.
- Data survives an application restart in local SQLite.
- Tests cover successful requests, invalid data, missing resources, and database behavior.
- The README documents setup, usage, limitations, and safe local-only operation.
