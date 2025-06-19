# Blog Board
## 用 n8n + Gemini + SearXNG 简易复刻一个免费的 Deep Research 低代码 n8n教程
![](https://raw.githubusercontent.com/jhfnetboy/MarkDownImg/main/img/202506191012043.png)

Date: 19 June 2025

Link: DeepResearchTutorial.md (/blog/infra/DeepResearchTutorial.md)

Deep Research类AI产品虽然功能强大，但其高昂的搜索API成本常常让人望而却步，例如SerpAPI每5000次搜索收费75美元，Google官方API每1000次查询高达35美元。本教程介绍了一种低成本的替代方案：通过n8n结合Gemini和开源搜索引擎SearXNG，搭建一个免费的Deep Research自动化工作流。用户只需下载提供的n8n工作流文件（DeepResearch_With_SearXNG.zip），即可在本地部署并实现AI驱动的搜索与数据处理。SearXNG作为开源搜索API，不仅免费，还能聚合多个搜索引擎结果，打破单一引擎限制。教程详细讲解了如何将n8n工作流配置为AI Agent工具，让用户灵活调用非标准服务，实现高效、低成本的自动化研究。
原文：https://vibe.akashio.com/t/topic/145[](https://vibe.akashio.com/t/topic/145)

Keywords:  
自动化工作流  

开源搜索  

n8n  

SearXNG  

Gemini  

Deep Research  

低代码  

AI Agent




## 纯净数据：可验证的中心化RPC链上数据
![](https://raw.githubusercontent.com/jhfnetboy/MarkDownImg/main/img/202506122224165.png)

**Date**: 12 June 2025
**Link**: [PureData.md](/blog/infra/PureData.md)


EIP-7919: Pureth 旨在解决以太坊用户过度依赖中心化RPC服务商所带来的安全与隐私风险。该提案通过改造区块、交易等核心数据结构，使其采用基于树的哈希。这使得RPC响应能直接附带高效的正确性与完整性证明，用户无需再盲目信任数据来源，可自行验证，从而实现信任最小化并抵御欺诈。此举还能提供更紧凑的证明以降低成本，并保证前向兼容性，为以太坊构建一个更安全、保护隐私且经济高效的数据访问基础。
原文：https://ethereum-magicians.org/t/glamsterdam-headliner-proposal-pureth/24459

**Keywords**:
- 数据泄露
- 隐私保护
- ZK加密
- 数据主权
- 社会工程学
- 数据变现
- 去中心化
- 个人隐私

## 数据泄露的经济学思考：从羔羊到数据主权
<img src="https://raw.githubusercontent.com/jhfnetboy/MarkDownImg/main/img/202506081156230.jpg" alt="Data Leak" width="50%"/>
<img src="https://raw.githubusercontent.com/jhfnetboy/MarkDownImg/main/img/202506081129813.png" alt="Data Security" width="50%"/>

**Date**: 8 June 2025
**Link**: [Data-Leak.md](/blog/economics/Data-Leak.md)

从经济学视角深入分析数据泄露问题。探讨了中心化平台对用户数据的控制与利用，以及当前数据保护机制的缺陷。文章提出了基于ZK和加密算法的个人数据自主管理方案，包括70多个数据字段的分类销售模型，以及基于客观数据和外部反馈的动态评估机制。同时讨论了社会工程学数据库的威胁，并提供了个人数据保护的实践建议。

**Keywords**:
- 数据泄露
- 隐私保护
- ZK加密
- 数据主权
- 社会工程学
- 数据变现
- 去中心化
- 个人隐私

## 以太坊轻客户端详解
我先说个人分析的结论：轻节点严重依赖全节点来提供大部分服务,目前layer2 dapp无法方便使用（核心是去中心，相比于Alchemy RPC），未来依赖rachive节点+全节点改造和提升+layer2专用轻节点+硬件算力提升成本下降+硬件需求下降，可能是一个思路，而轻节点应该再次退化更轻点？

Light clients enable more people to use Ethereum as first-class citizens, verifying data on the blockchain without relying on centralized service providers. Lodestar is actively contributing to light client development for Ethereum.

<img src="https://lodestar.chainsafe.io/window2.png" width="50%"/>

**Date**: 4 June 2025
**Link**: [Ethereum-Light-Client.md](/blog/infra/Ethereum-Light-Client.md)

深入分析以太坊轻客户端的能力、发展情况、安装部署及调用方法。

**Keywords**:
- light client
- light-ethjs
- lodestar
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
