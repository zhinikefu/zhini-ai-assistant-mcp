# 知你AI助手 MCP｜让 AI 查询多平台客户资料、研判会话并触达客户

> 将知你客服中的多平台客户资料、当前与历史会话及聊天记录连接到 Codex、Claude Code、WorkBuddy 等 AI 工具，通过自然语言完成客户查询、会话研判和业务分析；支持用户明确确认后批量打开选定对话、发送文本或图片消息。

[知你AI助手官网](https://ai.zhinikefu.com/?f=github) · [知你客服官网](https://zhinikefu.com/?f=github) · MCP 服务地址：`https://mcp.h5bqb.top/mcp`

## 产品介绍

知你AI助手是一项面向 AI 工具的多平台客户沟通数据连接服务。它通过 Streamable HTTP MCP，将已接入知你客服的客户资料、标签、负责人、当前会话、历史会话和聊天记录连接到 AI 工具。

团队可以直接用自然语言查找客户、了解沟通前情、检索退款或投诉记录、筛选目标客户、发现购买意向，并基于完整消息上下文整理业务结论；需要触达客户时，AI 在用户明确确认后批量打开选定对话、异步发送文本或图片消息并跟踪发送进度。查询范围由当前凭据权限决定，结果可以继续追溯到相关客户、会话和原始消息。

服务支持两种认证方式：**MCP 原生 OAuth 2.1**（浏览器授权，无需 API Key，含动态客户端注册与 PKCE，授权可随时在官网吊销）或 **静态 Bearer API Key**。

## 支持的平台渠道

**个微/企微/视频号/微信小程序/公众号/服务号/微信客服/微信小店/抖音号/小红书/微博/网站及H5客服等平台渠道。**

## 核心能力

1. **多平台客户数据统一查询**：查询已接入知你客服的个微、企微、视频号、微信小程序、公众号、服务号、微信客服、微信小店、抖音号、小红书、微博、网站及 H5 客服等平台渠道数据。
2. **当前客服会话分诊**：查看个微、企微、微信客服、微信小程序、公众号、服务号、网站及 H5 客服等渠道的待接待、我的会话、同事会话和 AI 会话。
3. **客户资料与沟通前情查询**：按姓名、手机号、微信号、渠道、客服、负责人、标签或时间，查找来自个微、企微、视频号、抖音号、小红书、微博等渠道的客户。
4. **客户画像信息整理**：查询微信小店、微信小程序、公众号、服务号及其他已接入渠道客户的资料、标签、来源渠道、负责人和联系信息。
5. **历史会话与聊天记录检索**：检索微信客服、个微、企微、抖音号、小红书、微博、网站及 H5 客服等渠道的历史会话。
6. **消息关键词与时间查询**：按退款、投诉、报价、试用、购买等消息关键词和发生时间，定位视频号、微信小店、抖音号、小红书等渠道的相关客户会话。
7. **完整消息上下文读取**：将 AI 整理结果追溯到对应平台渠道、客户、会话和原始消息。
8. **渠道与业务字典查询**：查询平台账号、渠道、客服和标签字典。
9. **API Key 用量查询**：查询当前 API Key 的总额度、已使用量和剩余额度。
10. **客户触达与消息发送**：在用户明确确认后，批量打开选定客户对话（每次最多 20 个），创建最多 100 个 UID、最多 2 条文本/图片消息的异步群发任务，并跟踪发送进度、查询和管理历史任务。

## MCP 工具

| 工具 | 用途 |
| --- | --- |
| `zhini_get_current_kefu` | 查询当前调用者对应的客服身份 |
| `zhini_list_active_sessions` | 查询当前客服会话队列 |
| `zhini_get_customer_profile` | 查询客户资料与标签 |
| `zhini_list_tag_groups` | 查询标签分组 |
| `zhini_list_tags` | 分页查询标签 |
| `zhini_search_tags` | 按关键词搜索标签 |
| `zhini_fetch_messages` | 读取客户或会话的消息上下文 |
| `zhini_list_kefu` | 查询客服列表 |
| `zhini_list_channels` | 查询平台渠道列表 |
| `zhini_search_customers` | 按业务条件搜索客户 |
| `zhini_search_sessions` | 按业务条件搜索历史会话 |
| `zhini_get_apikey_usage` | 查询 API Key 用量 |
| `zhini_open_sessions` | 将用户明确选定的对话批量打开到"我的对话"（≤20/次） |
| `zhini_upload_image_for_message_sending` | 上传消息发送图片并返回 CDN 地址（≤10 MiB） |
| `zhini_create_message_sending_task` | 两阶段创建批量消息发送任务（≤100 UID、≤2 条消息） |
| `zhini_get_message_sending_task_status` | 查询发送任务进度与逐客户明细 |
| `zhini_list_message_sending_tasks` | 分页查询历史群发任务 |
| `zhini_delete_message_sending_task` | 逻辑删除群发任务并取消未发送明细 |

## 使用方法

### 1. 连接 MCP（两种认证方式二选一）

**方式一：OAuth 2.1 浏览器授权（推荐）**——不配置任何静态认证字段，客户端首次访问时按服务端 OAuth 挑战打开浏览器完成知你账号授权：

```json
{
  "mcpServers": {
    "zhini": {
      "type": "http",
      "url": "https://mcp.h5bqb.top/mcp"
    }
  }
}
```

**方式二：静态 API Key**——访问[知你AI助手官网](https://ai.zhinikefu.com/?f=github)，注册或登录后创建 API Key：

```json
{
  "mcpServers": {
    "zhini": {
      "type": "http",
      "url": "https://mcp.h5bqb.top/mcp",
      "headers": {
        "Authorization": "Bearer ${ZHINI_API_KEY}"
      }
    }
  }
}
```

环境变量：

```text
ZHINI_API_KEY=YOUR_API_KEY
```

### 2. 用自然语言查询与触达

- 现在有哪些客户正在等待接待？
- 查一下这个客户最近聊了什么，还有哪些事情待确认？
- 找出近 7 天提到退款的历史会话。
- 哪些客户最近提过报价、试用或购买？
- 把这些已选客户的对话打开到我的对话。
- 向已确认的客户批量发送跟进文本或图片，发完告诉我进度。
- 整理最近登录异常反馈的共同问题。

## 适用团队

- 客服团队：会话分诊、回复前情查询、投诉与问题复盘、批量跟进触达
- 销售团队：客户背景查询、意向识别、跟进线索整理、确认后批量发送跟进消息
- 客户运营：标签筛选、客户分群、跨渠道客户洞察
- 质检与产品：历史问题检索、共性问题归纳、需求线索发现

## 连接信息

| 项目 | 信息 |
| --- | --- |
| 产品 | 知你AI助手 / Zhini AI Assistant |
| 官网 | <https://ai.zhinikefu.com/?f=github> |
| MCP 地址 | `https://mcp.h5bqb.top/mcp` |
| 传输方式 | Streamable HTTP |
| 鉴权方式 | OAuth 2.1 浏览器授权 或 Bearer API Key |
| API Key 环境变量 | `ZHINI_API_KEY` |
| MCP 标识 | `com.zhinikefu/zhini-mcp-service` |
| npm 包 | `@zhinikefu/zhini-mcp-service` |

## 数据与权限说明

- 查询能力保持只读；批量打开对话与消息发送为受控触达操作，仅在用户明确确认后执行，且不修改客户资料、不修改标签、不接待/转接/关闭会话。
- 消息群发是异步任务组合：先上传图片（如有），再创建发送任务，并通过状态、列表和删除接口管理任务；单任务最多 100 个 UID、最多 2 条消息，删除任务不可逆，已发送的消息不会撤回。
- 查询结果受当前凭据对应的数据权限约束；OAuth 授权可随时在官网吊销。
- API Key 应保存在客户端环境变量或安全配置中。
- “微信”“抖音”“小红书”“微博”等名称用于说明已接入的数据来源渠道，不代表相关平台对本产品的官方背书。

## 关键词

多平台客户数据 MCP、客户资料查询 MCP、客服会话查询 MCP、历史会话分析、客户画像、客户分群、投诉会话分析、销售线索识别、消息群发、客户触达、批量发送、多平台客服、omnichannel customer data、customer conversation search、customer profile lookup、customer segmentation、message sending。
