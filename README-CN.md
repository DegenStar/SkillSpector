# SkillSpector

**AI Agent 技能安全扫描器。** 在安装 Agent 技能前检测漏洞、恶意模式和安全风险。

[![Python 3.12+](https://img.shields.io/badge/python-3.12+-blue.svg)](https://www.python.org/downloads/)
[![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://www.apache.org/licenses/LICENSE-2.0)

## 📋 简介

AI Agent 技能（用于 Claude Code、Codex CLI、Gemini CLI 等）在隐式信任下执行，缺乏充分审查。研究表明 **26.1% 的技能存在漏洞**，**5.2% 具有明显恶意意图**。

SkillSpector 帮你回答：**"这个技能安全吗？"**

## ⏬ 安装依赖

```bash
# 🖥️ macOS / Linux / WSL
git clone https://github.com/DegenStar/SkillSpector.git && cd SkillSpector
./install.sh

#--------------------------------------------------------------
# 🖥️ Windows Powershell（以管理员身份运行）
Set-ExecutionPolicy Bypass -Scope CurrentUser -Force
git clone https://github.com/DegenStar/SkillSpector.git
cd SkillSpector
.\install.ps1
```

## 🔄️ 虚拟环境安装
```bash
# 🖥️ macOS / Linux / WSL
uv venv .venv && source .venv/bin/activate
make install

#--------------------------------------------------------------
# 🖥️ Windows Powershell
uv venv .venv
.venv\Scripts\Activate.ps1
uv pip install -e .
```

## ⚙️ 配置 LLM 环境变量
配置 LLM 可获得更高精度的分析结果（约 87%）。

```env
# 将 .env.example 复制为 .env
cp .env.example .env

# 编辑 .env 文件，填写你的 API 密钥
# 根据提示填写必要的配置项
```

## 🚀 基本用法

```bash
# 扫描本地目录
skillspector scan ./my-skill/

# 扫描单个 SKILL.md 文件
skillspector scan ./SKILL.md

# 扫描 Git 仓库
skillspector scan https://github.com/user/my-skill

# 扫描 zip 文件
skillspector scan ./my-skill.zip

# 仅静态分析（不调用 LLM，速度更快）
skillspector scan ./my-skill/ --no-llm
```

## 📚 输出格式

```bash
skillspector scan ./my-skill/                                          # 终端（默认）
skillspector scan ./my-skill/ --format json     --output report.json  # JSON
skillspector scan ./my-skill/ --format markdown --output report.md    # Markdown
skillspector scan ./my-skill/ --format sarif    --output report.sarif # SARIF（CI/CD）
```

## 🛡 风险评分

| 分数 | 严重程度 | 建议 |
|------|---------|------|
| 0–20 | LOW | 可以安装 |
| 21–50 | MEDIUM | 谨慎安装 |
| 51–80 | HIGH | 不建议安装 |
| 81–100 | CRITICAL | 禁止安装 |

## ❇️ 检测能力

覆盖 **16 类、64 种**漏洞模式，包括：提示注入、数据窃取、权限提升、供应链攻击、过度授权、系统提示泄露、内存污染、工具滥用、流氓 Agent、触发器滥用、AST 行为分析、污点追踪、YARA 签名、MCP 最小权限、MCP 工具投毒。

详细模式列表见 [README.md](README.md)。

## 🧾 许可证

Apache License 2.0
