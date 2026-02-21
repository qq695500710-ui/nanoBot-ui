# nanobot-ui（Windows 視覺化 UI for nanobot）

`nanobot-ui` 是面向一般使用者的 **Windows 視覺化前端**：不用懂程式，也能完成 nanobot 的依賴安裝、API 設定、社群平台接入（Telegram/Slack/Email 等）、MCP 工具接入、技能管理與排程任務等操作。

本專案致敬並相容香港大學開源專案 [HKUDS/nanobot](https://github.com/HKUDS/nanobot)。

> nanobot is an ultra-lightweight personal AI assistant inspired by [OpenClaw](https://github.com/openclaw/openclaw)

---

### 你會喜歡 nanobot-ui 的原因（給一般使用者）

- **不需要安裝 Python**：下載解壓後即可執行 `newui.exe`
- **視覺化設定**：API Key / 模型 / 社群平台 / MCP / 技能 / 排程任務，都能在介面操作
- **操作透明**：底部狀態列即時顯示「正在做什麼 + 已耗時」，可點擊查看詳細日誌
- **可升級不折騰**：nanobot 官方更新後，只要替換同級目錄的 `nanobot-main/` 就能繼續使用

---

### 快速開始（3 分鐘）

1) **下載發佈包**  
在本倉庫 Releases 下載 Windows 打包包（包含 `newui.exe` 的 `newui.dist/` 目錄）。

2) **放置 nanobot 官方專案（可隨時替換更新）**  
從官方倉庫下載/解壓 nanobot：  
[HKUDS/nanobot](https://github.com/HKUDS/nanobot)

把它放到 `newui.exe` 同級目錄，結構如下：

```
newui.dist/
  newui.exe
  nanobot-main/        <-- 放這裡（來自 HKUDS/nanobot）
    nanobot/
    pyproject.toml
    requirements.txt
    ...
```

3) **啟動 newui.exe**  
雙擊 `newui.exe`，依照介面提示完成：

- **設定 API Key**（含「測試連線」按鈕）
- 選擇預設模型
- （可選）設定社群平台並啟動網關

---

### 如何升級 nanobot（不必重發 newui.exe）

當 [HKUDS/nanobot](https://github.com/HKUDS/nanobot) 更新時：

- 重新下載官方專案
- 直接**替換** `newui.exe` 同級目錄的 `nanobot-main/` 資料夾

`newui.exe` 本身不需要重新打包即可繼續使用（以完全相容為目標）。

---

### 文件（建議先看）

- 一般使用者手冊：[`../普通用户使用手册_繁體.md`](../普通用户使用手册_繁體.md)
- 開發者手冊（技能/MCP/依賴機制）：[`../开发人员使用手册_繁體.md`](../开发人员使用手册_繁體.md)

---

### 點亮 Star

如果這個專案讓你 **不用寫程式也能用 nanobot**，請點亮右上角 **Star**，這對專案曝光非常重要。

