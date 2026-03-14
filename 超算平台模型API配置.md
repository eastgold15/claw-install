# 超算平台(SCNet)模型API配置

> 2026-03-13 配置完成

## API 信息

- **Base URL**: `https://api.scnet.cn/api/llm/v1`
- **兼容**: OpenAI 接口规范
- **API Key 管理**: 模型API-API Keys 页面创建

## 已配置模型

| 模型 | 别名 | 输入价格 | 输出价格 | 上下文长度 |
|------|------|----------|----------|------------|
| DeepSeek-V3.2 | DeepSeek | ¥0.5/M tokens | ¥0.75/M tokens | 128K |
| DeepSeek-R1-0528 | DeepSeek R1 | ¥1/M tokens | ¥4/M tokens | 128K |
| Qwen3-235B-A22B | Qwen3 | ¥0.5/M tokens | ¥2/M tokens | 32K |
| MiniMax-M2.5 | MiniMax | ¥0.5/M tokens | ¥2/M tokens | 128K |

## 平台完整模型列表

### 大语言模型

| 模型 | 上下文 | 输入价格 | 输出价格 |
|------|--------|----------|----------|
| Qwen3-235B-A22B-Thinking-2507 | 32K | ¥0.5/M | ¥5/M |
| MiniMax-M2.5 | 128K | ¥0.5/M | ¥2/M |
| MiniMax-M2 | 128K | ¥0.5/M | ¥2/M |
| DeepSeek-V3.2 | 128K | ¥0.5/M | ¥0.75/M |
| Qwen3-30B-A3B-Instruct-2507 | 256K | ¥0.5/M | ¥0.5/M |
| DeepSeek-R1-0528 | 128K | ¥1/M | ¥4/M |
| Qwen3-235B-A22B | 32K | ¥0.5/M | ¥2/M |
| Qwen3-30B-A3B | 128K | ¥1/M | ¥6/M |
| QwQ-32B | 32K | ¥1/M | ¥4/M |
| DeepSeek-R1-Distill-Llama-70B | 32K | ¥0.1/M | ¥6/M |
| DeepSeek-R1-Distill-Qwen-32B | 32K | ¥1/M | ¥4/M |
| DeepSeek-R1-Distill-Qwen-7B | 32K | ¥0.1/M | ¥0.1/M |

## 使用方式

OpenClaw 中切换模型：
```
/model DeepSeek      # 切换到 DeepSeek-V3.2
/model DeepSeek R1   # 切换到 DeepSeek-R1-0528
/model Qwen3         # 切换到 Qwen3-235B
/model MiniMax       # 切换到 MiniMax-M2.5
```

---
#API #超算 #SCNet #模型配置
