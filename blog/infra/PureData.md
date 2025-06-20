# 纯净数据：可验证的中心化RPC链上数据

原文：https://ethereum-magicians.org/t/glamsterdam-headliner-proposal-pureth/24459
![](https://raw.githubusercontent.com/jhfnetboy/MarkDownImg/main/img/202506122224165.png)

这和轻客户端目标有部分是一致的(不信任中心化RPC），但没有深入看，而且是craft状态，观察跟进。

---

**EIP-7919: Pureth** 整合了一系列改进，旨在让用户无需依赖受信任的 RPC 提供商或第三方索引器，即可更轻松地访问和验证以太坊数据。这些改进通过改变区块、交易和收据的数据结构来实现此目标，从而可以将高效的**正确性**（即有效性）证明和**完整性**（即无遗漏）证明添加到 RPC 响应中。

能够验证 RPC 响应对于安全至关重要。如今，大多数钱包和 dApp 都从极少数大型 RPC 提供商处获取数据，这使得在 RPC 提供商遭到黑客攻击、变为恶意行为者或使用了有缺陷的软件版本的情况下，用户将面临数据不正确和不完整的风险。这可能会诱骗用户授权一笔欺诈性交易。此外，中心化基础设施会受到外部数据收集和隐私政策的影响；即使用户的不同钱包之间没有链上关联，他们也可能会被进行画像分析。并且，外部索引器的成本可能相当高昂，减少对它们的依赖有助于资金不足的开发者。

这次数据结构改造的机会也被用来从**扁平（线性）哈希**切换到**基于树的哈希**，当用户只对部分数据感兴趣时，这能够提供更紧凑的证明。例如，与证明整个交易收据相比，证明单个日志（log）可能会降低 gas 成本，这对智能合约和 L2 桥接有利。最后，它还实现了**前向兼容性**；当不相关的以太坊功能发生变化时，验证器将不再需要更新。这一直是质押池（如 Lido、RocketPool）所要求的，因为它们如今已经在使用来自信标链的树状结构数据。

总而言之，这些变革为以太坊构建一个**信任最小化、保护隐私且成本效益高**的数据访问基础设施奠定了基础。
资料：
https://eips.ethereum.org/EIPS/eip-7919
https://purified-web3.box/