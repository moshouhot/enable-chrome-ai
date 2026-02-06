# Enable Chrome AI ✨

由 [lcandy2](https://twitter.com/vanillaCitron) 研究并制作脚本。

[![Twitter](https://img.shields.io/twitter/follow/vanillaCitron)](https://twitter.com/vanillaCitron)

[English](README.md) | 中文

在 Google Chrome 中启用 Gemini、AI 历史搜索、DevTools AI 等创新功能——无需清除数据或重新安装。

<img width="512" alt="Google Chrome Gemini in Chrome" src="https://github.com/user-attachments/assets/a88c56a7-f20b-432a-926c-0184194225b4" />

轻量 Python 脚本，通过修改本地 Chrome 配置自动启用浏览器内置 AI 功能，无需手动设置 flags。

## ✅ 环境要求
- Python `3.10+`（见 `.python-version` / `pyproject.toml`）
- 已安装 Google Chrome（Stable/Canary/Dev/Beta）

## ⚡️ 快速开始（uv）
1. 安装 uv（一次性）：
   - Windows: `powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"`
   - macOS & Linux: `curl -LsSf https://astral.sh/uv/install.sh | sh`
   - 更多安装方式请参考 [uv 安装文档](https://docs.astral.sh/uv/getting-started/installation/)。
2. 安装依赖（自动创建虚拟环境）：`uv sync`。
3. 运行脚本：`uv run main.py`。
4. 补丁过程中 Chrome 会被关闭；重启后根据提示按 Enter 结束。

## ⚡️ 快速开始（pip）
1. 创建并激活虚拟环境。
2. 安装依赖：`python -m pip install psutil`。
3. 运行：`python main.py`。

## 🔧 修改内容（共 5 处）

脚本会修改 Chrome `Local State` 文件中的以下 5 项设置：

| # | 设置项 | 修改 | 作用 |
|---|--------|------|------|
| 1 | `chrome://flags/#glic` | → 启用 | 启用 Gemini in Chrome 功能 |
| 2 | `chrome://flags/#glic-side-panel` | → 启用 | 启用 Gemini 侧边栏 |
| 3 | `is_glic_eligible` | → `true` | 标记用户有资格使用 AI 功能 |
| 4 | `variations_country` | → `"us"` | 绕过地区限制 |
| 5 | `variations_permanent_consistency_country[1]` | → `"us"` | 确保地区设置一致性 |

### 工作流程
- 自动定位 Windows / macOS / Linux 上的 Chrome Stable / Canary / Dev / Beta 用户数据目录。
- 关闭顶层 Chrome 进程以避免文件锁，再在补丁后恢复。
- 应用上述 5 项修改到 `Local State`。
- 重启补丁前已运行的 Chrome 版本。

## ⚠️ 已知限制 / 注意事项
- 脚本假设 `User Data/Local State` 已存在；若缺失可能直接失败（可先启动一次 Chrome 生成配置）。
- 只有在能从进程信息中取到可执行文件路径时，脚本才会自动重启 Chrome。
- macOS 上按进程名（`Google Chrome*`）识别，可能会终止不止"顶层"应用进程。
- Linux 上按可执行文件名 `chrome` 识别；若你的发行版/安装方式使用其他名字，可能不会关闭 Chrome（从而仍可能有文件锁）。

## 🛟 注意
- 脚本会修改现有 Chrome 配置，如需保险请先备份 `User Data`。
- 使用拥有该 Chrome 配置的同一系统用户运行，确保有写入权限。
- 与 Google 无关，风险自担。

## 📜 许可
转载或基于本研究二次创作需要注明来源。

## 🙏 致谢
- [show-copilot](https://github.com/hzkaai/show-copilot)
