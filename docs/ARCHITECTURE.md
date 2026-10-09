# p2p-net 设计基线（待细化）

## 需求

- Rust 应用通过 SDK 已认证直连路径实现两端虚拟私有 IP 通信，优先采用三层 TUN 和 QUIC DATAGRAM。
- 首个阶段：Linux 上两个节点配置 TUN、子网/路由与 IP 包传输，可用 ping/TCP/UDP 实测；随后扩展 Windows/macOS。
- QUIC DATAGRAM 受路径 MTU、最大 Datagram 大小、拥塞控制与丢包影响；不承诺所有游戏优于专用加密 UDP。
- 接口权限、Linux CAP_NET_ADMIN、Windows/macOS 适配、路由清理、虚拟 IP 冲突、MTU/重连属于核心安全稳定性问题。
- **TUN 不自动实现以太网广播域。** 游戏 LAN 广播自动发现、TAP/L2、多人成员/mesh 或中心式房主转发需单独确定；初版不暗示全部游戏即插即用。
- SDK 统一提供 ICE/QUIC、加密身份与诊断，不在应用内重写穿透。三套入口 CLI/TUI/GUI 必须共享 `net-core`。

## 最小里程碑

- M0：Rust Workspace、TUN/路由抽象、配置与安全约束文档。
- M1：Linux TUN localhost/namespace IP 包收发模型，明确 MTU 和取消。
- M2：接入 SDK 安全 Datagram，两节点异网直连、UDP/TCP over TUN。
- M3：延迟抖动/CPU/丢包基准，评估 QUIC 与专用安全 UDP 后端；按证据决定。
- M4：Windows/macOS、多人和广播兼容性评审；CLI/TUI/GUI 与正式发布。

## 关键手测

双端虚拟 IP/ping、UDP 游戏实际联机、跨 MTU 大包、丢包恢复、路由不覆盖默认网关、关闭后无残留 TUN 与路由、防火墙拒绝时明确 NoDirectPath 且不允许 relay。
