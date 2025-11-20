# RealPostman MCP Server

一个基于 Disify API 的 Model Context Protocol (MCP) 服务器，提供邮箱格式、DNS、MX、垃圾邮件嫌疑与临时邮箱检测等三种工具：`check-email`、`check-email-batch`、`view-valid-emails`。可在 Cursor、Claude Desktop 等支持 MCP 的客户端中使用，也可通过脚本直接调用。
在AIIDE中添加mcp可以判断邮箱的有效情况，结合officemcp之类的功能可能会有不小的帮助 好的，以下全是claude自己生成的，我无法判断是否严谨；我会在readme的末尾给出我的建议，先看看最后的建议好吗[doge玫瑰] 验证和确认单个邮箱地址。检查邮箱地址是否为一次性使用、临时性、MX 记录无效、是否拼写错误、是否不活跃或不存在。
## 功能亮点

- ✅ **单个邮箱检测**：验证格式、域名、DNS、MX、垃圾邮件嫌疑以及是否临时邮箱。
- 📨 **批量校验**：一次最多 100 个邮箱，返回详细统计与 session ID。
- 📋 **结果追溯**：通过 session ID 再次拉取批量校验中的有效邮箱列表。
- 🧰 **脚本体验**：提供 `scripts/check-email.mjs` 便于在本地终端快速调用 MCP 工具。

## 环境要求

- Node.js 18+（需包含内置 `fetch`）
- npm 或其他兼容的包管理器
- 可访问 [Disify API](https://www.disify.com/)

## 安装与构建

```bash
git clone https://github.com/your-org/realpostman.git
cd realpostman
npm install
npm run build
```

构建后会生成 `build/index.js`，既可以直接运行，也可作为 MCP 服务器入口。

## 在 Cursor / Claude Desktop 中配置 MCP

在客户端的 `settings.json`（或设置界面）添加：

```json
{
  "mcpServers": {
    "realpostman": {
      "command": "node",
      "args": [
        "C:/path/to/realpostman/build/index.js"  “这块是index.js文件的完整地址，根据自己的改”
      ]
    }
  }
}
```

- `args` 中路径请替换为你的实际 `build/index.js` 绝对路径。
- 如需代理或 API Key，可在该配置下添加 `env` 字段传入环境变量。

保存配置后重启客户端（或重新加载 MCP），即可在工具栏中看到：

- `check-email`
- `check-email-batch`
- `view-valid-emails`

## 本地脚本调试

无需打开 MCP 客户端，也可以直接在终端调用：

```bash
npm run build
node scripts/check-email.mjs someone@example.com
```

脚本会在后台启动 `build/index.js` 并调用 `check-email` 工具，输出与 MCP 客户端一致的结果，方便调试。

## 项目结构

```
realpostman/
├─ src/index.ts            # MCP 服务器实现
├─ scripts/check-email.mjs # 本地调用示例脚本
├─ package.json
├─ tsconfig.json
└─ README.md
```

## 开发指南

1. 修改 `src/` 下的代码。
2. 运行 `npm run build` 生成新的 `build/index.js`。
3. （可选）执行 `node scripts/check-email.mjs <email>` 验证行为。


## 许可协议

本项目默认采用 MIT License；请在仓库根目录提供 `LICENSE` 文件或按需调整许可条款。

我的建议：下载项目到某个盘里头问问你的AIIDE的看法，他会帮你解决的。
