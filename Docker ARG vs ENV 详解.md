# Docker ARG vs ENV 详解

> Next.js 项目中 `NEXT_PUBLIC_*` 环境变量的正确用法

## 核心区别

| 特性 | ARG | ENV |
|------|-----|-----|
| **作用时机** | 构建时（`docker build`） | 运行时（`docker run`） |
| **可见性** | 只在 Dockerfile 内部可见 | 容器运行时可访问 |
| **持久化** | 不会保存到镜像中 | 会保存到镜像中 |

---

## ⚠️ 常见错误

### 错误：只使用 env_file

```yaml
# ❌ 这样不行！
services:
  b2b-admin:
    env_file:
      - .env.local  # 只在运行时生效，构建时用不了
```

**后果：** 前端代码中 `NEXT_PUBLIC_*` 变量为空，导致：

```
Failed to construct 'URL': Invalid URL
```

**原因：** `env_file` 只在容器**运行时**生效，无法影响**构建过程**

---

## ✅ 正确做法

### Docker Compose 配置

```yaml
# Docker Compose
b2b-admin:
  build:
    args:
      - NEXT_PUBLIC_API_URL=http://localhost:9012  # 构建时参数
```

### Dockerfile 配置

```dockerfile
# Dockerfile
ARG NEXT_PUBLIC_API_URL      # 1. 接收构建时的参数
ENV NEXT_PUBLIC_API_URL=$NEXT_PUBLIC_API_URL  # 2. 转成环境变量
```

### 流程解析

```
构建时（docker build）
    │
    ├── Docker Compose 通过 build.args 传递参数
    ├── Dockerfile 用 ARG 接收这个值
    └── Next.js 在构建时读取 ENV，硬编码到 JS 代码中
    │
运行时（docker run）
    │
    └── 变量已被打包进代码，运行时修改不生效
```

---

## 为什么不直接用 ENV？

### ❌ 错误做法

```dockerfile
ENV NEXT_PUBLIC_API_URL=http://localhost:9012  # 硬编码，不灵活
```

**问题：** 值写死了，不同环境要改 Dockerfile

### ✅ 正确做法

```dockerfile
ARG NEXT_PUBLIC_API_URL        # 从外部传入
ENV NEXT_PUBLIC_API_URL=$NEXT_PUBLIC_API_URL  # 转成 ENV
```

**好处：** 不同环境可以传不同的值

| 环境 | 参数值 |
|------|--------|
| 本地测试 | `NEXT_PUBLIC_API_URL=http://localhost:9012` |
| 生产环境 | `NEXT_PUBLIC_API_URL=https://api.example.com` |

---

## 简化理解

```
构建时（ARG）────→ 设置 ENV ───→ Next.js 读取并写入 JS 代码
      ↑                              ↓
 Docker Compose 传入            运行时无法修改
```

---

## 💡 核心要点

1. **`NEXT_PUBLIC_*` 变量必须在构建时注入**
   - Next.js 在构建时将这些变量打包到 JavaScript 代码中
   - 不是运行时配置，是构建时配置！

2. **env_file 无法影响构建过程**
   - `env_file` 只在容器运行时生效
   - 构建时完全读不到这些变量

3. **必须使用 ARG + ENV 组合**
   - Docker Compose: 使用 `build.args` 传递
   - Dockerfile: 用 `ARG` 接收，再用 `ENV` 设置

---

## 🔧 完整配置示例

### docker-compose.yml

```yaml
services:
  b2b-admin:
    build:
      context: .
      dockerfile: Dockerfile
      args:
        - NEXT_PUBLIC_API_URL=${NEXT_PUBLIC_API_URL}
    env_file:
      - .env.local  # 运行时环境变量（非 NEXT_PUBLIC_* 的可以放这里）
```

### Dockerfile

```dockerfile
# 构建时参数
ARG NEXT_PUBLIC_API_URL
ENV NEXT_PUBLIC_API_URL=$NEXT_PUBLIC_API_URL

# 构建
RUN npm run build
```

---

#Docker #Next.js #DevOps #环境变量 #踩坑记录
