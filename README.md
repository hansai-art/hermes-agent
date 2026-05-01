<p align="center">
  <img src="assets/banner.png" alt="Hermes Agent" width="100%">
</p>

# Hermes Agent ☤

<p align="center">
  <a href="https://hermes-agent.nousresearch.com/docs/"><img src="https://img.shields.io/badge/文件-hermes--agent.nousresearch.com-FFD700?style=for-the-badge" alt="說明文件"></a>
  <a href="https://discord.gg/NousResearch"><img src="https://img.shields.io/badge/Discord-5865F2?style=for-the-badge&logo=discord&logoColor=white" alt="Discord"></a>
  <a href="https://github.com/NousResearch/hermes-agent/blob/main/LICENSE"><img src="https://img.shields.io/badge/授權-MIT-green?style=for-the-badge" alt="授權協議: MIT"></a>
  <a href="https://nousresearch.com"><img src="https://img.shields.io/badge/開發團隊-Nous%20Research-blueviolet?style=for-the-badge" alt="由 Nous Research 開發"></a>
</p>

**由 [Nous Research](https://nousresearch.com) 開發的自我進化 AI 代理。** 這是目前唯一內建學習迴圈的代理程式：它能從經驗中創造技能、在使用過程中改進技能、提醒自己持久化知識、搜尋過去的對話紀錄，並在不同會話間建立對你的深度理解模型。你可以將它運行在 $5 的 VPS、GPU 集群，或幾乎不產生閒置成本的無伺服器架構上。它不侷限於你的筆記型電腦：當它在雲端虛擬機工作時，你可以透過 Telegram 與它交談。

支援任何模型：[Nous Portal](https://portal.nousresearch.com), [OpenRouter](https://openrouter.ai) (支援 200+ 模型), [NVIDIA NIM](https://build.nvidia.com) (Nemotron), [Xiaomi MiMo](https://platform.xiaomimimo.com), [z.ai/GLM](https://z.ai), [Kimi/Moonshot](https://platform.moonshot.ai), [MiniMax](https://www.minimax.io), [Hugging Face](https://huggingface.co), OpenAI 或你自己的端點。使用 `hermes model` 即可切換，無需更改代碼，拒絕供應商綁定。

<table>
<tr><td><b>真實的終端介面</b></td><td>完整的 TUI 支援多行編輯、斜線指令自動補全、對話歷史、中斷與重定向，以及工具輸出的串流顯示。</td></tr>
<tr><td><b>無處不在</b></td><td>透過單一網關進程支援 Telegram, Discord, Slack, WhatsApp, Signal 和 CLI。支援語音備忘錄轉錄與跨平台對話連續性。</td></tr>
<tr><td><b>閉環學習</b></td><td>代理策劃的記憶與定期提醒。複雜任務後自動創建技能，技能在使用中自我改進。支援 FTS5 會話搜尋與 LLM 總結，實現跨會話召回。整合 <a href="https://github.com/plastic-labs/honcho">Honcho</a> 辯證式用戶建模。兼容 <a href="https://agentskills.io">agentskills.io</a> 開放標準。</td></tr>
<tr><td><b>定時自動化</b></td><td>內建 cron 排程器，可將結果發送至任何平台。支援以自然語言執行的每日報告、夜間備份與每週審計，完全自動化運行。</td></tr>
<tr><td><b>委派與並行</b></td><td>生成隔離的子代理進行並行工作。編寫 Python 腳本透過 RPC 調用工具，將多步流程壓縮為零上下文成本的輪次。</td></tr>
<tr><td><b>跨平台運行</b></td><td>支援六種終端後端：local, Docker, SSH, Daytona, Singularity 和 Modal。Daytona 與 Modal 提供無伺服器持久化：代理環境在閒置時休眠，隨時隨地按需喚醒，最大程度節省成本。支援 $5 VPS 或 GPU 集群。</td></tr>
<tr><td><b>研究就緒</b></td><td>批量軌跡生成、Atropos RL 環境、用於訓練下一代工具調用模型的軌跡壓縮。</td></tr>
</table>

---

## 快速安裝

```bash
curl -fsSL https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.sh | bash
```

支援 Linux, macOS, WSL2 以及 Android (透過 Termux)。安裝程式會自動為您處理平台相關設置。

> **Android / Termux:** 已驗證的手動安裝路徑請參考 [Termux 指南](https://hermes-agent.nousresearch.com/docs/getting-started/termux)。在 Termux 上，Hermes 會安裝精簡的 `.[termux]` 額外組件，因為完整的 `.[all]` 目前包含與 Android 不相容的語音依賴。
>
> **Windows:** 目前不支援原生 Windows 環境。請安裝 [WSL2](https://learn.microsoft.com/en-us/windows/wsl/install) 並執行上述指令。

安裝後：

```bash
source ~/.bashrc    # 重新載入 shell (或: source ~/.zshrc)
hermes              # 開始對話！
```

---

## 入門指令

```bash
hermes              # 互動式 CLI：啟動對話
hermes model        # 選擇 LLM 供應商與模型
hermes tools        # 配置啟用的工具
hermes config set   # 設置個別配置值
hermes gateway      # 啟動訊息網關 (Telegram, Discord 等)
hermes setup        # 執行完整設置嚮導 (一次配置所有內容)
hermes claw migrate # 從 OpenClaw 遷移 (如果您先前使用 OpenClaw)
hermes update       # 更新至最新版本
hermes doctor       # 診斷任何問題
```

📖 **[完整文件 →](https://hermes-agent.nousresearch.com/docs/)**

## CLI 與訊息平台快速參考

Hermes 有兩個入口：使用 `hermes` 啟動終端 UI，或運行網關透過 Telegram, Discord, Slack, WhatsApp, Signal 或 Email 與其交談。一旦進入對話，許多斜線指令在兩種介面上皆通用。

| 動作 | CLI | 訊息平台 |
|---------|-----|---------------------|
| 開始對話 | `hermes` | 執行 `hermes gateway setup` + `hermes gateway start` 後發送訊息 |
| 開啟新對話 | `/new` 或 `/reset` | `/new` 或 `/reset` |
| 切換模型 | `/model [供應商:模型]` | `/model [供應商:模型]` |
| 設置人格 | `/personality [名稱]` | `/personality [名稱]` |
| 重試或撤銷 | `/retry`, `/undo` | `/retry`, `/undo` |
| 壓縮上下文 / 檢查用量 | `/compress`, `/usage`, `/insights [--days N]` | `/compress`, `/usage`, `/insights [天數]` |
| 瀏覽技能 | `/skills` 或 `/<技能名稱>` | `/<技能名稱>` |
| 中斷當前工作 | `Ctrl+C` 或發送新訊息 | `/stop` 或發送新訊息 |
| 平台特定狀態 | `/platforms` | `/status`, `/sethome` |

如需完整指令清單，請參閱 [CLI 指南](https://hermes-agent.nousresearch.com/docs/user-guide/cli) 與 [訊息網關指南](https://hermes-agent.nousresearch.com/docs/user-guide/messaging)。

---

## 說明文件

所有說明文件均位於 **[hermes-agent.nousresearch.com/docs](https://hermes-agent.nousresearch.com/docs/)**：

| 章節 | 內容涵蓋 |
|---------|---------------|
| [快速入門](https://hermes-agent.nousresearch.com/docs/getting-started/quickstart) | 2 分鐘內完成安裝 → 設置 → 首次對話 |
| [CLI 用法](https://hermes-agent.nousresearch.com/docs/user-guide/cli) | 指令、快捷鍵、人格設置、會話管理 |
| [配置說明](https://hermes-agent.nousresearch.com/docs/user-guide/configuration) | 配置檔案、供應商、模型及所有選項 |
| [訊息網關](https://hermes-agent.nousresearch.com/docs/user-guide/messaging) | Telegram, Discord, Slack, WhatsApp, Signal, Home Assistant |
| [安全性](https://hermes-agent.nousresearch.com/docs/user-guide/security) | 指令審核、DM 配對、容器隔離 |
| [工具與工具集](https://hermes-agent.nousresearch.com/docs/user-guide/features/tools) | 40+ 工具、工具集系統、終端後端 |
| [技能系統](https://hermes-agent.nousresearch.com/docs/user-guide/features/skills) | 程序化記憶、技能中心、自定義技能 |
| [記憶功能](https://hermes-agent.nousresearch.com/docs/user-guide/features/memory) | 持久化記憶、用戶設定檔、最佳實踐 |
| [MCP 整合](https://hermes-agent.nousresearch.com/docs/user-guide/features/mcp) | 連接任何 MCP 伺服器以擴展能力 |
| [Cron 排程](https://hermes-agent.nousresearch.com/docs/user-guide/features/cron) | 定時任務與平台推送 |
| [內容文件](https://hermes-agent.nousresearch.com/docs/user-guide/features/context-files) | 塑造每場對話的專案背景資訊 |
| [架構設計](https://hermes-agent.nousresearch.com/docs/developer-guide/architecture) | 專案結構、代理迴圈、核心類別 |
| [貢獻指南](https://hermes-agent.nousresearch.com/docs/developer-guide/contributing) | 開發環境設置、PR 流程、代碼風格 |
| [CLI 參考](https://hermes-agent.nousresearch.com/docs/reference/cli-commands) | 所有指令與參數詳解 |
| [環境變數](https://hermes-agent.nousresearch.com/docs/reference/environment-variables) | 完整的環境變數參考表 |

---

## 從 OpenClaw 遷移

如果您先前使用 OpenClaw，Hermes 可以自動導入您的設置、記憶、技能與 API 金鑰。

**首次設置時：** 設置嚮導 (`hermes setup`) 會自動檢測 `~/.openclaw` 並在配置開始前詢問是否遷移。

**安裝後的任何時間：**

```bash
hermes claw migrate              # 互動式遷移 (完整預設)
hermes claw migrate --dry-run    # 預覽遷移內容
hermes claw migrate --preset user-data   # 僅遷移用戶數據 (不含金鑰)
hermes claw migrate --overwrite  # 強制覆蓋現有衝突
```

導入內容包括：
- **SOUL.md** — 人格定義檔案
- **Memories** — MEMORY.md 與 USER.md 條目
- **Skills** — 用戶創建的技能 → `~/.hermes/skills/openclaw-imports/`
- **Command allowlist** — 指令核准清單
- **Messaging settings** — 平台配置、允許用戶、工作目錄
- **API keys** — 允許的金鑰 (Telegram, OpenRouter, OpenAI, Anthropic, ElevenLabs)
- **TTS assets** — 工作區音訊檔案
- **Workspace instructions** — AGENTS.md (配合 `--workspace-target`)

詳情請參閱 `hermes claw migrate --help`，或使用 `openclaw-migration` 技能由代理引導您進行帶有預覽的互動式遷移。

---

## 貢獻指南

我們歡迎任何形式的貢獻！請參閱 [貢獻指南](https://hermes-agent.nousresearch.com/docs/developer-guide/contributing) 了解開發環境設置、代碼風格及 PR 流程。

開發者快速入門：使用 `setup-hermes.sh` 一鍵完成：

```bash
git clone https://github.com/NousResearch/hermes-agent.git
cd hermes-agent
./setup-hermes.sh     # 安裝 uv、建立 venv、安裝 .[all]、建立軟連結至 ~/.local/bin/hermes
./hermes              # 自動檢測 venv，無需手動執行 source
```

手動路徑 (等同於上述操作)：

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
uv venv venv --python 3.11
source venv/bin/activate
uv pip install -e ".[all,dev]"
scripts/run_tests.sh
```

> **RL 訓練 (選配)：** RL/Atropos 整合 (`environments/`) 透過 `.[all,dev]` 引入的 `atroposlib` 與 `tinker` 依賴提供，無需額外設置子模組。

---

## 社群連結

- 💬 [Discord](https://discord.gg/NousResearch)
- 📚 [Skills Hub](https://agentskills.io)
- 🐛 [問題回報](https://github.com/NousResearch/hermes-agent/issues)
- 🔌 [HermesClaw](https://github.com/AaronWong1999/hermesclaw) — 社群微信橋接：在同一個微信帳號上同時運行 Hermes Agent 與 OpenClaw。

---

## 授權協議

MIT — 詳見 [LICENSE](LICENSE)。

由 [Nous Research](https://nousresearch.com) 開發。
