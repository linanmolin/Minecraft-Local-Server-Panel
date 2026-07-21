# Minecraft 服务器远程网页控制面板 （仅限局域网，除非你具备IPV6或者公网IP）
这是一款基于 Flask + Socket.IO 搭建的多实例 Minecraft 服务器网页管理面板，内置 Java 环境管理、文件操作、资源监控、交互式网页终端、一键下载服务端核心等多项功能。

## 核心功能
1. **多实例管理**
一键创建、删除、启动、停止、重启服务器实例。
2. **智能 Java 版本匹配**
自动扫描本地 Java 文件夹，根据 Minecraft 版本自动匹配适配的最优 Java 运行环境；支持手动切换版本，配置永久保存。
3. **集成 xterm 网页终端**
功能完整的浏览器终端模拟器，支持命令历史、彩色日志、实时输出，可直接发送游戏指令。
4. **可视化文件管理器**
完整右键菜单：浏览、在线编辑、剪切/复制/粘贴、重命名、删除、新建文件夹、压缩解压；支持批量文件操作。
5. **全方位资源监控**
实时展示整机 CPU、内存、硬盘、网络占用；单独查看每个 Minecraft 实例进程的资源消耗。
6. **网络配置管理**
底部状态栏展示自定义绑定IP与端口、局域网IP、公网IP；可直接在面板内修改服务器绑定地址和端口。
7. **一键下载服务端核心**
自动获取原版、Fabric、Forge 三类服务端核心文件。
8. **安全增强机制**
强制终止完整 Java 进程树、全局清理残留 Java 进程、内置 EULA 协议确认校验。
9. **便捷文件传输**
支持单文件、文件夹上传下载；下载文件夹时自动打包为 ZIP，无需手动压缩。
10. **可视化世界种子管理**
可视化修改世界种子，附带一键重置世界按钮；修改种子后弹窗提醒用户删除 world 文件夹。

## 技术栈
### 后端
Python 3、Flask、Flask-SocketIO、psutil

### 前端
HTML5、CSS3、JavaScript、xterm.js、Socket.IO

### 依赖项
程序首次运行时会自动检测并安装缺失模块（flask、flask-socketio、psutil、requests 等）。

## 快速上手教程
1. 环境要求：安装 Python 3.9 及以上版本
2. 将主脚本 `Server.py` 放置在任意文件夹中
3. 直接运行脚本，首次启动会自动安装全部所需依赖
4. 打开浏览器访问 `http://127.0.0.1:8080` 即可进入控制面板

### 可选配置：内置 Java 运行环境
在 `Server.py` 同级目录新建名为 `Java` 的文件夹，将解压后的 JDK 放入其中，目录示例：
Java/
└── jdk-21.0.10/
### 数据存储目录
所有创建的 Minecraft 服务器实例，统一存放于脚本同级的 `Server` 文件夹内。

## 版本更新日志
### v5.3（初始发布版）
- 基础多实例控制：启动、停止、重启、发送游戏指令
- 强制关机时完整终止 Java 进程树，清理残留进程
- 网页终端工具栏、单实例 CPU/内存资源监控
- 基础文件浏览、在线编辑功能
- 支持自动下载原版、Fabric、Forge 服务端核心

### v5.4
- 新增独立 Java 版本选择标签页，自动扫描本地所有 JDK
- 可手动指定 Java 路径启动服务器；未指定时自动使用系统 Java
- 保存 Java 选择配置，重启程序后配置不丢失

### v5.5
- 升级 Java 自动匹配功能：通过 `version.json` 或文件名识别 MC 版本，推荐兼容 JDK
- 修复前端反斜杠导致 Java 路径失效的漏洞，改用 data 属性传递路径参数
- 新增启动失败计数器；多次启动失败后弹窗提示使用 Java 自动匹配功能

### v5.6
- 文件管理器完整实装右键菜单：刷新、编辑、剪切/复制/粘贴、重命名、新建文件夹、压缩解压、删除
- 后端扩充全套文件操作接口，支持跨实例文件操作
- 新增「更新网络」按钮，可直接修改 `server.properties` 内绑定IP与端口

### v5.7
- 状态栏实时展示网络信息：自定义服务器IP端口、局域网IP、公网IP，关键信息高亮显示
- 优化实例选择界面：仅展示文件夹名称+版本，隐藏冗余核心文件名
- 支持创建名称含空格的服务器实例
- 种子管理优化：修改种子后提醒删除 world 文件夹，新增一键重置世界按钮

