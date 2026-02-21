# nanobot-ui（Windows 可视化 UI for nanobot）

`nanobot-ui` 是一个面向普通用户的 **Windows 可视化前端**：不用懂代码，也能完成 nanobot 的安装依赖、API 配置、社交平台接入（Telegram/Slack/Email 等）、MCP 工具接入、技能管理与定时任务等操作。

本项目致敬并兼容香港大学开源项目 [HKUDS/nanobot](https://github.com/HKUDS/nanobot)。

> nanobot is an ultra-lightweight personal AI assistant inspired by [OpenClaw](https://github.com/openclaw/openclaw)

---

### 你会喜欢 nanobot-ui 的原因（给普通用户）

- **不需要安装 Python**：下载解压后即可运行 `newui.exe`
- **可视化配置**：API Key / 模型 / 社交平台 / MCP / 技能 / 定时任务，都在界面里点选
- **操作透明**：底部状态栏实时显示“正在做什么 + 已耗时”，可点击查看详情日志
- **可升级不折腾**：nanobot 官方项目更新后，你只需替换同级目录的 `nanobot-main/` 文件夹即可继续使用

---

### 快速开始（3 分钟）

1) **下载发布包**  
在本仓库的 Releases 下载 Windows 打包包（包含 `newui.exe` 的 `newui.dist/` 目录）。

2) **放置 nanobot 官方项目（可随时替换更新）**  
从官方仓库下载/解压 nanobot：  
[HKUDS/nanobot](https://github.com/HKUDS/nanobot)

把它放到 `newui.exe` 同级目录，结构如下：

```
newui.dist/
  newui.exe
  nanobot-main/        <-- 放这里（来自 HKUDS/nanobot）
    nanobot/
    pyproject.toml
    requirements.txt
    ...
```

3) **启动 newui.exe**  
双击 `newui.exe`，按界面提示完成：

- **设置 API Key**（带“测试连接”按钮）
- 选择默认模型
- （可选）配置社交平台并启动网关

---

### 如何升级 nanobot（无需重发 newui.exe）

当 [HKUDS/nanobot](https://github.com/HKUDS/nanobot) 更新时：

- 重新下载官方项目
- 直接**替换** `newui.exe` 同级目录的 `nanobot-main/` 文件夹

`newui.exe` 本身不需要重新打包即可继续使用（保持完全兼容为目标）。

---

### 文档（建议先看）

- 普通用户手册：[`../普通用户使用手册.md`](./普通用户使用手册.md)
- 开发人员手册（技能/MCP/依赖机制）：[`./开发人员使用手册.md`](../开发人员使用手册.md)

---

### 点亮 Star

如果这个项目让你 **不用写代码也能用 nanobot**，请点亮右上角 **Star**，这对项目曝光非常重要。


