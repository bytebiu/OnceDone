# OnceDone

OnceDone 是一款 macOS 本地效率工具，用一个轻量入口连接常用桌面操作，减少在多个工具和窗口之间来回切换。

## 下载

前往 [Releases](https://github.com/bytebiu/OnceDone/releases) 下载最新版本。

当前预览版提供：

- `OnceDone-v0.1.1.dmg`：可拖拽安装的 macOS 安装包
- `OnceDone-v0.1.1.sha256`：安装包 SHA-256 校验文件

## 主要能力

- 统一入口：通过主面板快速搜索和启动常用操作。
- 截图与录屏：面向日常桌面采集、保存和复制流程。
- 翻译：提供本地优先的翻译入口。
- 剪贴板：管理常用复制内容，减少重复查找。
- 权限提示：在需要屏幕录制、辅助功能等 macOS 权限时给出明确提示。

## 安装

1. 在 [Releases](https://github.com/bytebiu/OnceDone/releases) 下载 `.dmg`。
2. 打开 `.dmg`，将 `OnceDone.app` 拖入 `Applications`。
3. 从 `Applications` 打开 OnceDone，不要直接在 `.dmg` 或下载目录中运行。

## 未签名版本打开方式

当前预览版未使用 Apple Developer ID 签名，也未经过 Apple 公证。macOS 首次打开时可能提示无法验证开发者或拦截打开。

如果遇到拦截，请先确认安装包来自本仓库 Release，然后在“系统设置 > 隐私与安全性”中点击允许打开。也可以在终端执行下面的命令移除隔离标记后再打开：

```bash
xattr -dr com.apple.quarantine /Applications/OnceDone.app
```

这个命令表示手动信任当前安装到 `/Applications` 的预览版 App。只建议在确认下载来源可信时使用。

## 权限问题处理

OnceDone 的截图、录屏、自动粘贴、按键监听、音频和摄像头能力会按需请求 macOS 权限。授权后请完全退出并重新打开 OnceDone，让系统权限状态重新生效。

如果系统设置中已经显示 OnceDone，但 App 仍提示未授权，可以先退出 OnceDone，然后在普通终端中执行下面的命令重置授权记录。不要使用 `sudo` 执行这些命令，否则可能重置到错误的用户权限库。

```bash
tccutil reset ScreenCapture me.oncedone.app
tccutil reset Accessibility me.oncedone.app
tccutil reset ListenEvent me.oncedone.app
tccutil reset Microphone me.oncedone.app
tccutil reset Camera me.oncedone.app
```

执行后重新打开 OnceDone，并按 App 内提示重新授权。常见对应关系如下：

- 屏幕录制或截图无法使用：重置 `ScreenCapture`，再到“系统设置 > 隐私与安全性 > 屏幕录制”重新允许 OnceDone。
- 自动粘贴或辅助操作无效：重置 `Accessibility`，再到“辅助功能”重新允许 OnceDone。
- 快捷键或按键监听无效：重置 `ListenEvent`，再到“输入监听”重新允许 OnceDone。
- 麦克风或摄像头授权短暂生效后失效：重置 `Microphone` 或 `Camera`，重新授权后退出并重开 OnceDone。
- 权限列表里出现多个 OnceDone：删除旧记录或执行上面的重置命令，然后只保留 `/Applications/OnceDone.app` 这一份安装位置。

## 系统要求

- macOS 15 或更高版本

## 隐私

OnceDone 以本地使用为主。截图、录屏、剪贴板内容和翻译文本默认不上传到云端。涉及第三方网络翻译时，应以应用内设置和提示为准。
