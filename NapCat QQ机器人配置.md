# 🤖 NapCat QQ机器人配置

## 📋 基础配置信息

### WebSocket 服务器配置
- **监听地址**: `0.0.0.0`
- **端口**: `15150`
- **访问令牌**: `openclaw-qq-token-2026`
- **消息格式**: `array`

### 配置文件结构
```json
{
  "network": {
    "httpServers": [],
    "httpClients": [],
    "websocketServers": [
      {
        "name": "OpenClawWS",
        "enable": true,
        "host": "0.0.0.0",
        "port": 15150,
        "messagePostFormat": "array",
        "reportSelfMessage": false,
        "token": "openclaw-qq-token-2026",
        "enableForcePushEvent": true,
        "debug": false,
        "heartInterval": 30000
      }
    ],
    "websocketClients": []
  }
}
```

## 🔗 连接信息

### WebSocket 连接地址
```
ws://localhost:15150?access_token=openclaw-qq-token-2026
```

### 认证信息
- **Token**: `openclaw-qq-token-2026`
- **连接类型**: WebSocket 服务端（正向WS）
- **认证方式**: URL 参数 access_token

### ✅ 验证的连接信息
- **QQ 号**: 3568645809
- **在线状态**: 在线
- **运行状态**: 正常

## 📡 消息格式

### 消息上报格式（array）
```json
{
  "type": "message",
  "message_type": "private",
  "message_id": 123456,
  "user_id": 123456789,
  "message": [
    {
      "type": "text",
      "data": {
        "text": "Hello World"
      }
    }
  ]
}
```

### 事件格式
```json
{
  "type": "event",
  "event_type": "friend_add",
  "user_id": 123456789,
  "timestamp": 1642680000
}
```

## 🔧 API 操作

### 发送消息
```json
{
  "action": "send_msg",
  "params": {
    "message_type": "private",
    "user_id": 123456789,
    "message": "Hello from OpenClaw"
  }
}
```

### 获取好友列表
```json
{
  "action": "get_friend_list"
}
```

### 获取群列表
```json
{
  "action": "get_group_list"
}
```

## 💻 开发示例

### Python 连接示例
```python
import asyncio
import websockets
import json

async def napcat_client():
    uri = "ws://localhost:15150"
    async with websockets.connect(uri) as websocket:
        # 认证
        auth_message = {
            "action": "authenticate",
            "token": "openclaw-qq-token-2026"
        }
        await websocket.send(json.dumps(auth_message))
        
        # 接收消息
        async for message in websocket:
            data = json.loads(message)
            print(f"收到消息: {data}")

# 运行客户端
asyncio.get_event_loop().run_until_complete(napcat_client())
```

### JavaScript 连接示例
```javascript
const ws = new WebSocket('ws://localhost:15150');

ws.onopen = () => {
    // 认证
    ws.send(JSON.stringify({
        action: 'authenticate',
        token: 'openclaw-qq-token-2026'
    }));
};

ws.onmessage = (event) => {
    const data = JSON.parse(event.data);
    console.log('收到消息:', data);
};

// 发送消息示例
function sendMessage(userId, message) {
    ws.send(JSON.stringify({
        action: 'send_msg',
        params: {
            message_type: 'private',
            user_id: userId,
            message: message
        }
    }));
}
```

## 🔍 开发应用指南

### 1. 基础应用开发
- **消息机器人**: 接收并回复消息
- **自动回复**: 根据关键词自动回复
- **消息转发**: 将消息转发到其他平台

### 2. 高级应用开发
- **群管理**: 自动管理群聊
- **数据分析**: 分析聊天数据
- **智能回复**: 结合 AI 的智能回复

### 3. 集成开发
- **与 OpenClaw 集成**: 让 AI 处理 QQ 消息
- **与 Web 服务集成**: 通过 HTTP API 扩展功能
- **与数据库集成**: 存储聊天记录

## 🚨 注意事项

1. **Token 安全**: 不要泄露访问令牌
2. **端口占用**: 确保 15150 端口未被占用
3. **网络防火墙**: 确保端口开放
4. **消息频率**: 避免频繁发送消息导致封号

## 🔗 相关链接

- [[📚 OpenClaw 知识库索引]] - 知识库主页
- [NapCat 官方文档](https://napneko.github.io/config/basic)
- [OneBot 协议文档](https://github.com/botuniverse/onebot-11)

---

*配置文档最后更新: 2026-03-12*