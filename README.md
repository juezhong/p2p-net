# p2p-net

安全 P2P 虚拟网络（TUN / 游戏）

> **状态：规划阶段。** 当前尚无可用的 Rust 实现，也无已完成的 CLI/TUI/GUI。请从 [AGENTS.md](AGENTS.md) → [docs/WORKFLOW.md](docs/WORKFLOW.md) → [docs/STATUS.md](docs/STATUS.md) 开始。

## 产品目标

先实现 L3 TUN 的两节点私有 IP 互通，优先评估 SDK QUIC DATAGRAM；再以指标决定其他加密 UDP 后端及多人组网。

使用 Rust + Tokio，共享 [p2p-sdk](https://github.com/juezhong/p2p-sdk) 的 ICE、NAT/IPv4/IPv6、身份认证、Quinn/QUIC、诊断能力。所有业务数据直连、端到端加密，不经信令服务器中继。发行版必须提供 **CLI、TUI、GUI**，三种界面共享同一业务 core。

完整开发说明见 [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md)。
