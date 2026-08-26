# dsh-sysinfo-report

[DSH](https://github.com/deepseek-ai/dsh) 技能插件：采集电脑硬件/系统/软件/网络信息，生成 JSON 供 AI 分析。

## 功能

- 采集 26 个模块的系统信息（CPU/内存/磁盘/显卡/系统/软件/网络等）
- 生成结构化 JSON 数据，AI 可直接读取分析
- 支持脱敏模式（隐藏序列号/MAC/IP/用户名）
- 支持按电脑名分目录存储
- 事件日志全面加强（蓝屏/意外关机/WHEA/磁盘错误/服务崩溃等 12 类排查信息）

## 安装

```bash
# 方式 1：通过 DSH 安装
dsh plugin --profile <你的profile名> add dsh-sysinfo-report

# 方式 2：本地安装
dsh plugin --profile <你的profile名> add /path/to/dsh-sysinfo-report
```

## 前置条件

- [SysInfoTool.exe](https://github.com/GuerGuaZhang/SysInfoTool) 需要在系统 PATH 中或当前工作目录
- Windows 10 1809+ / Windows 11
- .NET Framework 4.8（系统自带）

## 使用

安装后，在对话中说以下内容即可触发：

- "生成电脑信息报告"
- "看看这台电脑的配置"
- "排查一下系统问题"
- "导出硬件信息"

AI 会自动调用 `SysInfoTool.exe --console --json-only` 生成 JSON 报告。

## 采集内容

| 分类 | 模块 |
|------|------|
| 硬件 | CPU、主板/BIOS/TPM、内存、硬盘、显卡、显示器、网卡、声卡、电池、USB |
| 系统 | 版本/Build/激活、更新历史、UEFI/安全启动、页面文件、还原点 |
| 软件 | 已安装程序、启动项、服务、计划任务、驱动、浏览器、运行时 |
| 痕迹 | 用户目录、最近文件、回收站、WiFi、打印机、蓝牙、共享文件夹 |
| 性能与日志 | Uptime、内存快照、Top 进程、事件日志（12 类排查信息） |
| 网络 | IP/网关/DNS/MAC、代理、监听端口 |

## 事件日志（面向错误排查）

- 系统/应用/安装日志 Critical/Error/Warning 统计
- 蓝屏记录（BugCheck 1001）
- 意外关机/重启（Kernel-Power 41）
- WHEA 硬件错误
- 磁盘错误（Event 7/11/15/51/55）
- 服务异常崩溃（7031/7034）
- 驱动加载失败（PnP 219）
- 登录失败统计（Security 4625）

## 相关项目

- [SysInfoTool](https://github.com/GuerGuaZhang/SysInfoTool) - 核心采集工具

## License

MIT
