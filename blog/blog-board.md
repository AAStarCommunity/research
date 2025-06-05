# Blog Board

## 以太坊轻客户端详解
我先说个人分析的结论：轻节点严重依赖全节点来提供大部分服务,目前layer2 dapp无法方便使用（核心是去中心，相比于Alchemy RPC），未来依赖rachive节点+全节点改造和提升+layer2专用轻节点+硬件算力提升成本下降+硬件需求下降，可能是一个思路，而轻节点应该再次退化更轻点？

Light clients enable more people to use Ethereum as first-class citizens, verifying data on the blockchain without relying on centralized service providers. Lodestar is actively contributing to light client development for Ethereum.

![Lodestar](https://lodestar.chainsafe.io/window2.png)

**Date**: 4 June 2025
**Link**: [Ethereum-Light-Client.md](/blog/infra/Ethereum-Light-Client.md)

深入分析以太坊轻客户端的能力、发展情况、安装部署及调用方法。

**Keywords**:
- EIP-4844
- Blob Data
- Pectra
- Optimism
- Layer2
- 数据可用性
- 全节点
- Rollup

---

## SDSS雨计算：去中心化服务系统的技术架构
![SDSS Architecture](https://raw.githubusercontent.com/jhfnetboy/MarkDownImg/main/img/202506031332213.png)
**Date**: 3 June 2025
**Link**: [SDSS-Rain-Computing.md](/blog/infra/SDSS-Rain-Computing.md)

深入探讨SDSS（标准去中心化服务系统）的技术架构和实现细节。作为云计算的替代方案，SDSS/Rain Computing通过去中心化方式提供计算服务，同时避免数据和计算能力的垄断。文章详细介绍了V0.1版本的核心组件，包括节点体系（N0-N3）、服务发现机制、ENS集成以及声誉系统等关键特性，并探讨了去中心化服务的未来发展方向。

**Keywords**:
- 雨计算
- 去中心化服务
- ENS
- TEE
- 边缘计算
- 服务发现
- 声誉系统
- 分布式架构

---

## 平台垄断与协作创新：从美团到去中心化平台的思考
<img src="https://img.meituan.net/smartvenus/a8d3630547a9bc02c113b24f730446e9891533.png" width="50%" alt="Platform Economy vs DAO"/>

**Date**: 2 June 2025
**Link**: [Monopoly&Cooperation.md](/blog/economics/Monopoly&Cooperation.md)

深入探讨平台经济的垄断本质与协作创新的可能性。通过分析美团和阅文集团等案例，揭示了平台经济如何通过技术创新创造价值，但同时也带来价值分配不均的问题。文章提出了基于区块链和DAO的协作平台"好团"概念，探索一种能够平衡效率与公平的新型经济模式。包含详细的技术框架设计、经济模型分析和治理机制建议。

**Keywords**:
- 平台经济
- 去中心化
- DAO
- 区块链治理
- 协作创新
- 价值分配
- 开源协作
- 社会福祉

## OP-TEE TEE OS 架构与操作解析
![TEE Architecture](https://raw.githubusercontent.com/jhfnetboy/MarkDownImg/main/img/202505301409954.png)
https://optee.readthedocs.io/en/latest/general/about.html

<img src="https://raw.githubusercontent.com/jhfnetboy/MarkDownImg/main/img/202505101719766.png" width="50%"/>

**Date**: 30 May 2025
**Link**: [blog-3.md](/blog/blog-3.md)

深入分析OP-TEE可信执行环境操作系统的架构和工作原理，探讨了其在安全世界和普通世界之间的隔离机制，以及TEE作为AAStar安全基石的重要性。包含了系统启动、安全应用执行和通信协议等关键环节的详细解析。

**Keywords**:
- TEE
- OP-TEE
- 安全架构
- Trusted Applications
- Secure World
- 系统安全
- SGX
- 硬件安全

---

## gRPC和libp2p的结合使用研究
![](https://www.grpc.io/img/landing-2.svg)
**Date**: 28 May 2025
**Link**: [blog-1.md](/blog/blog-1.md)

深入探讨gRPC和libp2p在网络协议栈中的位置，以及如何在P2P架构中结合使用这两种技术。分析了从传统分布式系统迁移到P2P模式的技术考量。

**Keywords**:
- gRPC
- libp2p
- Protocol Buffers
- P2P
- 分布式系统
- 网络协议
- Rust
- 系统架构

---

## DePIN和边缘计算的硬件选型
![](https://docs.toradex.com/114705-verdn-imx95-evk.png?_gl=1*164vy2*_gcl_au*MTgwNjY4MDE5My4xNzQ4NTAzNjI0*_ga*MTA3MzE0MjgwNS4xNzQ4NTAzNjI0*_ga_LBHPF2CRC5*czE3NDg1MDM2MjQkbzEkZzEkdDE3NDg1MDUzMTIkajYwJGwwJGgw)
**Date**: 29 May 2025
**Link**: [blog-2.md](/blog/blog-2.md)

SDSS和Rain Computing探索DePIN实现方式的硬件选型分析，重点关注NXP i.MX95等ARM芯片的性能、成本和供应稳定性。

**Keywords**:
- DePIN
- 边缘计算
- ARM芯片
- NXP i.MX95
- 硬件选型
- TEE
- 系统架构
- 物联网

---