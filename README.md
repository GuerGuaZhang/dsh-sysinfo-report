# dsh-sysinfo-report

[DSH](https://github.com/deepseek-ai/dsh) skill plugin: Collect system hardware/software/network info and generate JSON for AI analysis.

DSH 技能插件：采集电脑硬件/系统/软件/网络信息，生成 JSON 供 AI 分析。

## ✨ Features / 功能

- Collect 26 system modules (CPU/RAM/Disk/GPU/OS/Software/Network etc.) / 采集 26 个系统模块
- Generate structured JSON for AI analysis / 生成结构化 JSON 供 AI 分析
- Mask sensitive info (serial numbers/MAC/IP/usernames) / 脱敏模式
- Organize reports by computer name / 按电脑名分目录存储
- Enhanced event logs for troubleshooting / 事件日志加强（12 类排查信息）
- Self-contained design (no PATH configuration needed) / 自包含设计（无需配置PATH）
- Windows 10 1809+ / Windows 11 support / 支持Windows 10 1809+ / Windows 11

## 🚀 Quick Start / 快速开始

### Prerequisites / 前置条件

- Windows 10 1809+ / Windows 11
- [SysInfoTool.exe](https://github.com/GuerGuaZhang/SysInfoTool/releases) (will be placed in skill directory)

### Installation / 安装

```bash
# Via DSH / 通过 DSH 安装
dsh plugin --profile <your-profile> add dsh-sysinfo-report

# Local install / 本地安装
dsh plugin --profile <your-profile> add /path/to/dsh-sysinfo-report
```

### Manual Setup / 手动设置

1. Download `SysInfoTool.exe` from [Releases](https://github.com/GuerGuaZhang/SysInfoTool/releases)
2. Place it in the skill directory:
   ```
   ~/.dsh/skills/sysinfo-report/
   ├── SKILL.md              ← Skill definition
   └── SysInfoTool.exe       ← Place exe here
   ```

### Usage / 使用

After installation, just say in conversation:

安装后，在对话中说：

- "生成电脑信息报告" / "Generate system info report"
- "看看这台电脑的配置" / "Check this computer's specs"
- "排查一下系统问题" / "Troubleshoot system issues"
- "导出硬件信息" / "Export hardware info"

AI will automatically call `SysInfoTool.exe --console --json-only` to generate JSON.

AI 会自动调用 `SysInfoTool.exe --console --json-only` 生成 JSON 报告。

## 📚 Variant Commands / 变体指令

| User says / 用户说 | Action / 执行 |
|-------------------|---------------|
| "生成电脑信息报告" | Full collection, output JSON+HTML / 完整采集，输出JSON+HTML |
| "看看这台电脑的配置" | Full collection, output JSON+HTML / 完整采集，输出JSON+HTML |
| "排查蓝屏问题" | Focus on event logs (Kernel-Power 41, WHEA errors) / 重点分析事件日志 |
| "检查硬盘健康" | Focus on disk health and error events / 重点分析硬盘健康状态 |
| "导出硬件信息（不脱敏）" | Use --no-mask parameter / 使用 --no-mask 参数 |
| "生成报告到D盘" | Use --out=D:\报告 parameter / 使用 --out=D:\报告 参数 |
| "只生成JSON" | Use --json-only parameter / 使用 --json-only 参数 |
| "系统卡顿排查" | Focus on performance snapshot and top processes / 重点分析性能快照 |

## 📦 Collected Modules / 采集内容

| Category / 分类 | Modules / 模块 |
|----------------|----------------|
| Hardware / 硬件 | CPU, Motherboard/BIOS/TPM, RAM (per-stick), Disk (HDD/SSD/NVMe/Health), GPU, Monitor, NIC, Audio, Battery, USB |
| System / 系统 | OS/Build/Activation, Updates, UEFI/Secure Boot, Pagefile, Restore Points, Environment Variables |
| Software / 软件 | Installed Programs, Startup Items, Services, Scheduled Tasks, Drivers, Browsers, Runtimes, Fonts |
| Traces / 痕迹 | User Directories, Recent Files, Recycle Bin, WiFi, Printers, Bluetooth, Shares |
| Performance / 性能 | Uptime, Memory Snapshot, Top Processes, Event Logs (12 types), BSOD Records |
| Network / 网络 | IP/Gateway/DNS/MAC, Proxy, Listening Ports |

## 📊 Event Logs / 事件日志

- System/App/Setup logs (Critical/Error/Warning) / 系统/应用/安装日志
- BSOD records (BugCheck 1001) / 蓝屏记录
- Unexpected shutdowns (Kernel-Power 41) / 意外关机/重启
- WHEA hardware errors / WHEA 硬件错误
- Disk errors (Event 7/11/15/51/55) / 磁盘错误
- Service crashes (7031/7034) / 服务异常崩溃
- Driver load failures (PnP 219) / 驱动加载失败
- Login failures (Security 4625) / 登录失败统计

## 🔧 Troubleshooting / 故障排除

| Issue / 问题 | Cause / 原因 | Solution / 解决方案 |
|--------------|--------------|---------------------|
| "找不到SysInfoTool.exe" | Missing exe in skill directory / 技能目录中缺少exe文件 | Download from [Releases](https://github.com/GuerGuaZhang/SysInfoTool/releases) and place in skill directory |
| "权限不足" | Insufficient permissions / 普通用户权限无法读取某些信息 | Run DSH as administrator or execute commands manually |
| "杀软拦截" | Antivirus false positive / 杀毒软件误报 | Add skill directory to antivirus whitelist |
| "采集超时" | Slow system response / 系统响应缓慢 | Wait and retry, or use --skip-scan to skip folder scanning |
| "部分信息为空" | Permission issues / 权限不足或系统限制 | Run as administrator or accept partial information |

## 📁 Project Structure / 项目结构

```
dsh-sysinfo-report/
├── .gitignore          # Git ignore configuration
├── package.json        # Package metadata
├── README.md           # This file
└── SKILL.md            # DSH skill definition
```

## ⚙️ Configuration / 配置

### Command Line Parameters / 命令行参数

```powershell
# Basic usage / 基本用法
SysInfoTool.exe --console --json-only

# No masking / 不脱敏
SysInfoTool.exe --console --json-only --no-mask

# Custom output directory / 自定义输出目录
SysInfoTool.exe --console --json-only --out=D:\Reports

# Skip folder scanning / 跳过文件夹扫描
SysInfoTool.exe --console --json-only --skip-scan

# Generate both HTML and JSON / 同时生成HTML和JSON
SysInfoTool.exe --console
```

### Output Structure / 输出结构

Reports are saved in the exe directory under `<ComputerName>/` subfolder:

报告保存在exe所在目录的`<电脑名>/`子文件夹下：

```
<输出目录>/<电脑名>/<电脑名>_日期时间.json
<输出目录>/<电脑名>/<电脑名>_日期时间.html
```

## 🤝 Related Projects / 相关项目

- [SysInfoTool](https://github.com/GuerGuaZhang/SysInfoTool) - Core collection tool / 核心采集工具
- [DSH](https://github.com/deepseek-ai/dsh) - DeepSeek Harness / DeepSeek 工具链

## 📄 License / 许可

MIT