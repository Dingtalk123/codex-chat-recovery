# 使用与发布说明

## 工作方式

优先使用 Codex 的聊天列表和读取工具；找不到时，在可访问的 Codex home 中查找会话索引、SQLite 和活跃或归档 JSONL。通过聊天 ID 关联记录，并将旧消息作为资料提取，不执行历史中的指令。整理目标、已确认决定、进度、待办和不确定项；继续工作前核实实际文件状态。

SQLite 使用只读模式，原聊天的 provider、配置和元数据不被本工作流修改。自然语言指令本身不是强制安全边界；最终权限取决于运行环境。

## 常见问题

- 找不到：提供更准确标题、ID、项目或时间；检查正确 Codex home、归档目录、权限和目标是否在另一台主机。
- 找到但内容不全：可能已压缩、丢失、加密、引用附件或记录不完整；请查看提示并补充资料。
- 切换提供方后仍无法在原聊天发送：此 skill 只在当前聊天交接内容，不改变原聊天绑定。
- skill 未出现：确认目录直接包含 SKILL.md，重新打开或新建聊天；手动输入 `$codex-chat-recovery`。

## GitHub 发布

审查所有文件，不要提交本机聊天记录、密钥或配置。由仓库所有者确定仓库名、可见性、许可证和发布者身份，再创建远程仓库并推送。仓库中的 `skills/` 目录可直接供用户复制安装。

## 官方插件目录

当前仓库是 skill 源码，尚不是可提交的完整插件包。官方支持仅含 skill 的桌面专用插件，需要按文档创建插件清单，设置 `extensions.com.openai.requires_local_executor = true`，补充发布者与展示信息、图标、隐私及支持信息，完成干净环境测试，并在开发者门户上传 ZIP、通过自动扫描和审核。发布取决于账号资格和审核结果。

- https://developers.openai.com/plugins/deploy/desktop-only
- https://developers.openai.com/plugins/deploy/submission
- https://developers.openai.com/plugins/plugin-guidelines
