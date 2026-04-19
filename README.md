# Engine Refacting

LLM 驱动的文字冒险引擎，采用“规则结算 + 世界状态演化 + 叙事合并”的分层架构，并提供 Streamlit 调试界面，便于回合级观察、回滚和一致性排查。

## 主要能力

- 自然语言输入与元命令输入统一路由
- 世界真值与叙事真值分离存储
- 状态补丁、回滚与一致性校验
- NPC 调度、执行与后处理链路
- Streamlit 调试 UI，用于查看回合、追踪和日志

## 目录说明

- `src/`：核心引擎、规则系统、数据模型与工具代码
- `world/`：世界数据、运行时 SQLite 与日志输出
- `config/`：配置文件与配置 schema
- `docs/spec/`：保留用于对外发布的规范与开发手册
- `tests/`：分阶段测试与验证脚本

## 运行方式

1. 准备 Python 环境并安装依赖。
2. 配置 `config/config.yaml` 中的模型地址、密钥和运行参数。
3. 启动命令行模式或 Streamlit 调试界面：

```powershell
python main.py
streamlit run streamlit_app.py
```

## 配置说明

默认配置位于 `config/config.yaml`，核心字段包括：

- `llm`：模型、API 地址、温度、超时与密钥
- `system`：重试、降级和快照间隔
- `agent`：DM、NPC 与叙事相关的记忆参数
- `storage`：世界与叙事 SQLite 路径

## 文档范围

仓库中仅保留 `docs/spec/` 作为公开文档内容。

## 许可证

当前仓库未包含许可证文件，如需开源发布，建议在首次公开前补充合适的许可证。