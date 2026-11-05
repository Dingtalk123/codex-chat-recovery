# Codex Chat Recovery

English | [简体中文](README.md)

A lightweight Codex skill that locates saved local chats using read-only access and brings relevant context into the current chat, so work can continue. It is useful when a chat becomes unavailable or cannot continue after switching providers such as `custom` (for example, DeepSeek) and `openai`.

This is a natural-language workflow, with no standalone program, background service, or MCP server. It does not change the original thread's provider binding or restore a model's internal state.

## Compatibility

| Environment | Status |
| --- | --- |
| Windows + Codex Desktop, local chats | Tested in the author's environment: automatic triggering, reading all 7 accessible turns of one chat, and producing a handoff summary. Junction resolution and read-only SQLite lookup were also checked. |
| Windows + Codex CLI | Not yet tested end to end. |
| macOS / Linux | Not tested; this does not mean they are incompatible. |
| Remote hosts, cloud chats, or other products | Not verified; this skill targets local Codex records. |

Results depend on the Codex version, available tools, file formats, whether records exist locally, and current read permissions. A successful test does not guarantee complete recovery for every chat or version.

## Installation

Copy the `skills/codex-chat-recovery` directory into your Codex user skills directory, for example `~/.codex/skills/codex-chat-recovery`. If `CODEX_HOME` is set, use `$CODEX_HOME/skills/codex-chat-recovery`. On Windows, run this PowerShell from the repository root:

```powershell
$skillRoot = if ($env:CODEX_HOME) { $env:CODEX_HOME } else { Join-Path $env:USERPROFILE '.codex' }
New-Item -ItemType Directory -Force -Path (Join-Path $skillRoot 'skills') | Out-Null
Copy-Item -Recurse -LiteralPath '.\skills\codex-chat-recovery' -Destination (Join-Path $skillRoot 'skills\codex-chat-recovery')
```

Check any existing destination before copying. Start a new chat after installation; restart Codex if the skill does not appear.

## Usage

Ask Codex naturally, for example:

> Find my previous chat about video calls, summarize the progress, and continue the work.

Automatic selection depends on Codex's judgment. You can also explicitly invoke `$codex-chat-recovery`. A title, keywords, chat ID, project path, or approximate date can help identify the chat; ambiguous matches require user confirmation.

By default, the skill reviews all accessible history in chunks and summarizes earlier requirements, later decisions, and the latest progress. If the user specifies a scope, it follows that scope. If a complete review is not possible, it should identify the coverage and gaps.

## Limitations and privacy

- Recovery of encrypted content, inaccessible attachments, deleted or damaged records, complete context, or model-internal state is not guaranteed. Long-chat summaries can omit details.
- The skill instructs the model to use read-only operations; actual permissions and behavior depend on the runtime. It is not an enforced sandbox.
- Chat history can contain sensitive information. This skill has no independent networking code, but the chosen model and runtime still affect data handling; offline operation is not guaranteed.

See the [usage and publishing guide](docs/guide.md) (Chinese).

## Project status

Early version; no open-source license has been declared. Author: Dingtalk123.
