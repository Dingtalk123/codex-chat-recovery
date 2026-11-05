# Codex Chat Recovery

一个轻量的 Codex skill：以只读方式查找本地 Codex 聊天，把已保存的上下文带入当前聊天。适用于在 `deepseek这类custom供应商`和`openai` 官方提供方之间切换后，原聊天无法继续或无法在列表中找到和继续该聊天的情况。

它是自然语言工作流程，不含独立程序、后台服务或 MCP 服务器。它不会将原聊天切换到新提供方；恢复效果取决于本地记录、权限和 Codex 执行环境。

## 安装

将 `skills/codex-chat-recovery` 整个目录复制到你的 Codex 用户技能目录，例如 `~/.codex/skills/codex-chat-recovery`。如果设置了 `CODEX_HOME`，使用 `$CODEX_HOME/skills/codex-chat-recovery`。Windows 示例：

```powershell
$skillRoot = if ($env:CODEX_HOME) { $env:CODEX_HOME } else { Join-Path $env:USERPROFILE '.codex' }
New-Item -ItemType Directory -Force -Path (Join-Path $skillRoot 'skills') | Out-Null
Copy-Item -Recurse -LiteralPath '.\skills\codex-chat-recovery' -Destination (Join-Path $skillRoot 'skills\codex-chat-recovery')
```

在仓库根目录运行；如果目标已存在，先检查现有内容。新建 Codex 聊天后调用：

```text
使用 $codex-chat-recovery 找到“聊天标题”，整理目标、已完成内容和待办，然后接着做。
```

也可以提供聊天 ID、项目路径、关键词或大致时间。遇到多个候选项时，skill 会请求确认。

## 环境和限制

- 需要支持 Agent Skills 的 Codex 环境，以及对目标机器本地历史的读取权限。具体可用工具依安装、版本及权限而异。
- 主要面向本地 Codex Desktop/CLI 历史；目标聊天必须有可读取的本地索引或会话记录。远程主机、云端聊天或其他产品的记录不保证可用。
- Windows 上已对目录联接解析、SQLite 只读查询及一条 `custom` 聊天的文件定位做过检查；macOS、Linux、其他 Codex 版本和完整端到端调用尚未验证。
- 技能指导模型操作，模型仍须具备可用的文件读取和解析工具。SQLite 不可用时可尝试索引和 JSONL；格式可能随版本变化。
- 不保证恢复加密内容、不可访问的附件、已删除或损坏的记录、完整上下文或模型内部状态。长对话摘要可能遗漏内容。
- 旧聊天可能包含敏感信息。只读取用户指定的目标和必要内容；运行环境、权限和所用模型提供方仍决定数据如何处理。技能本身没有独立网络代码，但不能保证模型运行环境离线。

详见 [使用与发布说明](docs/guide.md)。

## 状态

这是初版。没有声明开源许可证；未经权利人授权，不应假定允许再分发或修改。发布前应由作者选择适用许可证。

作者：Dingtalk123

项目地址：https://github.com/Dingtalk123/codex-chat-recovery
