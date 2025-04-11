<div align="center">
  <h1>SubDroid</h1>
  <p>🌐 自动化子域名枚举与安全扫描工具 | 集成多工具联动的企业级资产测绘解决方案</p>
  <img src="https://img.shields.io/badge/License-MIT-green" alt="License">
  <img src="https://img.shields.io/badge/Python-3.8%2B-blue" alt="Python">
  <img src="https://img.shields.io/badge/OS-Linux%2FmacOS-brightgreen" alt="OS Support">
</div>

---

## 📖 目录
- [核心特性](#-核心特性)
- [设计理念](#-设计理念)
- [工具集成](#-工具集成)
- [快速开始](#-快速开始)
  - [环境要求](#环境要求)
  - [安装指南](#安装指南)
  - [基础用法](#基础用法)
- [进阶配置](#-进阶配置)
- [输出结构](#-输出结构)
- [性能优化](#-性能优化)
- [贡献指南](#-贡献指南)
- [免责声明](#-免责声明)
- [致谢](#-致谢)

---

## 🚀 核心特性
1. **全流程自动化扫描**  
   整合子域名发现、DNS解析、端口探测、指纹识别、Poc验证等模块，一键启动多维度资产测绘。
2. **智能结果聚合**  
   自动归类并保存扫描结果至标准化目录结构，报告内置AI api分析（可选）。
3. **灵活策略配置**  
   支持自定义线程数、超时阈值、扫描深度等参数，适配不同规模目标。
4. **跨工具协同**
   自研证书透明度，域传送漏洞检测  
   基于 `subfinder`、`masscan`、`Tidefinger` 等流行工具构建，优化执行顺序与数据传递逻辑。
6. **轻量级部署**  
   提供 `install.sh` 自动化初始化脚本，支持 Python 虚拟环境隔离依赖。

---

## 🎯 设计理念
SubDroid 旨在解决多工具手动串联以及信息收集中信息分拣的效率瓶颈，通过模块化设计实现以下目标：
- **降低使用门槛**：简化命令行参数，隐藏复杂工具交互细节。
- **提升扫描效率**：通过并行任务调度减少总体耗时（注：大规模扫描时建议调整并发参数避免资源过载）。
- **结果可追溯性**：标准化输出目录与日志记录，便于审计与二次分析。
- **理论支持强大**：拥有全套信息收集矩阵，提供强大理论支持
- **供应链信息收集**： （研发中，将作为新的工具独立开发并联动其中）
---

## 🛠️ 工具集成
| 模块             | 工具                           | 功能描述                    |
|------------------|--------------------------------|-----------------------------|
| 子域名枚举       | subfinder, shuffledns，subtake | 多源聚合子域名发现           |
| DNS解析          | dnsx,subtake(自研）            | 域名解析与存活验证           |
| 端口扫描         | masscan                        | 高速TCP/UDP端口探测          |
| 指纹识别         | TideFinger                     | Web服务指纹库匹配            |
| 漏洞扫描         | nuclei（集成中）               | 基于模板的CVE/漏洞检测       |
| 目录爆破         | ffuf（集成中）                 | 敏感路径与文件模糊测试       |

---

## ⚡ 快速开始

### 环境要求
- **操作系统**: Linux (Windows需配置WSL)
- **Python**: 3.8+ (推荐使用虚拟环境)
- **依赖工具**: 确保已安装 [subfinder](https://github.com/projectdiscovery/subfinder)、[masscan](https://github.com/robertdavidgraham/masscan) 等核心工具。
- **网络环境**： 需要设置桥接或者frp穿透以及端口转发（虚拟环境下）
### 安装指南
```bash
# 克隆仓库
git clone https://github.com/satoru-qwq/SubDroid.git
cd SubDroid

# 初始化环境 (自动安装依赖工具)
chmod +x install.sh
./install.sh

# 配置api
其中result.py报告生成需要ai的api Key
自研subtake需要配置zoomeye以及virustotal的api
subfinder shuffledns 需要配置各大平台的apikey
```

### 基础用法
```bash
# 基础扫描
./subdroid.sh example.com -silent
./subdroid.sh example.com 
```

---


## 📂 输出结构
```
F:\tmp\example\
|—— example_report.txt
├── ALIVE\
│   ├── alive.txt
│   └── wayback\
├── Finger\
├── IP\
│   ├── domain\
│   │   └── hackpax.top.txt
│   └── ip\
│       └── hackpax.top.txt
├── PORTS\
│   ├── masscan_results.txt
│   └── open_ports.txt
└── SUB\
    └── hackpax.top.txt
```

---

## ⚙️ 性能优化
- **资源限制**：通过 `--rate` 参数控制 masscan 扫描速率，避免触发目标防火墙。
- **分布式扫描**：拆分目标域至多台主机并行执行，合并结果时使用 `merge_results.py`。
- **缓存复用**：启用 `--use-cache` 跳过已扫描域名，减少重复请求。

---

## 🤝 贡献指南
欢迎通过以下方式参与项目：
1. **问题反馈**：提交 [GitHub Issue](https://github.com/Sat0ru-qwq/SubDroid/issues) 报告BUG或建议。
2. **文档改进**：优化使用说明或翻译多语言版本。

---

## ⚠️ 免责声明
SubDroid 仅限授权测试使用，禁止用于非法用途。使用者需自行承担因滥用工具导致的法律责任。

---

## 🙏 致谢
- 核心工具贡献者：Sat0ru,LinTu 等
- 指导专家：NightWatch Diffany



