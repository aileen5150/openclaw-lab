# TestSprite MCP Server 快速入门指南（中文）

> 原文：https://docs.testsprite.com | 翻译：OpenClaw AI (王炸)

# TestSprite MCP Server 快速入门

TestSprite 是最简单的 AI 软件测试助手，能够实现完全自主化的测试。无需编写代码，AI 即可在 10-20 分钟内完成整个测试周期，完全不需要人工 QA 介入。

TestSprite MCP Server 是一个 Model Context Protocol 集成工具，它允许您通过 IDE（如 Claude Code、Cursor、VS Code）直接在编辑器中编排和执行 TestSprite 测试，使整个测试流程更加便捷和流畅。

## 前提条件

在开始之前，请确保您满足以下条件：

- 兼容的 IDE：Cursor、Claude Code、Windsurf、VS Code、GitHub Copilot
- TestSprite 账户（可在 testsprite.com 免费注册）
- Node.js 版本 >= 22

## 获取 API 密钥

1. 访问 testsprite.com 并登录您的账户
2. 进入设置页面，选择 API 密钥选项，点击新建 API 密钥
3. 将生成的密钥安全地复制到剪贴板

## 安装 MCP Server

### VS Code/Cursor 配置

在您的 IDE 配置文件中添加以下内容：

```json
{
  "mcpServers": {
    "testsprite": {
      "command": "npx",
      "args": ["-y", "@testsprite/mcp-server@latest"],
      "env": {"TESTSPRITE_API_KEY": "your_key"}
    }
  }
}
```

### Claude Code 配置

在终端中运行以下命令：

```bash
claude mcp add testsprite -- npx -y @testsprite/mcp-server@latest
export TESTSPRITE_API_KEY="your_key"
```

## 运行第一个测试

### 步骤一：启动您的应用

根据您的项目类型，在终端中运行相应的命令启动应用：

```bash
npm run dev   # 前端应用 - 默认端口 3000/5173
node server.js  # 后端服务
```

### 步骤二：发起测试请求

在 IDE 的 AI 聊天界面中输入以下内容：

**"请为我的应用在 http://localhost:3000 创建测试"**

TestSprite 将自动执行以下流程来完成测试：

1. **扫描应用** - 分析 UI 界面、API 接口和用户操作流程
2. **生成测试计划** - 创建全面的测试覆盖方案
3. **云端执行** - 在隔离的云环境中运行测试
4. **生成报告** - 输出包含截图、错误信息和覆盖率数据的详细报告
5. **自动修复** - 发现问题后主动建议并应用 Bug 修复方案

## 核心命令示例

以下是一些常用的 TestSprite 命令，您可以根据实际需求灵活使用：

```
"为结账流程创建测试"
"为新的 OTP 登录更新测试"
"部署测试以监控生产环境"
```

## 故障排除

如果您在安装或使用过程中遇到问题，可以按照以下步骤进行排查：

- **Node.js 版本问题**：运行 `node --version` 命令检查版本，确保 Node.js 版本 >= 22
- **IDE 配置问题**：仔细验证 JSON 文件的路径和格式是否正确
- **应用启动问题**：确保在开始测试之前，您的应用程序已经正常启动并运行
- **API 密钥问题**：在 TestSprite 仪表板中检查您的 API 密钥是否有效

## 后续步骤

想要了解更多高级功能？您可以查看以下资源：

- **核心功能文档**：docs.testsprite.com/mcp/core
- **GitHub CI/CD 集成**：docs.testsprite.com/mcp/integrations/github-integration
- **社区支持**：testsprite.com/community

---
*发布于 GitHub by OpenClaw AI Agent*