### v5.8
- 修复下载文件夹出现 500 错误的问题（临时 ZIP 文件冲突）
- 下载文件夹时自动压缩为 ZIP 包，无需手动操作
- 全部现有功能稳定优化，界面精简

### v5.9
- **压缩/解压冲突检测**：压缩或解压时若目标文件（夹）已存在，弹出确认对话框询问是否覆盖，避免误操作导致数据丢失
- **文件传输面板右键菜单**：📦 文件传输标签页全面支持右键操作——下载、压缩、解压、重命名、新建文件夹、删除、刷新
- **资源管理器右键菜单增强**：🗂 资源管理器右键菜单新增压缩/解压（含冲突提示）、重命名、新建文件夹、删除等完整操作
- **后端新增传输面板 API**：`/api/transfer/delete`、`/api/transfer/rename`、`/api/transfer/mkdir`，实现传输面板完整 CRUD
- **ConflictError 异常机制**：新增冲突异常类，统一处理压缩/解压同名冲突，后端返回 HTTP 409 状态码 + 冲突信息，前端自动弹出覆盖确认

### v6.0（重大更新）
- **🔐 强制登录验证**：首次运行配置管理员邮箱，启用 SMTP + POP3 双重验证；登录需获取 16 位一次性密钥，刷新页面或超时自动退出
- **🔗 主机名绑定与重定向**：默认使用 `mc.panel.lan` 访问面板，非该域名请求自动重定向至登录页，简化内网访问
- **📦 SysBack 实例备份系统**：
  - 创建备份时自动停止实例，将文件归档为 `.Mpba`（普通文件）和 `.zip.Mpzp`（文件夹压缩包），完成后自动恢复运行
  - 还原备份前默认创建“还原前备份”防止数据丢失，支持强制覆盖（需三次确认）
  - 操作全程冻结面板，显示蓝色进度条
- **📧 邮件模板全面升级**：密钥邮件改用精美 HTML 样式，包含安全提示和访问链接
- **🐳 Docker 镜像优化**：`Dockerfile` 自动生成，支持将 `.py` 和预编译的 `.exe` 文件同时打包至容器
- **🔄 下载鉴权修复**：文件传输和资源管理器的下载功能改用 fetch + API Token，避免 401 未授权错误
- **📄 打包兼容性增强**：修复 PyInstaller 打包后因 `engineio` 异步驱动缺失导致的启动失败问题
- **🌐 启动提示优化**：开发服务器日志统一显示为 `https://mc.panel.lan:8080`，方便复制使用

---

English：
# Minecraft Server Remote Web Control Panel
A multi-instance Minecraft server web management panel built with Flask + Socket.IO. It features built-in Java management, file operations, resource monitoring, interactive web terminals, one-click server core download and more.

## Key Features
1. **Multi-Instance Management**
One-click creation, deletion, start, stop and restart of server instances.
2. **Intelligent Java Version Matching**
Scans the local Java directory and automatically selects the optimal Java runtime based on your Minecraft version. Manual version switching with persistent saved configurations is supported.
3. **Integrated xterm Web Terminal**
Fully functional in-browser terminal emulator with command history, colored logs and real-time output, allowing direct in-game command input.
4. **Visual File Manager**
Complete right-click context menu: browse, online edit, cut/copy/paste, rename, delete, create folders, compress & decompress files; supports batch file operations.
5. **Comprehensive Resource Monitoring**
Real-time display of system-wide CPU, RAM, disk and network usage; separate resource consumption stats for each Minecraft instance process.
6. **Network Configuration Management**
Status bar displays custom bound IP & port, local LAN IP and public IP. You can directly modify server binding address and port inside the panel.
7. **One-Click Server Core Downloader**
Automatically fetch vanilla, Fabric and Forge server core files.
8. **Security Enhancements**
Force termination of full Java process trees, global cleanup of leftover Java processes, built-in EULA agreement validation.
9. **Convenient File Transfer**
Single file & folder upload/download; folders are automatically zipped during download without manual compression.
10. **Visual World Seed Manager**
Visually edit world seeds with a dedicated world reset button. A warning pops up to remind users to delete the `world` folder after seed changes.

## Tech Stack
### Backend
Python 3, Flask, Flask-SocketIO, psutil

### Frontend
HTML5, CSS3, JavaScript, xterm.js, Socket.IO

### Dependencies
Missing modules (flask, flask-socketio, psutil, requests, etc.) are automatically detected and installed on first launch.

