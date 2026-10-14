# Contributing to Topview 3D Builder

This page is for people changing the code or cutting releases. If you just want
to use the plugin, the [README](README.md) is all you need.

Read [docs/topview-3d-cli.md](docs/topview-3d-cli.md) before changing the CLI
contract or the `.topview-3d/` project format.

## Repository layout

| Path | What's in it |
| --- | --- |
| `editor/` | The 3D Builder editor workspace, including Studio (Next.js) and the renderer |
| `agent/` | The `topview_3d_cli` Python package; the director document contract is in `topview_3d_cli/contracts`. `agent/pyproject.toml` defines the `topview-3d-cli` distribution and command |
| `skills/topview-3d-cli/` | The agent skill: `SKILL.md` plus one `references/*.md` per workflow stage. Every command it quotes runs against the CLI |
| `builtin-assets/` | Built-in characters, poses and primitives (CC BY 4.0) |
| `scripts/` | `build_dist.py`, `install.sh`, `install.ps1`, `lint_skills.py`, `set_version.py`, `package-codex-plugin.mjs`, `wheel_smoke.py` |
| `.codex-plugin/`, `.claude-plugin/`, `.cursor-plugin/`, `.agents/plugins/` | Plugin manifests |
| `assets/` | Plugin logo and icon (see [assets/README.md](assets/README.md)) |
| `.github/workflows/` | `ci.yml` and `release.yml` (PyPI / TestPyPI) |
| `docs/` | CLI contract and the migration plan |

Python 3.11+ handles document and operation logic. Node and Playwright are the
rendering runtime. Docker isn't used locally.

### Which manifest each agent reads

| Agent | Manifest |
| --- | --- |
| ChatGPT (Codex app) and Codex CLI | `.codex-plugin/plugin.json`, `.agents/plugins/marketplace.json`, `.mcp.json` |
| Cursor | `.cursor-plugin/plugin.json` |
| Claude Code | `.claude-plugin/plugin.json`, `.claude-plugin/marketplace.json` |

Only the Codex manifest declares an MCP server (`topview-3d`, in `.mcp.json`);
Codex asks you to sign in to Topview the first time the plugin uses it. Cursor
and Claude Code load the skill only.

## Development setup

You'll also need pnpm 8+ (`corepack enable pnpm` is enough).

```bash
# macOS / Linux
scripts/install.sh
```

```powershell
# Windows (PowerShell 5.1 or 7)
powershell -ExecutionPolicy Bypass -File scripts\install.ps1
```

The script:

1. Installs the CLI in editable mode into one shared environment:
   `~/.local/share/topview-3d-cli/venv` (`$XDG_DATA_HOME/topview-3d-cli/venv` when set), or
   `%LOCALAPPDATA%\topview-3d-cli\venv` on Windows. With `--dev` it uses `agent/.venv`.
   It uses `uv` when present, otherwise `python -m venv` plus pip.
2. Installs the renderer and Studio with `pnpm install --frozen-lockfile` (`--dev` installs the whole editor workspace).
3. Builds `@topview/3d-builder`.
4. Runs `topview-3d-cli browser ensure` to download Playwright Chromium.
5. Runs `topview-3d-cli doctor`.

It's safe to re-run. Options: `--dev` / `-Dev`, `--install-uv` / `-InstallUv`,
`--skip-node` / `-SkipNode`, `--skip-browser` / `-SkipBrowser`.

### Installing the CLI without a checkout

```bash
pipx install topview-3d-cli
# or, without a permanent install:
uvx --python 3.12 topview-3d-cli doctor
# or, with neither: one environment shared by every project
python3 -m venv ~/.local/share/topview-3d-cli/venv
~/.local/share/topview-3d-cli/venv/bin/python -m pip install topview-3d-cli
topview-3d-cli browser ensure
topview-3d-cli doctor
```

Pass `--python 3.12` to `uvx`; a plain `uvx topview-3d-cli` fails when the default
Python is older than 3.11. `pip install --user` isn't used because many Python
installs refuse it (PEP 668). If your pip mirror lags behind, add
`--index-url https://pypi.org/simple/`.

### A first scene from the command line

```bash
topview-3d-cli project init my-scene
topview-3d-cli asset search sit --kind pose
topview-3d-cli node batch my-scene changes.json   # add / update / delete nodes atomically
topview-3d-cli evaluate my-scene                  # numerical checks, no browser
topview-3d-cli inspect views my-scene             # numbers and renders for every camera
topview-3d-cli renders show my-scene              # path of the latest contact sheet
```

