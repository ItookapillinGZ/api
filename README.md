Self-Operating Integrator | 基于隔离沙盒的自主式 API 集成 Agent
针对 AI Agent 在本地多任务并行开发时易引发的“依赖冲突、环境污染、异构系统崩溃”等痛点，本项目实现了一套具备物理隔离、数据强校验与环境自愈能力的自主式 API 集成智能体框架。

Agent 能够根据用户的非结构化自然语言指令，在隔离的沙盒中独立完成“依赖盘点 -> 契约建模 -> 代码编写 -> 异常捕获 -> 环境自愈 -> 联调交付”的全生命周期闭环。

🌟 核心亮点
1. 任务级物理隔离沙盒 (Task & Worktree Isolation)
利用 Git Worktree 机制为每个集成任务动态构建物理隔离的 Sandbox 环境。

安全性：实现“阅后即焚”式生产，有效防止 Agent 在并行处理多个复杂集成任务（如 auth-refactor, weather-service）时的依赖踩踏与代码污染。

隔离性：每个任务拥有独立的临时工作目录，确保宿主机环境的纯净。

2. 强类型“契约式”数据校验 (Strict Schema Modeling)
摒弃传统的非结构化 JSON 读写，强制 Agent 使用 Pydantic v2 对第三方异构 API 进行严谨的 Schema 建模。

故障前移：利用 model_validate 机制在数据注入业务逻辑前进行强校验，确保 Agent 输入的 100% 确定性，从根源上杜绝脏数据导致的下游崩溃。

3. 环境自愈循环 (Self-Healing Workflow)
针对跨平台运行时频发的编码冲突（如 Windows 宿主机下的 GBK/UTF-8 冲突）引入“物理环境感知能力”。

自主重构：Agent 能够捕获运行时 Traceback，在下一轮迭代中自主重构代码（如动态注入编码声明、重配置 I/O 流并清洗冲突字符），实现 0 人工干预 的跨平台闭环自愈。

4. 智能化编排与多源补偿
设计了清晰的动态编排逻辑（顺序执行、条件分支与并行分发），并引入多源数据补偿机制。当单一数据源失效或触发 Rate Limiting 时，Agent 能自主切换检索策略并生成格式化的 Markdown 综合研判报告。

🛠️ 技术栈
Language: Python 3.11+

Validation: Pydantic v2

Version Control: Git (Worktree mechanism)

API Interaction: Requests, RESTful API Design

Environment: Dotenv, Python-standard CLI tools

📋 工作流程
任务拆解：接收自然语言指令，识别所需集成的 API 终端。

沙盒构建：通过 Git Worktree 动态创建隔离的工作路径。

契约建模：定义 Pydantic 模型，确立数据交互契约。

循环迭代：在沙盒中执行测试，通过错误日志触发 Self-Healing 逻辑。

交付报告：完成联调后，提交格式化的 Markdown 文档并清理沙盒。

Author: 黄家乐 (中山大学数学学院)
Project Status: 核心框架已完成，支持多源 API 自主集成。
