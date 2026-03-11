```json
{
  "meta": {
    // 元数据：记录配置文件的版本和最后修改时间
    "lastTouchedVersion": "2026.3.8",
    "lastTouchedAt": "2026-03-11T15:29:33.831Z"
  },
  "wizard": {
    // 向导数据：记录了上次运行配置向导的时间和命令
    "lastRunAt": "2026-03-10T12:45:39.125Z",
    "lastRunVersion": "2026.3.8",
    "lastRunCommand": "onboard",
    "lastRunMode": "local"
  },
  "auth": {
    // 认证配置：定义了使用的认证方式
    "profiles": {
      "zai:default": {
        "provider": "zai", // 使用 Z.ai (硅基流动) 作为模型提供商
        "mode": "api_key"  // 认证模式为 API Key
      }
    }
  },
  "models": {
    // 模型配置：定义了可用的模型列表
    "mode": "merge",
    "providers": {
      "zai": {
        "baseUrl": "https://api.z.ai/api/paas/v4",
        "api": "openai-completions",
        "models": [
          // 这里列出了 Z.ai 支持的 GLM 系列模型
          // 注意：此处定义了模型，但下面的 defaults 里引用了一个不存在的 glm-4.5，可能会报错
        ]
      }
    }
  },
  "agents": {
    // 智能体配置：定义了 AI 大脑的默认设置
    "defaults": {
      "model": {
        // ❌ 错误点：这里引用了 glm-4.5，但上面 models 列表里只有 glm-5, glm-4.7 等，没有 glm-4.5
        "primary": "zai/glm-4.5"
      },
      "models": {
        "zai/glm-5": {
          "alias": "GLM"
        },
        "zai/glm-4.5": {}
        // 如果 glm-4.5 不存在，这里会导致找不到模型
      },
      "workspace": "C:\\Users\\boer\\.openclaw\\workspace",
      "compaction": {
        "mode": "safeguard"
      },
      "maxConcurrent": 4
    }
  },
  "tools": {
    // 工具配置：定义了默认的工具集
    "profile": "coding"
  },
  "bindings": [
    // 绑定配置：将渠道账号绑定到智能体
    {
      "agentId": "main", // 绑定到名为 "main" 的智能体
      "match": {
        "channel": "feishu", // 渠道为 飞书
        "accountId": "default" // 账号为 default
      }
    }
  ],
  "channels": {
    // 渠道配置：定义了各个通讯渠道的设置
    "feishu": {
      "enabled": true,
      "connectionMode": "websocket", // 使用 WebSocket 连接
      "domain": "feishu",
      "accounts": {
        "default": {
          "enabled": true,
          // ✅ 正确的位置：App ID 和 Secret 应该在这里
          "appId": "cli_a927a83881b85bc2",
          "appSecret": "cli_a927a83881b85bc2",
          "dmPolicy": "open", // 私聊策略：开放
          "groupPolicy": "open", // 群聊策略：开放
          "allowFrom": ["*"],
          "groupAllowFrom": ["*"]
        }
      },
      // ❌ 错误点：下面这两行是多余的，而且会覆盖上面的配置，导致出错
      // appId 和 appSecret 不应该出现在 accounts 外面这一层
      "appId": "cli_a925bfc385f89bd7",
      "appSecret": "i79LJAUPYmSOo9Z7bKyf4dLAf6wfxchv",
      "groupPolicy": "open"
    }
  },
  "gateway": {
    // 网关配置：OpenClaw 本地服务的端口和认证
    "port": 18789,
    "mode": "local",
    "bind": "loopback",
    "auth": {
      "mode": "token",
      "token": "493453c4751b7eb1d4e9b9d1d971d732da105652d031a911"
    }
  }
}

```