A sample batch lives at `agent/topview_3d_cli/tests/fixtures/local-project/operations.json`
(`topview-3d-cli document apply my-scene <file>`). Every command prints one JSON
object; exit code 0 is success, 2 invalid input, 1 execution failure.

## Tests

```bash
agent/.venv/bin/python -m pytest agent              # needs install.sh --dev
agent/.venv/bin/python scripts/lint_skills.py       # skill frontmatter, wording, links, commands
pnpm -C editor --filter @topview/3d-builder typecheck
pnpm -C editor --filter @topview/3d-builder test:evaluate
pnpm -C editor --filter @topview/3d-director-cli test
```

## Versions

One version is shared by the CLI (`agent/topview_3d_cli/__init__.py`), the three
plugin manifests and every `topview-3d-cli==` pin in the skill:

```bash
python3 scripts/set_version.py 0.2.0     # rewrite all of them
python3 scripts/set_version.py --check   # CI: exit 1 when any disagree
```

Packages under `editor/` are versioned separately.

## Building the distribution

```bash
agent/.venv/bin/python scripts/build_dist.py   # after install.sh --dev; needs `pip install build`
```

Writes the wheel and sdist to `dist/`. The wheel includes a standalone Studio
build, so this builds Studio too. Nothing is published.

## Publishing to PyPI

`.github/workflows/release.yml` builds with `scripts/build_dist.py` and publishes
with PyPI Trusted Publishing (OIDC, no stored credentials).

- **TestPyPI:** run the workflow by hand (Actions → Release to PyPI → Run workflow). TestPyPI refuses a version it already has, so bump with `set_version.py` between uploads.
- **PyPI:** push a `v<version>` tag matching `agent/topview_3d_cli/__init__.py`. Runs only when the repository variable `PYPI_PUBLISH_ENABLED` is `true`.

Both need a Trusted Publisher for `topview-3d-cli` (owner `topviewai`, repository
`topview-3d-builder`, workflow `release.yml`).

## Building the Codex upload archive

```bash
node scripts/package-codex-plugin.mjs            # warns about TODO fields in the manifest
node scripts/package-codex-plugin.mjs --release  # fails on them
```

Packs the committed `HEAD` into `dist/topview-3d-builder-plugin.zip` under one
`topview-3d-builder/` folder. It stops with a named reason if the manifest
version isn't semver, `mcpServers` doesn't point at `./.mcp.json`, an image isn't
a square 48–4096 px PNG of at most 5 MiB, a skill directory is nested or hidden,
a file is a symlink or over 100 MiB, or the archive exceeds 100 MB. Workspace
admins upload this zip through the plugin submission flow.

## Updating and uninstalling

**Codex** caches plugins by version, and `main` can ship under the same number,
so remove before re-adding:

```bash
codex plugin remove topview-3d-builder@topview-3d-builder
codex plugin marketplace remove topview-3d-builder
codex plugin marketplace add https://github.com/topviewai/topview-3d-builder.git --ref main
codex plugin add topview-3d-builder@topview-3d-builder
```

Use `--ref v<version>` to pin a release. If `codex plugin list` still shows an
old version, delete `~/.codex/plugins/cache/topview-3d-builder`.

**Cursor**

```bash
git -C ~/.cursor/plugins/local/topview-3d-builder fetch origin main
git -C ~/.cursor/plugins/local/topview-3d-builder checkout -B main origin/main
# or remove it
rm -rf ~/.cursor/plugins/local/topview-3d-builder
```

**Claude Code**

```bash
claude plugin marketplace update topview-3d-builder
claude plugin update topview-3d-builder@topview-3d-builder
# or remove it
claude plugin uninstall topview-3d-builder@topview-3d-builder
claude plugin marketplace remove topview-3d-builder
```

**The CLI**

```bash
rm -rf ~/.local/share/topview-3d-cli/venv   # Windows: %LOCALAPPDATA%\topview-3d-cli\venv
pipx uninstall topview-3d-cli
uv cache clean topview-3d-cli
```

The user cache (`~/Library/Caches/topview-3d-cli`, `%LOCALAPPDATA%\topview-3d-cli\Cache`
or `~/.cache/topview-3d-cli`) holds Playwright and Chromium, Studio's list of
project folders and the Topview sign-in. Delete it only if you want all of that
gone. Project folders are never touched.
