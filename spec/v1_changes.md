# Changes

Compared to the original spec, I've divided the changes into three levels.

- **Refine:** without changing the mechanism, only defining the behavior, defining the boundaries of the behavior, or rename.
- **Breaking**: the mechanism has been **minor** adjusted, **but the core mechanism: AnyTLS Padding Scheme v0  remains unchanged.**
- **Breaking Breaking**: the mechanism has been **significantly** adjusted, **but the core mechanism: AnyTLS Padding Scheme v0 remains unchanged.**

## Refine Changes

- **Use** a modern package format description method (from RFC 9000)
- **Define** the K-V serialization rules for the Data section: **AnyTLS Data Block K-V Serialization V0**
- **Define** the text encoding rules for the Data section: **AnyTLS Data Block TEXT Serialization V0**
- 定义了 ANYTLS 最高抽象行为： TLS Connection Upgrade to ANYTLS Connection ，类似于 http upgrade websocket
- 定义抽象层次

```
Session → ANYTLS Connection
Stream → Stream
command → frame
```

- **Mandate** that ANYTLS Connection and Stream **MUST** have a timeout mechanism.
- **Define** the classification of frames (formerly *commands*) into two categories based on `stream_id`:
    - `stream_id = 0`: connection-scoped frames
    - `stream_id > 0`: stream-scoped frames
- **Mandate** that authentication frames (AUTH frames) **MUST** be transmitted only after the TLS handshake has completed.
- **Explicitly prohibit** sending authentication frames (AUTH frames) within **TLS 1.3 0-RTT handshake phase**.
- The original **mandatory** constraints on client-side connection handling have been reclassified as **discretionary** implementation guidelines.
- Provide a new proxy implementation guideline: **Guidelines for Proxy Implementation A**, and retaining the original proxy implementation guideline: **Guidelines for Proxy Implementation B**
- **Formalize** the original padding scheme: **AnyTLS Padding Scheme V0**
    - Absolutely compatible with the original code implementation of padding behavior
    - Define the syntax of the DSL used by the original padding scheme
    - Corrected the incorrect description in the original spec
    - Define an abstract model and state machine for padding
    - The behavior of padding schemes is described in detail, and practical suggestions are provided.
    - Describe the behavior of padding scheme in detail, and provide an implementation guideline
- Define 如何从 TLS Connection 升级成 ANYTLS Connection
- 定义了 **ANYTLS Connection Client State Machine** and **ANYTLS Connection  Server State Machine**
- Define 了 Stream 的管理
- Define Stream **Client State Machine** 和 **Stream Server State Machine**
