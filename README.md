```markdown
# 🎮 MC Panel v5.9 — Minecraft 服务器远程网页控制面板

**语言 / Language**：本面板完整支持 **中文 (zh-CN)** 界面。本文档同时提供 [English version](#english-version) below.

---

## 📖 项目简介

**MC Panel** 是一款基于 Flask + Socket.IO 构建的多实例 Minecraft 服务器网页管理面板。你可以在浏览器中完成**创建、启停、监控、配置文件编辑、文件传输、Java 版本切换、服务端核心下载**等全部操作——无需登录服务器桌面，一切尽在 Web 端掌控。

> ⚡ **零配置启动**：首次运行自动安装依赖，双击 Python 脚本即用。
> 🧠 **智能 Java 匹配**：自动识别服务端核心所需的 JDK 版本，告别 `UnsupportedClassVersionError`。
> 🖱 **完整右键菜单**：实例文件、传输面板、资源管理器均支持上下文操作。
> 🧩 **中文优先**：整个前端界面使用中文，同时后端逻辑完全国际化。

---

## ✨ 核心功能

| 功能 | 说明 |
|------|------|
| 🖥 **多实例管理** | 一键创建、删除、启动、停止、重启、强制终止服务器实例 |
| ☕ **Java 版本管理** | 自动扫描内置 `Java` 目录及系统 Java；手动选择 / 自动匹配最优版本；设置永久保存 |
| 💻 **xterm 网页终端** | 完整终端模拟器，支持命令历史、彩色日志、实时输出，可直接发送游戏指令 |
| 📁 **文件管理器** | 浏览实例文件、在线编辑文本、右键操作（复制/剪切/粘贴/重命名/删除/新建文件夹） |
| 🗂 **资源管理器** | 浏览电脑全部磁盘分区，跨磁盘复制/迁移文件，右键压缩/解压（含冲突提示） |
| 📦 **文件传输面板** | 实例与中转目录之间上传/下载；下载文件夹自动打包为 ZIP；右键全面支持 |
| 📊 **资源监控** | 实时显示系统整机及单个实例的 CPU、内存、硬盘、网络速率 |
| 🌐 **网络信息展示** | 状态栏显示服务器绑定 IP/端口、局域网 IP、公网 IP（通过 ipify.org 获取） |
| 📥 **一键下载核心** | 自动拉取 Mojang 官方原版 / Fabric / Forge 服务端核心文件 |
| ⚙️ **server.properties 编辑器** | 可视化修改所有服务器属性；独立修改 IP 绑定与端口 |
| 🌍 **种子管理** | 一键修改世界种子 + 重置世界文件夹 |
| 🛡 **安全机制** | EULA 协议确认；强制终止完整 Java 进程树；全局清理残留 Java 进程 |
| 🔥 **隐藏彩蛋** | 连续点击 4 次「强制开机」触发倒计时动画，执行带清理的强制启动 |
| 🧩 **压缩/解压冲突提示** | 同名文件弹出覆盖确认对话框，防止误操作 |

---

## 🛠 技术栈

| 层级 | 技术 |
|------|------|
| 后端 | Python 3.9+、Flask、Flask-SocketIO、psutil |
| 前端 | HTML5、CSS3、原生 JavaScript、xterm.js 5.3、Socket.IO 4.7 |
| 依赖管理 | 首次启动自动检测安装 (`pip install -q`) |

---

## 🚀 快速上手

```bash
# 1. 环境要求：Python 3.9 及以上
python --version

# 2. 将 Server.py（或 Server zh-cn.py）放到任意文件夹

# 3. 运行脚本（首次启动自动安装依赖）
python "Server zh-cn.py"

