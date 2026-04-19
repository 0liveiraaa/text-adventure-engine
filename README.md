# Engine Refacting

一个基于大语言模型的文字冒险引擎，采用“规则结算 + 世界状态演化 + 叙事合并”的分层架构。仓库同时提供命令行入口和 Streamlit 调试界面，适合做回合级调试、剧情验证和世界数据演示。

## 项目特性

- 自然语言输入与元命令输入统一处理
- 世界真值与叙事真值分离存储
- 状态补丁、回滚和一致性校验链路
- NPC 调度、执行和后处理流程
- Streamlit 调试面板，可查看回合、日志和运行状态

## 仓库内容

- `main.py`：命令行入口，适合直接游玩或做回合调试
- `streamlit_app.py`：Streamlit 调试界面
- `src/`：核心引擎、规则系统、数据模型和工具代码
- `config/`：默认配置、配置 schema 和表单定义
- `world/`：示例世界数据
- `docs/spec/`：对外公开的规范与开发手册

## 运行环境

建议使用 Python 3.10+。项目依赖至少包括 `streamlit`、`pydantic` 和 `PyYAML`；如果你的环境里没有这些包，请先安装后再运行。

## 快速开始

1. 安装依赖。
2. 按需修改 `config/config.yaml`，填入你的模型地址、API Key 和运行参数。
3. 选择命令行或 Streamlit 方式启动。

### 命令行启动

```powershell
python main.py
```

可选参数：

- `--world-dir`：指定世界目录，默认是 `world/world1`
- `--config`：指定配置文件，默认是 `config/config.yaml`
- `--actor-id`：覆盖默认玩家角色 ID
- `--show-debug`：每回合输出调试 payload

说明：命令行入口当前只支持真实 LLM；不要传 `--use-fake-llm`。

### Streamlit 启动

```powershell
streamlit run streamlit_app.py
```

Streamlit 侧边栏可切换世界、配置文件、模型名、真实 LLM 开关和调试显示。

## 配置说明

默认配置文件是 `config/config.yaml`。配置加载优先级为：命令行覆盖 > 环境变量 > 配置文件 > 默认值。

常见字段：

- `llm`：模型名、API Base、API Key、温度、超时和 token 上限
- `system`：重试、降级和快照间隔
- `agent`：DM、NPC 和叙事侧的记忆参数
- `storage`：世界真值和叙事真值 SQLite 路径
- `runtime`：回合 ID、trace ID 和流式输出节奏

环境变量支持 `ER_` 前缀，例如 `ER_LLM__MODEL`、`ER_SYSTEM__MAX_RETRY_COUNT`。

## 世界数据

`world/` 下提供了两个示例世界：`world1/` 和 `world2/`。每个世界目录通常包含：

- `world.json`：世界元信息
- `map/`：地图定义
- `charactor/`：角色定义
- `item/`：物品定义
- `end/`：结局规则

运行时生成的 SQLite 数据和日志会写到 `world/` 下的本地文件中，这些内容已加入忽略规则，不建议提交到仓库。

## 文档范围

仓库中仅保留 `docs/spec/` 作为公开文档内容，其他 `docs/` 子目录不作为对外发布内容。

## 开源前检查

- 确认 `config/config.yaml` 里没有真实密钥或私有地址
- 确认 `world/` 下没有未清理的运行时数据库和日志
- 确认本机路径、账号信息和临时调试内容没有残留在公开文档里

## 许可证

当前仓库未包含许可证文件。准备公开到 GitHub 前，建议补充一个明确的开源许可证。