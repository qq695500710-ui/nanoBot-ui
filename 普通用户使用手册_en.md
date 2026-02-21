# User Manual (newui.exe)

This manual is for **non-programmers / beginners**. It explains how to use the packaged `newui.exe` on Windows to configure and run nanobot (the official open-source project lives in a sibling `nanobot-main/` folder and can be replaced to upgrade).

---

### 1) What you will have

Your packaged folder (e.g. `newui.dist/`) should contain:

- **`newui.exe`**: the Windows GUI app
- **runtime dependencies** next to `newui.exe` (bundled by packaging)
- **`nanobot-main/` (important)**: the official nanobot project folder placed next to `newui.exe`

Recommended layout:

```
newui.dist/
  newui.exe
  nanobot-main/
    nanobot/
    pyproject.toml
    requirements.txt
    ...
  (other packaged runtime files/folders)
```

When nanobot updates, you only need to **replace the sibling `nanobot-main/` folder**.

---

### 2) Where your config/data is stored

`newui.exe` stores settings in your user profile (so moving the app folder won’t lose config):

- **Main config**: `C:\Users\<you>\.nanobot\config.json`
- **newui log**: `C:\Users\<you>\.nanobot\newui\newui.log`
- **Skills folder**: `C:\Users\<you>\.nanobot\workspace\skills\`
- **Cron jobs file**: shown in the “Cron” window (usually under `~\.nanobot\...`)

#### 2.1 Backup / migrate to a new PC

Backup these two locations:

- `C:\Users\<you>\.nanobot\config.json`
- `C:\Users\<you>\.nanobot\workspace\`

On a new PC, restore them to the same paths and unzip `newui.dist/` anywhere.

---

### 3) Main window: day-to-day usage

The main UI has a chat area on the right, a session list on the left, and **Settings** on the top right.

#### 3.1 First time: set your API key

- Click **Settings** → **Set API Key**
- Choose your provider (openrouter / openai / custom / etc.)
- Paste the API key
- Save

Then go back to chat and send “Hello” as a test.

#### 3.1.1 Detailed: how to configure your LLM API (copy/paste)

In the “Set LLM Provider” dialog you will see:

- **Active Provider** (dropdown)
- **API Key**
- **API Base URL** (optional; mostly for custom/compatible endpoints)
- **Default model** (saved into `agents.defaults.model`)

Two important buttons:

- **Test connection**: sends a tiny request (“Say OK”) using your current inputs
- **Save**: saves the config and restarts the embedded agent so it takes effect immediately

Common setups:

##### A) OpenRouter

1) Active Provider: `OpenRouter (openrouter)`  
2) API Key: usually starts with `sk-or-`  
3) API Base: leave empty (default)  
4) Model: e.g. `anthropic/claude-opus-4-5`  

##### B) OpenAI

1) Active Provider: `OpenAI (openai)`  
2) Paste your OpenAI API key  
3) API Base: leave empty unless you use a proxy/Azure/compatible endpoint  
4) Model: e.g. `gpt-4o-mini` (example)  

##### C) DeepSeek

1) Active Provider: `DeepSeek (deepseek)`  
2) Paste your DeepSeek key  
3) Do **not** set API Base to openrouter.ai  
4) Model: e.g. `deepseek/deepseek-chat` (example)  

##### D) Custom (OpenAI-compatible endpoint / local model server)

1) Active Provider: `Custom (custom)`  
2) API Key: fill it if your endpoint requires auth (some endpoints still require a non-empty key)  
3) API Base examples:
   - `http://127.0.0.1:8000/v1`
   - `https://your-domain.com/v1`
4) Model: whatever your server supports  

#### 3.1.2 Quick switching provider/model (without changing keys)

At the top of the chat area you can switch **Provider / Model** and click **Switch**.

- This is for quickly changing the model once keys are already configured.
- Switching restarts the embedded agent automatically.

#### 3.2 Sessions (conversation tabs)

- Click **+ New session** for a clean chat
- Right-click a session to rename/delete

#### 3.3 Bottom status bar (important)

The status bar shows:

- what the app is doing
- elapsed time

Click it to open detailed logs (useful when it looks “stuck”).

---

### 4) Configure chat channels (Telegram / Slack / Email / Mochat / etc.)

Click **Configure channels**:

- choose a channel
- fill required fields
- for Telegram/Slack/Email/Mochat, the UI may auto-expand advanced optional fields
- click **Save**

Then start the gateway.

#### 4.1 Telegram (recommended)

Fields:

- `Bot Token`
- `allowFrom` (optional, comma-separated)

Steps:

1) Open `https://t.me/BotFather`
2) Create a bot with `/newbot`
3) Paste the token into `Bot Token`
4) (Recommended) set `allowFrom` to limit who can use the bot
5) Save → Start gateway

#### 4.2 Slack (Socket Mode)

Fields:

- `Bot Token (xoxb-...)`
- `App Token (xapp-...)`

High-level steps:

1) Create an app at `https://api.slack.com/apps`
2) Enable Socket Mode and create an App-Level token (`xapp-...`)
3) Install the app to your workspace to obtain the Bot token (`xoxb-...`)
4) Save → Start gateway and test

#### 4.3 Email (IMAP/SMTP)

Fill IMAP/SMTP host, username, password (often an “app password”), and fromAddress.  
Recommended: use a dedicated mailbox for the bot.

#### 4.4 Mochat (Claw IM)

Fill `claw_token` and `agent_user_id`, then save and start gateway.

#### 4.5 WhatsApp (bridge required)

Fill the bridge websocket url (default `ws://localhost:3001`).  
You must run a WhatsApp bridge (usually Node.js) and login first.

---

### 5) Start/Stop gateway

- **Start gateway**: enables channel messaging based on your `config.json`
- **Stop gateway**

If you changed cron/jobs or some config, you may need to restart the gateway for changes to apply.

---

### 6) Cron (scheduled tasks)

Open **Cron** and create:

- one-time tasks (run once at a date/time)
- repeating tasks (every N seconds)

The “message content” is what nanobot will receive at run time.

---

### 7) Skills (SKILL.md)

Skills are folders with a `SKILL.md` file that teaches the agent a workflow.

In **Skills Manager** you can:

- enable built-in skills (copy to workspace)
- import a skill folder (must contain `SKILL.md`)
- create a custom skill (template)

Use in chat:

- “Use skill <skill-name> to …”

---

### 8) MCP Servers (advanced tools)

Add MCP servers in the MCP Manager:

- **stdio**: command + args (nanobot starts the process and talks over stdio)
- **HTTP**: url (you run the server elsewhere)

After connecting, tools are registered as:

- `mcp_<serverName>_<toolName>`

Use in chat:

- “Use mcp_<server>_<tool> with params {...}”

---

### 9) Settings → Install dependencies (pip)

If you see:

- `No module named 'xxx'`

Go to **Settings → Install dependencies**, install `xxx`, then restart `newui.exe`.

---

### 10) Integrate your existing programs (exe / bat)

You can ask in chat:

- “Run `C:\Path\To\App.exe`”
- “Execute `C:\tools\do_something.bat`”

You can also schedule it via Cron.

Security note: don’t run unknown scripts/programs; backup important files first.