# 4. 浏览器打开
http://127.0.0.1:8080
```

### 可选：内置 Java 环境

在脚本同目录新建 `Java` 文件夹，放入 JDK 即可被自动识别：

```
你的文件夹/
├── Server zh-cn.py
├── Java/
│   ├── jdk-17.0.10/
│   └── jdk-21.0.5/
└── Server/          ← 实例数据存放目录（自动创建）
```

---

## 📊 版本更新日志

### v5.3 — 初始发布
- 基础多实例控制、chrome 终端、文件浏览、原版/Fabric/Forge 核心下载

### v5.4
- 新增 Java 选择标签页，自动扫描 JDK，手动切换 / 自动匹配，配置持久化

### v5.5
- 通过 `version.json` 精准识别 MC 版本；Java 路径使用 data 属性防转义

### v5.6
- 文件管理器完整右键菜单；跨实例复制粘贴；`server.properties` 网络配置

### v5.7
- 网络信息状态栏；实例名支持空格；种子重置按钮

### v5.8
- 修复下载文件夹 500 错误；文件夹自动打包为 ZIP

### v5.9 (最新)
- **压缩/解压冲突检测**：同名文件弹出覆盖确认
- **传输面板右键菜单**全面支持下载/压缩/解压/重命名/新建文件夹/删除
- **资源管理器右键菜单**增强
- 新增 3 个传输面板后端 API (`/api/transfer/delete|rename|mkdir`)
- `ConflictError` 异常机制统一处理冲突

---

## ⚠️ 注意事项

1. Windows 下强制终止 Java 进程可能需要**管理员权限**；普通启动无需
2. 修改种子后请使用「重置世界」按钮清除旧的 `world` 文件夹
3. 公网 IP 依赖 `ipify.org` 接口，无网络时显示 `——`
4. 压缩/解压遇到同名文件时会弹出确认框，请按需选择

---

## 📜 许可

MIT License · 仅供学习与非商业用途

---

<p align="center">
  <br>
  <strong>⭐ 如果这个项目对你有用，欢迎给个 Star！</strong>
</p>

---

# English Version

## 🎮 MC Panel v5.9 — Minecraft Server Web Control Panel

**Language**: The panel UI is fully in **Chinese (zh-CN)**. The English mirror of this README is provided below.

---

## 📖 Overview

**MC Panel** is a multi-instance Minecraft server management panel built with Flask + Socket.IO. Create, start, stop, monitor, configure and transfer files for all your Minecraft server instances — entirely from your browser.

> ⚡ **Zero config**: auto-installs dependencies on first launch.
> 🧠 **Smart Java matching**: automatically picks the right JDK for each Minecraft version.
> 🖱 **Full right-click context menus**: available in Instance Files, Transfer Panel and Resource Explorer.
> 🧩 **Chinese-first UI** with internationalized backend logic.

---

## ✨ Key Features

| Feature | Description |
|---------|-------------|
| 🖥 Multi-Instance | Create, delete, start, stop, restart, force-kill servers |
| ☕ Java Manager | Auto-scan local JDKs + system Java; manual select & auto matching; persistent settings |
| 💻 xterm Terminal | Full terminal emulator, command history, colored logs, live output |
| 📁 File Manager | Browse, online edit, cut/copy/paste, rename, delete, create folders |
| 🗂 Resource Explorer | Browse all disk partitions, cross-drive file ops, compress/decompress with conflict prompts |
| 📦 Transfer Panel | Upload/download files & folders; folders auto-zipped on download; full right-click support |
| 📊 Monitoring | Real-time system & per-instance CPU/RAM/Disk/Network stats |
| 🌐 Network Info | Bound IP/Port, LAN IP, Public IP displayed on status bar |
| 📥 Core Downloader | One-click fetch Vanilla / Fabric / Forge server cores |
| ⚙️ Properties Editor | Visual editor for `server.properties`; separate IP & port controls |
| 🌍 Seed Manager | Edit world seed + one-click world reset |
| 🛡 Safety | EULA validation; full Java process tree termination; global leftover cleanup |
| 🔥 Easter Egg | Click "Force Start" 4 times for a countdown animation & clean launch |
| 🧩 Conflict Detection | Overwrite confirmation dialog when compressing/extracting to existing files |

---

## 🛠 Tech Stack

| Layer | Technology |
|-------|------------|
| Backend | Python 3.9+, Flask, Flask-SocketIO, psutil |
| Frontend | HTML5, CSS3, Vanilla JavaScript, xterm.js 5.3, Socket.IO 4.7 |
| Deps | Auto-installed via pip on first run |

---

## 🚀 Quick Start

```bash
# 1. Requires Python 3.9+
python --version

# 2. Place Server.py (or Server zh-cn.py) in any folder

# 3. Run (auto-installs dependencies on first launch)
python "Server zh-cn.py"

# 4. Open browser
http://127.0.0.1:8080
```

### Optional: Bundled JDKs

Create a `Java/` folder next to the script and drop extracted JDK builds inside:

```
Your Folder/
├── Server zh-cn.py
├── Java/
│   ├── jdk-17.0.10/
│   └── jdk-21.0.5/
└── Server/          ← Instance data (auto-created)
```

---

## 📊 Changelog

### v5.3 — Initial Release
- Basic multi-instance control, xterm terminal, file browser, Vanilla/Fabric/Forge downloader

### v5.4
- Java selection tab, auto JDK scanning, manual switch & auto match, persistent config

### v5.5
- Precise MC version detection via `version.json`; Java path fixes with data attributes

### v5.6
- Full right-click menu in File Manager; cross-instance copy/paste; network property editor

### v5.7
- Network info status bar; spaces in instance names; world reset button

### v5.8
- Fixed 500 error on folder download; auto-zip folders before download

### v5.9 (Latest)
- **Compression/Decompression conflict detection** with overwrite confirm dialog
- **Transfer Panel right-click menu** fully supported (download/compress/decompress/rename/new folder/delete)
- **Resource Explorer right-click menu** enhanced
- 3 new Transfer API endpoints (`/api/transfer/delete|rename|mkdir`)
- `ConflictError` exception mechanism for unified conflict handling

---

## ⚠️ Notes

1. Windows: force-killing Java processes may require **admin privileges**; normal startup does not
2. After changing world seed, use the "Reset World" button to delete old `world` data
3. Public IP is fetched via `ipify.org`; displays `——` when unreachable
4. A confirmation dialog appears when compressing/extracting to a path that already exists

---

## 📜 License

MIT License · For personal learning and non-commercial use only

---

<p align="center">
  <br>
  <strong>⭐ Found this useful? Give it a Star!</strong>
</p>
```
