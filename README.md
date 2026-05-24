# Claude Code Telegram Bot - Deploy

自动部署 [claude-code-telegram](https://github.com/RichardAtCT/claude-code-telegram) 到 Debian 服务器的 GitHub Actions 配置。

## 项目结构

```
├── .env                 # Bot 配置模板（无敏感信息，安全提交）
└── .github/workflows/
    └── deploy.yml       # 自动部署工作流
```

## 部署原理

推送代码到 `main` → GitHub Actions SSH 到服务器 → 安装依赖 → 注入 Secrets → 重启服务。

7 个阶段全部幂等，首次部署和后续更新走同一流程。

## 需要配置的 GitHub Secrets

Settings → Secrets and variables → Actions → Repository secrets：

```
SSH_HOST                服务器 IP
SSH_USER                root
SSH_PRIVATE_KEY         SSH 私钥
TELEGRAM_BOT_TOKEN      Bot Token
TELEGRAM_BOT_USERNAME   Bot 用户名
TELEGRAM_ALLOWED_USERS  允许的用户 ID
ANTHROPIC_AUTH_TOKEN    DeepSeek API Key
MISTRAL_API_KEY         空值（预留）
```

## 配置修改

直接编辑 `.env` 提交即可，下次部署自动生效。机密值通过 GitHub Secrets 注入，不要写入 `.env`。
