<img src="Source/title.png" alt="alt" width="20%">

# LYCHEE: 自动化运维与智能监控利器 🚀

**LYCHEE (荔枝)** 是一款集成了 **CI/CD 部署**、**系统监控** 和 **预警通知** 功能的工具。它旨在简化您的运维流程，确保系统服务的健康运行，并在出现问题时及时发送通知。告别繁琐，拥抱高效！✨

-----

## 核心功能 💡

  * **Systemd 服务监控：** 对 `systemctl` 服务进行基础且有效的监控，确保它们正常运行。👁️‍🗨️
  * **飞书集成通知：** 将警报和通知无缝发送到您的飞书（Lark）群组。📨
  * **日志异常检测（基础）：** 监控服务日志中的特定关键词，帮助您及早发现潜在问题（目前为基础实现，尚待全面测试）。🔍
  * **服务健康检查：** 主动检查指定服务是否正常运行，并记录和过滤相关日志以供分析。❤️‍🩹

-----

## 规划中的功能 (TODO) 🗓️

我们正在持续努力扩展 LYCHEE 的功能。未来的开发计划包括：

1.  **Web 界面：** 提供一个用户友好的网页界面，以便更轻松地进行配置和监控。🌐
2.  **容器管理：** 支持监控和管理容器化应用程序。🐳
3.  **多账号日志发送：** 增强日志发送功能，支持将日志发送到多个账号或目的地。📧

-----

## 安装 🛠️

在 **Ubuntu 发行版**上安装 LYCHEE 非常简单。

只需使用 `sudo` 运行安装脚本即可：

```bash
sudo ./install.sh
```

-----

## 从源码构建 🏗️

### 构建要求

  * **Go 1.24.4** 或更高版本

您也可以使用 **Nix Flake** 来构建，以获得可复现的构建环境。

要构建可执行文件，请运行：

```bash
go build -o lychee ./cmd/app/main.go
```

-----

## 使用方法 🚀

构建或安装完成后，您可以通过指定配置文件来运行 LYCHEE：

```bash
./lychee -config configs/config.yaml
```

-----

## 配置文件示例 ⚙️

以下是一个 `config.yaml` 示例，帮助您快速上手：

```yaml
# config.yaml

# LYCHEE 检查服务状态和日志的频率（秒）。⏱️
checkInterval: 60

# 飞书（Lark）机器人 Webhook URL，用于发送通知。🔔
lark:
  WebhookURLs:
    - "https://open.feishu.cn/open-apis/bot/v2/hook/URLA"
    - "https://open.feishu.cn/open-apis/bot/v2/hook/URLB"

# --- Systemd 服务监控 ---
# 要监控的 systemd 服务列表。LYCHEE 会检查它们是否处于 'active' 状态。✅
systemd:
  services:
    - "daed.service"
    - "sshd.service"
    - "nginx.service"

# --- Journald 日志监控 ---
# 配置特定服务和关键词的日志监控。
# 如果在服务的 Journal 日志中发现任何指定关键词，LYCHEE 将发出警报。🚨
journal:
  - serviceName: "nginx.service"
    keywords:
      - "error"
      - "failed"
      - "denied"
  - serviceName: "sshd.service"
    keywords:
      - "Failed password"
      - "Invalid user"
```