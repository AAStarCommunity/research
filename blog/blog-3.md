# OpenClave TEE OS 架构与操作解析
## 背景
TEE是我们（AAStar）依靠的一个安全基石之一，我们假设硬件厂家不会作恶，黑客有很高成本攻克硬件安全设施。
当然ZKP会后面引入，这样相互制衡，硬件作恶，也无法伪造凭证(因为算法验证而非依赖硬件），从而制造一个均衡下的多方验证安全。
本blog会汇总TEE相关的研究分析在此。
[TEE](Blog/TEE/TEE-analysis.md)
[TEE-OpenClave](Blog/TEE/TEE-OpenClave.md)
[TEE-VM](Blog/TEE/TEE-VM.md)
[TEE-SGX](Blog/TEE/TEE-SGX.md)
[TEE-wallet](Blog/TEE/TEE-wallet.md)
[NixOS](Blog/TEE/NixOS.md)
[VM](Blog/TEE/VM-Investigation.md)

## OpenClave TEE OS 架构与操作解析

OpenClave 作为一个开源的可信执行环境操作系统，构建了一个与主要的、可能不受信任的普通世界（Normal World，常称为富执行环境 REE，承载如 Linux 或 Android 等操作系统）相隔离的安全世界 (Secure World)。

以下是其操作流程的更详细分解：

系统启动与 TEE 初始化：

设备启动时，通常会启动一个安全启动 (Secure Boot) 流程。此流程负责加载并验证普通世界操作系统和 OpenClave TEE 操作系统。
OpenClave 独立引导启动或由早期引导阶段加载，从而建立隔离的安全世界。它会初始化其核心功能，并准备托管可信应用。
安全世界中的可信应用 (Trusted Applications, TAs)：

您提到的“基于 SDK 的 server 端”即是可信应用 (TA)。
TAs 被安全地加载并在 OpenClave TEE OS（即安全世界）内部完整执行。它们被设计用于执行敏感操作，例如加密功能、安全数据存储或关键业务逻辑，并受到保护，免受来自普通世界的威胁。
该 SDK 为 TAs 提供了访问 TEE 特定资源和 API（通常遵循如 GlobalPlatform TEE 内部核心 API 等标准）的能力，以利用 TEE 的安全特性。
普通世界中的客户端应用 (Client Applications, CAs)：

您提到的“client 端”即是客户端应用 (CA)，它运行在普通世界的操作系统（例如 Linux、Android）中。
CAs 本身不被视为可信的，并在 TEE 的保护边界之外运行。
通过标准化接口提供服务：

OpenClave 内的 TAs 向普通世界中的 CAs 暴露安全服务。
CA 与 TA 之间的通信由 TEE 基础设施协调，并且通常遵循标准化的 TEE API，例如 GlobalPlatform TEE 客户端 API。
当 CA 需要一项安全服务时，它会使用 TEE 客户端 API 向特定的 TA 发出请求。这通常会触发一次从普通世界到安全世界的上下文切换，此切换常通过安全监控调用 (Secure Monitor Call, SMC) 指令来管理。
安全服务执行与通信协议：

OpenClave TEE 操作系统接收到请求后，会将其路由到指定的 TA。
TA 在隔离的安全世界内处理该请求，执行必要的操作。
处理结果随后被安全地返回给普通世界中的 CA，此过程通常也涉及 SMC 和上下文切换。
总结来说：

OpenClave 构建了一种双操作系统架构，其中可信应用 (TAs) 在其安全且隔离的环境（安全世界）中运行，为驻留在主操作系统（普通世界）中的客户端应用 (CAs) 提供受保护的服务。这种交互由标准化的 TEE API（例如 GlobalPlatform 规范）进行约束，确保由 TAs处理的敏感数据和计算免受普通世界中潜在的威胁。其“独立引导启动”特性确保了 TEE 本身的完整性，之后它才能开始提供这些安全服务。

该模型是 TEE 如何为各种应用（包括移动支付、数字版权管理 (DRM) 和企业安全解决方案）提供增强安全性的基础。