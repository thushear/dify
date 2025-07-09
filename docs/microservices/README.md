# Dify 微服务拆分方案

本文档概述了将当前单体架构拆分为适用于企业级分布式部署的多个独立项目的建议。每个子项目都可以独立部署和扩展，通过统一的 API 网关进行访问。

## 总览

- **gateway-service**：提供统一的入口，处理鉴权、路由和限流等通用逻辑。
- **auth-service**：负责用户注册、登录、权限管理及 API Token 颁发。
- **app-service**：管理应用配置、对话流程以及相关的业务逻辑，是核心业务服务。
- **workflow-service**：处理异步任务、事件和流程编排，提供任务队列和调度能力。
- **dataset-service**：管理知识库和数据集，提供文档上传、分片和检索接口。
- **model-service**：与各类模型供应商交互，进行模型调用、配额统计及内容审核。
- **web-service**：前端项目，负责向最终用户呈现界面，可独立部署并调用其他服务的接口。

各服务通过消息队列或 gRPC/HTTP 进行通信，核心数据存储可根据需要拆分为独立的数据库实例。

## 目录结构示例

```
microservices/
├── gateway-service
├── auth-service
├── app-service
├── workflow-service
├── dataset-service
├── model-service
└── web-service
```

上述目录用于存放各服务的代码仓库链接或子模块，也可以作为单独项目的占位符。

## 部署建议

1. 统一 API Gateway 负责请求入口、流量控制及安全策略。
2. 服务之间采用轻量级通信协议（HTTP/gRPC），业务解耦后可按需独立扩容。
3. 公共组件（如数据库、缓存、消息队列）按服务拆分或共享，视业务量和隔离需求而定。
4. 建议使用容器化方式（Docker/Kubernetes）进行部署，实现弹性扩展和 CI/CD。

