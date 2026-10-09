# p2p-net：新会话 Agent 开发入口

**必读顺序：** `AGENTS.md` → `docs/WORKFLOW.md` → `docs/STATUS.md` → `docs/ARCHITECTURE.md`，随后查看 main、分支、未合并 PR 和 CI。

## 不可违反

- 所有新业务代码使用 **Rust**，Tokio；应用层 CLI/TUI/GUI **三种都必须交付**，业务逻辑共享一个 core。
- STUN/ICE/IPv6/IPv4/NAT/端口映射/Quinn/身份加密/诊断由 `juezhong/p2p-sdk` 统一实现，本仓库不得自行复制。
- **禁止**业务数据中继；不允许自动退回 TURN、HTTP 代理或服务器转发；连接无直连可用路径时明确报告失败。
- 手动配对和可选只交换元数据的信令服务器由 SDK 提供。
- 在独立 `feat/` 分支开发、通过测试后提交中文 PR；状态写入 `docs/STATUS.md`。
- 明确区分“文档规划”“有源码”“经过 CI/手工真实双机验证”，不虚报已完成功能。
- 不修改旧 Go `p2p-friend` 仓库；Go v0.16.4 仅为 Transfer 的只读参考。
- 跨仓库修改必须检查 SDK 当前真实代码、主分支与尚未合并的功能 PR。

## 新会话用法

用户只需说：“读取 `p2p-net` 仓库状态并继续开发”，Agent 就应当按上面的顺序自主寻找任务、核实 CI、按现有里程碑推进，而不是等待用户重复整个历史。
