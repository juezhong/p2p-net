# p2p-net 开发工作流

1. 读 `AGENTS.md`、`docs/STATUS.md`、`docs/ARCHITECTURE.md`。
2. 检查 main HEAD、打开的 PR、GitHub Actions 失败日志；对未合并代码明确分支，不将 PR 里的实现误认为 main 已具备。
3. 查看 [p2p-sdk AGENTS.md](https://github.com/juezhong/p2p-sdk/blob/main/AGENTS.md) 和 [STATUS.md](https://github.com/juezhong/p2p-sdk/blob/main/docs/STATUS.md)，确定 SDK 实际提供的 API、尚未完成的能力。参考 SDK PR #2 与 Transfer PR #1 的历史决策，**不要自动合并这些设计记录 PR**。
4. 选择首个未完成任务，在功能分支增量开发并运行 `cargo fmt --all -- --check`、`cargo clippy --workspace --all-targets -- -D warnings`、`cargo test --workspace`；运行不了就注明未测试。
5. 按真实网络及系统平台验证，不把 localhost 当成 NAT 成功；记录脱敏日志。
6. 在中文 PR 中写出变更范围、测试、阻塞、下一项任务，同步更新 `docs/STATUS.md`。

## 复制到新会话的简短指令

> 读取 `juezhong/p2p-net` 的 AGENTS.md / docs/WORKFLOW.md / docs/STATUS.md，检查 main、未合并 PR 和 CI，再检查依赖的 p2p-sdk 实现状态。继续第一个未完成的 Rust 里程碑，用独立分支提交中文 PR 并维护状态文件。不要复制 SDK 穿透实现，也不要把未经测试的功能标记为完成。
