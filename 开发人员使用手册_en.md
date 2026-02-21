# Developer Manual (packaged `newui.exe` + external `nanobot-main`)

This manual is for **developers / maintainers / power users**. It explains how the packaged `newui.exe` loads a sibling `nanobot-main/` folder, where data is stored, how the packaged dependency installer works, and how to develop & connect Skills and MCP servers in a “no Python required on the target machine” distribution.

---

### 1) Recommended release layout (nanobot-main is replaceable)

The distributed output is the `newui.dist/` folder (standalone build).

Recommended layout:

```
newui.dist/
  newui.exe
  nanobot-main/               # external: put HKUDS/nanobot here
    nanobot/
    pyproject.toml
    requirements.txt
    ...
  (other packaged runtime files)
```

To upgrade nanobot later:

- download a newer [HKUDS/nanobot](https://github.com/HKUDS/nanobot)
- replace the sibling `nanobot-main/` folder next to `newui.exe`

---

### 2) Runtime paths (Windows)

- **nanobot config**: `%USERPROFILE%\.nanobot\config.json`
- **newui state**: `%USERPROFILE%\.nanobot\newui\`
  - log: `%USERPROFILE%\.nanobot\newui\newui.log`
  - sessions: `%USERPROFILE%\.nanobot\newui\sessions.json`
  - **vendor site-packages (writable)**:
    - `%USERPROFILE%\.nanobot\newui\vendor\site-packages\`
- **workspace**: `%USERPROFILE%\.nanobot\workspace\`
  - skills: `%USERPROFILE%\.nanobot\workspace\skills\`

---

### 3) How `newui.exe` loads external `nanobot-main`

At startup, `newui.exe`:

- checks whether `nanobot-main\nanobot\cli\commands.py` exists next to the executable
- if present, inserts `nanobot-main/` to the front of `sys.path` (prefer external source)
- if missing, the UI can still start, but embedded agent/gateway features will fail (errors shown in logs)

Outcome:

- keep `nanobot-main/` as a sibling folder to make upgrades possible without rebuilding the UI.

---

### 4) Packaged dependency installer (no system Python)

The distribution goal is: **target machines do not need Python**.

Therefore, dependency installation in the UI works like this:

- uses packaged pip internals (`pip._internal`)
- installs packages into:

`%USERPROFILE%\.nanobot\newui\vendor\site-packages\`

Then `newui.exe` prepends this folder to `sys.path`, so:

- newly installed deps can override bundled deps
- when `nanobot-main` upgrades introduce new dependencies, users can install missing modules via UI and restart

---

### 5) Troubleshooting patterns

1) `ModuleNotFoundError: No module named 'xxx'`
   - instruct users to install `xxx` in **Settings → Install dependencies**
   - restart `newui.exe`

2) Package data files missing (e.g. JSON assets)
   - fix packaging by adding `--include-package-data=<package>`
   - or install/upgrade the package via UI to vendor site-packages (override)

---

### 6) Skills development (SKILL.md)

#### 6.1 Where skills live

Skills are loaded from:

- `%USERPROFILE%\.nanobot\workspace\skills\<skill-name>\SKILL.md`

Workspace skills override built-in skills.

#### 6.2 Recommended SKILL.md frontmatter format

SkillsLoader does a minimal `key: value` frontmatter parse, so keep it simple and keep `metadata` as single-line JSON:

```markdown
---
name: my-skill
description: Example skill for Windows automation
metadata: '{"nanobot": {"requires": {"bins": [], "env": []}, "always": false}}'
---
```

`metadata.nanobot.requires` is used by the UI to show availability:

- `bins`: checked with `shutil.which()` (e.g. `git`, `node`)
- `env`: checked via environment variables

#### 6.3 Creating a skill on a target machine (no Python required)

1) In newui: **Skills Manager → Open skills folder**
2) Create: `%USERPROFILE%\.nanobot\workspace\skills\<skill-name>\`
3) Create `SKILL.md` (Notepad is enough)
4) Back to Skills Manager, refresh and preview
5) In chat: “Use skill <skill-name> to …”

#### 6.4 Example: “run a local exe” skill template

```markdown
---
name: run-local-exe
description: Run a local exe/bat and report output.
metadata: '{"nanobot": {"requires": {"bins": [], "env": []}, "always": false}}'
---

## Workflow (Windows)
1) Confirm the full path and arguments if unclear.
2) Use exec tool to run the program.
3) Report exit code and key output.

## exec examples
- `cmd /c \"C:\\\\Tools\\\\MyApp\\\\myapp.exe\" --help`
- `cmd /c \"C:\\\\Tools\\\\do_something.bat\"`
```

---

### 7) MCP servers (tool servers) in a “no Python on target” distribution

MCP config is stored in `config.json` under:

- `tools.mcpServers` (also compatible with `tools.mcp_servers`)

Tools are registered as:

- `mcp_<serverName>_<toolName>`

#### 7.1 UI fields

- stdio:
  - `command`: runnable command (ideally `xxx.exe`, or `npx`/`node`)
  - `args`: args list
  - `env`: JSON env injection
- HTTP:
  - `url`: MCP HTTP endpoint

#### 7.2 Key constraint

If target machines must not install Python:

- do **not** rely on `python -m your_mcp_server` for stdio MCP
- either:
  - ship an **MCP server as a standalone exe** and point `command` to it
  - or deploy an **HTTP MCP** server remotely and only configure `url`

#### 7.3 Recommended routes (most portable first)

1) **HTTP MCP** (best portability)
2) **stdio MCP with a standalone exe**
3) **stdio MCP via Node/npx** (requires Node installed)

#### 7.4 Calling MCP tools (stable test phrases)

- Natural language: “Use <serverName>'s <toolName> to …”
- Explicit tool call: “Use tool `mcp_<serverName>_<toolName>` with params `{...}`”

#### 7.5 Validate in newui

In **MCP Servers Manager**:

- click **Test connection / list tools**
- verify `mcp_*` tools show up

