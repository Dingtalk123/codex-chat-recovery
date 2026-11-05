# Codex Chat Recovery

[English](README.en.md) | 简体中文

一个轻量的 Codex skill，以只读方式查找已保存的本地聊天，并将相关上下文带入当前聊天，方便继续工作。适用于切换 `custom`（如 DeepSeek）和 `openai` 等提供方后，原聊天不可继续或无法在列表中找到的情况。

它是一份自然语言工作流程，不包含独立程序、后台服务或 MCP 服务器。它不会改变原聊天的提供方绑定，也不能恢复模型内部状态。

## 兼容性

| 环境 | 状态 |
| --- | --- |
| Windows + Codex Desktop，本地聊天 | 已在作者的环境中测试：自动触发、读取一条聊天的全部 7 轮可访问对话并生成交接摘要；也检查了目录联接和 SQLite 只读查询。 |
| Windows + Codex CLI | 尚未进行完整测试。 |
| macOS / Linux | 尚未测试；不代表一定不兼容。 |
| 远程主机、云端聊天或其他产品 | 尚未验证；本 skill 面向本地 Codex 记录。 |

实际效果取决于 Codex 版本、可用工具、文件格式、目标记录是否保存在本机，以及当前文件读取权限。一次测试通过不代表所有版本和聊天都能完整恢复。

## 安装

将 `skills/codex-chat-recovery` 目录复制到 Codex 用户技能目录，例如 `~/.codex/skills/codex-chat-recovery`。设置了 `CODEX_HOME` 时使用 `$CODEX_HOME/skills/codex-chat-recovery`。在仓库根目录运行 Windows PowerShell：

```powershell
$skillRoot = if ($env:CODEX_HOME) { $env:CODEX_HOME } else { Join-Path $env:USERPROFILE '.codex' }
New-Item -ItemType Directory -Force -Path (Join-Path $skillRoot 'skills') | Out-Null
Copy-Item -Recurse -LiteralPath '.\skills\codex-chat-recovery' -Destination (Join-Path $skillRoot 'skills\codex-chat-recovery')
```

如果目标目录已存在，请先检查现有内容。安装后新建聊天；若技能未出现，可重启 Codex。

## 使用

安装后可以新建聊天测试：输入“找到某个聊天标题，接着这个聊天工作”。如果没有自动触发，可以输入：

```text
使用 $codex-chat-recovery 找到“聊天标题”，整理目标、已完成内容和待办，然后接着做。
```


直接告诉 Codex 要找的聊天，例如：

> 找到我之前关于腾讯云通话的聊天，整理进度并接着做。

自动触发取决于 Codex 的判断；也可明确指定 `$codex-chat-recovery`。提供标题、关键词、聊天 ID、项目路径或大致时间有助于定位；多个结果无法区分时需要用户确认。

默认分段检查目标聊天的全部可访问历史，整理早期要求、后续决定和最新进度；用户指定范围时按其要求处理。无法读全时应说明已读范围和缺口。

## 限制与隐私

- 不能保证恢复加密内容、不可访问的附件、已删除或损坏的记录、完整上下文或模型内部状态；长对话摘要可能遗漏细节。
- skill 指导模型进行只读操作，权限和实际行为由运行环境决定；它不是强制沙箱。
- 历史聊天可能包含敏感内容。此 skill 没有独立网络代码，但所选模型和运行环境仍会影响数据如何处理，不能保证离线。

详见 [使用与发布说明](docs/guide.md)。

## 项目状态

初版，尚未声明开源许可证。作者：Dingtalk123。
