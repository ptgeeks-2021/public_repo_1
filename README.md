# public_repo_1

Fixture repository for an external, private test suite. Content under
`cases/` is small synthetic scaffolding; content under `web/`, `app/`,
and `vendor/big/` is vendored, unmodified except for version bumps and
slicing, from the upstream open-source projects listed in the
provenance table below.

## Frozen-fixture policy

- `main` received its complete base tree (cases scenario files plus
  vendored scale content) in a single setup pass, then froze. No further
  commits land on `main`.
- `main` and every fixture branch below are protected: no force push, no
  branch deletion.
- Any test failure against these fixtures is a fixture fidelity gap to
  fix here, not a reason to edit `main` or patch the consuming test.

## PR map

| Branch | Diff shape |
|---|---|
| `scale-monster` | `web/package-lock.json` version bump (~18k full-context rows) plus two small `app/` edits |
| `scale-sprawl` | 90 real files changed under `app/` (mixed tiny/small/medium) |
| `scale-mixed` | `vendor/big/sqlite3.c` + `vendor/big/duckdb.cpp` version bumps plus tiny/medium sibling edits |

Cases scenario branches (`case-<group>-left`/`case-<group>-right`) are cut
from this frozen `main` head in a later change; only the scenario base
files under `cases/` exist on `main` today.

## Provenance

| Project | License | Version pair | Files | Copied |
|---|---|---|---|---|
| microsoft/vscode | MIT | 1.95.0 -> 1.101.0 | `web/package-lock.json`, `app/**` | 2026-07-10 |
| SQLite amalgamation | Public domain | 3.45.1 -> 3.53.3 | `vendor/big/sqlite3.c` (sliced to 220,000 lines) | 2026-07-10 |
| DuckDB amalgamation | MIT | v1.1.0 -> v1.5.4 | `vendor/big/duckdb.cpp` (sliced to 200,000 lines) | 2026-07-10 |

Upstream LICENSE files sit beside each vendored directory (`web/LICENSE`,
`app/LICENSE`, `vendor/big/SQLITE-LICENSE.txt`,
`vendor/big/DUCKDB-LICENSE.txt`).

## Layout

```
cases/            small synthetic scenario files (diff/merge edge cases)
web/              vendored VS Code package-lock.json (large single-file diff)
app/              vendored VS Code src/vs/base/common/ slice (many-file diff)
vendor/big/       vendored SQLite + DuckDB amalgamations (very large single files)
```
