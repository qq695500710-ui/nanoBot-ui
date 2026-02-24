2026-02-25 Update Content
Synchronized and implemented the core changes recorded in up.md (related to QQ / Feishu, multimodal 'previous image' follow feature).
Currently fixing some issues with Chinese character display glitches.
Currently fixing the issue where Feishu cannot be configured after QQ configuration.
Adapting to the latest official nanobot project code version 2026-02-21.
Submitted 3 code fixes related to QQ and Feishu to the official University of Hong Kong project (PR): https://github.com/HKUDS/nanobot/pull/1137
Added manual memory addition in the visualization page (the original project automatically archived every 50 entries; now it is 'automatic archiving with manual addition in visualization').
New project website: http://www.ie95.com
If you encounter any problems or have any suggestions during use, please feel free to contact us; all feedback will be recorded and gradually improved.

Introduction to features being updated in the next version:
Web Interface / Webpage: The goal is to access it via 127.0.0.1:port; after server configuration, domain access can be realized through reverse proxy.
Website customization: Supports copying the web development rules to the AI, allowing AI to customize personalized pages according to your requirements.



======================================================
#  [`点击下载 /DOWNLOAD`](https://github.com/qq695500710-ui/nanoBot-ui/releases/download/nanobot-ui2.0/nanobot-ui2.0.zip)
======================================================

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

**Interface image**


Visual dialogue page: Supports direct modification of computer files, supports drag-and-drop, supports all functions of the original project, and currently, after modification, it is almost the same as the cursor function (the difference is that the modified content cannot be seen for comparison)

<img width="934" height="568" alt="Screen capture 2026-02-21 230448" src="https://github.com/user-attachments/assets/8f340d6b-59d2-4b38-8712-c73a505e3d68" />

Settings Page

<img width="590" height="409" alt="Screen capture 2026-02-21 230614" src="https://github.com/user-attachments/assets/24742400-7c85-4482-bd0a-f2c684172728" />

The API configuration page supports all AI providers supported by nanobot projects

<img width="471" height="482" alt="Screen capture 2026-02-21 230832" src="https://github.com/user-attachments/assets/35d80a8f-fef6-475e-8a69-0c22faf3cda0" />

The chat platform configuration page supports all chat dialogues supported by the nanobot project

<img width="552" height="433" alt="Screen capture 2026-02-21 230939" src="https://github.com/user-attachments/assets/140831b4-9316-460a-9ba9-2243e5503bc9" />

QQ direct conversation for control: The screenshot shows a test conversation in a browser

<img width="1658" height="515" alt="Screen capture 2026-02-21 231047" src="https://github.com/user-attachments/assets/a2782ea2-1091-4961-9055-5dbb24c25b7a" />

Install dependency function: Usage scenario, for example: If your project is an unpacked Python script and requires installing dependencies, you can directly enter the command to install dependencies here.

<img width="677" height="432" alt="Screen capture 2026-02-21 231145" src="https://github.com/user-attachments/assets/d750f05f-710f-4a40-8fef-e243fb277c99" />

Activate the gateway function:
After configuring QQ, click to launch the gateway, and then you can control the computer through AI conversation in the QQ chat window

Scheduled task function:
Initiate skills, MCP, or perform straightforward dialog operations through AI dialog control.

Memory management function:

<img width="766" height="532" alt="Screen capture 2026-02-21 231421" src="https://github.com/user-attachments/assets/63ec2a76-79d2-4d9e-b10b-1d9e8bcf468d" />

Skill management function:

<img width="773" height="511" alt="Screen capture 2026-02-21 231505" src="https://github.com/user-attachments/assets/7f1720f4-d694-41e4-92e5-c5a2c3ec529d" />

MCP management function:

<img width="772" height="489" alt="Screen capture 2026-02-21 231543" src="https://github.com/user-attachments/assets/061f7795-d5d4-49b9-8511-c03a58127fe6" />

