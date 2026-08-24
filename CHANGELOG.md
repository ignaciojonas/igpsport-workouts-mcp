# Changelog

All notable changes to this project are documented here. The format is based on
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project
adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.2.0] - 2026-08-24

### Fixed
- **Login migrated to OAuth2.** iGPSPORT retired the old
  `i.igpsport.com/Auth/Login` cookie flow (that host is now a static bucket; the
  web app moved to `app.igpsport.com` with an SSO). `login()` now uses the
  OAuth2 password grant against `POST /service/auth/connect/token` and returns
  the `access_token` as a Bearer header. The REST API is unchanged, so only
  authentication was affected. Endpoint captured from the iPhone app via
  mitmproxy and verified live.

### Changed
- Removed all references to intervals.icu across README, package description,
  docstrings, and the GitHub repository metadata.
- README now leads with the "let any LLM create workouts on iGPSPORT via MCP"
  positioning.

## [0.1.0] - 2026-06-30

### Added
- **MCP server** (`igpsport_mcp.py`, FastMCP) exposing three tools:
  - `igpsport_list_workouts` — list existing custom workouts.
  - `igpsport_create_workout` — create (or edit, via `edit_workout_id`) a
    structured workout from a strict Pydantic block schema.
  - `igpsport_delete_workout` — delete a workout by id. Endpoint
    (`WorkOut/CustomWorkOutDel?id=`) reverse-engineered from the iPhone app.
- **Heart-rate targets**: steps can target a BPM range (`{"bpm": [min, max]}`)
  or an HR zone (`{"hr_zone": 1-5}`), in addition to power (watts or %FTP). A
  step targets power XOR heart rate.
- **Keychain-backed credentials** (`igpsport_credentials.py`) via `keyring`, so
  no secrets live in the MCP client config. Env-var fallback for local dev.
- **CLI** (`igpsport_cli.py`) with `list`, `upload-example`, and `delete`.
- Offline test suite for the workout mapping and request shapes.
- `uv` project (`pyproject.toml`), README, and example Claude Desktop config.

### Changed
- Project renamed to **igpsport-workouts-mcp** (package, GitHub repo, and MCP
  server id `igpsport-workouts`).
- Client and CLI translated to English.

[0.2.0]: https://github.com/ignaciojonas/igpsport-workouts-mcp/releases/tag/v0.2.0
[0.1.0]: https://github.com/ignaciojonas/igpsport-workouts-mcp/releases/tag/v0.1.0
