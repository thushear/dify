# app-service

核心业务服务，负责应用的创建、配置和对话流程管理。主要职责包括：

- 维护应用元数据和配置
- 提供对话、任务等业务接口
- 与 workflow-service 协同处理异步任务
- 调用 model-service 进行模型推理