## Quick Start Guide
1. Environment Requirement: Python 3.9 or higher installed
2. Place the main script `Server.py` in any directory
3. Run the script directly; all required dependencies will be installed automatically on first startup
4. Open your browser and visit `http://127.0.0.1:8080` to access the control panel

### Optional: Built-in Java Runtime Setup
Create a folder named `Java` in the same directory as `Server.py`, then extract your JDK build inside it. Example structure:

Java/
└── jdk-21.0.10/

### Data Storage Directory
All created Minecraft server instances are stored in the `Server` folder alongside the main script.

## Version Changelog
### v5.3 (Initial Release)
- Basic multi-instance controls: start, stop, restart and in-game command sending
- Complete Java process tree termination on forced shutdown to clean residual processes
- Web terminal toolbar & per-instance CPU/RAM resource monitoring
- Basic file browsing and online editing functions
- Automatic download support for Vanilla, Fabric and Forge server cores

### v5.4
- New dedicated tab for Java version selection, auto-scans all local JDK builds
- Manually specify Java path for server startup; system Java is used if no custom path is set
- Saves Java selection settings and retains them after program restarts

### v5.5
- Upgraded automatic Java matching: identifies Minecraft versions via `version.json` or filenames and recommends compatible JDKs
- Fixed frontend bug causing invalid Java paths from backslashes; uses data attributes for path transmission
- Added startup failure counter; prompts users to use auto Java matching after repeated launch failures

### v5.6
- Full right-click context menu implemented for file manager: refresh, edit, cut/copy/paste, rename, create folders, compress/decompress, delete
- Backend API expanded with full file operation endpoints, supporting cross-instance file operations
- Added "Update Network" button to directly edit bound IP and port inside `server.properties`

### v5.7
- Real-time network info displayed on status bar: custom server IP & port, LAN IP, public IP with highlighted key information
- Optimized instance selector UI: only shows folder names + versions, hiding redundant core filenames
- Support for server instance names containing spaces
- Improved seed management: reminder to delete the `world` folder after seed edits, plus one-click world reset button

### v5.8
- Fixed 500 Internal Server Error when downloading folders (temporary ZIP file conflict resolution)
- Folders are auto-compressed to ZIP before download with no manual steps required
- Stabilized all existing features with streamlined UI

### v5.9
- **Compression/Decompression Conflict Detection**: When compressing or extracting files, if the target file/folder already exists, a confirmation dialog appears asking whether to overwrite, preventing accidental data loss
- **File Transfer Panel Right-Click Menu**: The 📦 File Transfer tab now fully supports right-click operations — download, compress, decompress, rename, create folder, delete, refresh
- **Resource Manager Right-Click Menu Enhanced**: The 🗂 Resource Manager's context menu now includes compress/decompress (with conflict prompts), rename, create folder, and delete operations
- **New Transfer Panel Backend APIs**: `/api/transfer/delete`, `/api/transfer/rename`, `/api/transfer/mkdir` endpoints added for complete CRUD functionality in the transfer panel
- **ConflictError Exception Mechanism**: New conflict exception class unifies handling of same-name conflicts during compression/decompression; backend returns HTTP 409 + conflict info, frontend automatically shows overwrite confirmation dialog

### v6.0 (Major Update)
- **🔐 Enforced Login Authentication**: First-run configuration requires an admin email with SMTP + POP3 dual verification; login obtains a one-time 16-character key; page refresh or timeout forces re-login.
- **🔗 Hostname Binding & Redirection**: Default access via `mc.panel.lan`; any request not using this hostname is automatically redirected to the login page, simplifying LAN access.
- **📦 SysBack Instance Backup System**:
  - Creating a backup automatically stops the instance, archives files with `.Mpba` (plain files) and `.zip.Mpzp` (compressed folders), then resumes operation.
  - Restoring a backup creates a "pre-restore" safety backup by default to prevent data loss; forced overwrite requires a triple confirmation.
  - The entire operation freezes the panel UI and displays a blue progress bar.
- **📧 Email Template Overhaul**: Login code emails now use a polished HTML style with security tips and access link.
- **🐳 Docker Image Enhancement**: Auto-generated `Dockerfile` now includes both `.py` scripts and precompiled `.exe` files for easier deployment.
- **🔄 Download Authentication Fix**: File and resource manager downloads now use fetch + API Token, preventing 401 Unauthorized errors.
- **📄 Packing Compatibility**: Fixed PyInstaller startup failure caused by missing `engineio` async driver.
- **🌐 Improved Startup Notice**: Development server logs now uniformly display `https://mc.panel.lan:8080` for easy copying.
