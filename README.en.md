# nanobot-ui (Windows GUI for nanobot)

`nanobot-ui` is a **Windows desktop GUI** that makes [HKUDS/nanobot](https://github.com/HKUDS/nanobot) usable for non-programmers: configure LLM API keys, connect chat channels (Telegram/Slack/Email, etc.), manage Skills, connect MCP tool servers, run the gateway, and schedule tasks — all from a visual UI.

This project is a tribute to and stays compatible with the official nanobot project:

> nanobot is an ultra-lightweight personal AI assistant inspired by [OpenClaw](https://github.com/openclaw/openclaw)

---

### Why nanobot-ui (for non-coders)

- **No Python installation required**: run `newui.exe` after unzipping
- **Visual setup**: API keys, models, channels, MCP, skills, cron — click to configure
- **Transparent operations**: a status bar shows *what it's doing + elapsed time*, click for detailed logs
- **Easy upgrades**: when official nanobot updates, just replace the sibling `nanobot-main/` folder — no need to rebuild `newui.exe`

---

### Quick start (3 minutes)

1) **Download the release**  
Download the Windows release from this repository (the `newui.dist/` folder containing `newui.exe`).

2) **Place the official nanobot project next to `newui.exe`**  
Download/zip the official project from:  
[HKUDS/nanobot](https://github.com/HKUDS/nanobot)

Put it as a sibling folder:

```
newui.dist/
  newui.exe
  nanobot-main/        <-- put HKUDS/nanobot here
    nanobot/
    pyproject.toml
    requirements.txt
    ...
```

3) **Run `newui.exe`**

- Open **Settings → Set API Key**, click **Test connection**, then **Save**
- Pick a default model
- (Optional) configure a chat channel and start the gateway

---

### Updating nanobot without rebuilding the UI

When [HKUDS/nanobot](https://github.com/HKUDS/nanobot) releases a new version:

- download the updated project
- replace the `nanobot-main/` folder next to `newui.exe`

`newui.exe` remains the same.

---

### Documentation

- User manual: [`../普通用户使用手册_en.md`](./普通用户使用手册_en.md)
- Developer manual (Skills/MCP/packaged dependency mechanism): [`./开发人员使用手册_en.md`](./开发人员使用手册_en.md)

---

### Star the project

If this project helps you use nanobot **without writing code**, please give it a **Star** — it helps a lot.


