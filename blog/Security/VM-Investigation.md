# VM Investigation

### 主流区块链数量及分类

- **数量**：研究表明，大约有10-15个主流区块链支持智能合约，其中11个在本次调研中被详细分类。
- **分类依据**：根据虚拟机（VM）实现和Gas机制（或费用机制）进行划分。
- **主要发现**：主流区块链多采用EVM、WASM、SVM或自定义VM，费用机制因平台而异，通常与原生代币挂钩。
- **争议**：哪些区块链算“主流”可能因市场份额、采用率或技术特性而有不同看法。

#### 什么是主流区块链？

主流区块链通常指市场资本化高、交易量大或在行业内广泛采用的区块链平台。用户提到的Solana和Ethereum是支持智能合约的典型例子，因此本调研聚焦于类似平台。

#### 虚拟机和Gas机制

- **虚拟机（VM）**：区块链用于执行智能合约的运行环境，如以太坊的EVM。
- **Gas机制**：衡量区块链上操作计算成本的单位，通常以原生代币支付，如以太坊的ETH。

#### 表格概览

以下表格列出了11个主流区块链，按其VM实现和Gas机制分类，基于2025年4月24日的数据。

---

# 主流区块链按虚拟机实现和Gas机制分类

## 背景

区块链技术已从比特币的简单交易系统发展为支持复杂智能合约的平台。主流区块链，如以太坊和Solana，因其市场影响力、开发活跃度和应用广泛性而备受关注。本调研响应用户需求，聚焦于支持智能合约的主流区块链，分析其虚拟机（VM）实现和Gas机制（或费用机制），并提供分类表格。

## 方法

通过网络搜索和页面浏览，收集了关于主流区块链的最新信息。数据来源包括行业报告、技术文档和社区讨论。调研重点关注以下方面：

- **主流区块链的定义**：基于市场资本化、交易量和行业认可度。
- **虚拟机实现**：识别每个区块链用于执行智能合约的VM类型。
- **Gas机制**：分析交易费用如何计算和支付。
  由于“主流”定义可能因标准不同而变化，本调研选择了11个支持智能合约的区块链作为代表。

## 主流区块链列表

以下是调研中识别的11个主流区块链，均支持智能合约，适合按VM和Gas机制分类：

1. 以太坊（Ethereum）
2. 币安智能链（Binance Smart Chain）
3. Solana
4. 卡尔达诺（Cardano）
5. 波卡（Polkadot）
6. Avalanche（C-Chain）
7. Polygon
8. NEAR
9. Aptos
10. Stellar（Soroban）
11. 瑞波（XRP Ledger）

## 虚拟机实现

虚拟机是区块链执行智能合约的核心组件。以下是各区块链的VM类型：

- **EVM（以太坊虚拟机）**：以太坊首创，广泛用于支持Solidity语言的智能合约。币安智能链、Avalanche（C-Chain）和Polygon均兼容EVM。
- **WASM（WebAssembly）**：一种高效的跨平台字节码格式，波卡、NEAR和Stellar的Soroban使用WASM。
- **SVM（Solana虚拟机）**：Solana专有VM，优化了并行处理。
- **Move VM**：Aptos使用的VM，基于Move语言，强调安全性和资源管理。
- **Plutus**：卡尔达诺的智能合约平台，基于Haskell语言，非传统VM。
- **Hooks**：瑞波XRP Ledger的自定义智能合约系统，尚在开发中。

值得注意的是，卡尔达诺正在开发KEVM（K框架下的EVM），以实现EVM兼容性，但目前主要依赖Plutus。瑞波的Hooks系统较为独特，可能不完全符合传统VM定义。

## Gas机制

Gas机制用于衡量区块链操作的计算成本，通常以原生代币支付。以下是各区块链的费用机制：

- **EVM-based（以太坊、币安智能链、Avalanche、Polygon）**：使用Gas单位，每条操作码有固定或动态成本，支付代币分别为ETH、BNB、AVAX和MATIC。若Gas耗尽，交易失败，状态回滚。
- **Solana**：使用计算单位（Compute
  Units），根据操作消耗计算，费用以SOL支付，优化了高吞吐量场景。
- **波卡**：基于交易“权重”的费用模型，费用以DOT支付，权重反映计算和存储需求。
- **NEAR**：费用基于存储和计算使用量，以NEAR代币支付。
- **Aptos**：使用Gas机制，类似EVM，以APT支付。
- **卡尔达诺**：费用以ADA支付，基于交易大小（字节）和脚本执行成本（执行单位），非传统Gas模型。
- **Stellar（Soroban）**：费用以XLM支付，基于操作数量和数据存储需求。
- **瑞波（XRP
  Ledger）**：费用以XRP支付，包括基础费用和基于交易复杂度的额外费用。

## 分类表格

以下表格总结了11个主流区块链的VM实现和Gas机制：

| **区块链**           | **虚拟机实现**        | **Gas机制**                         |
| -------------------- | --------------------- | ----------------------------------- |
| 以太坊               | EVM                   | Gas（ETH）                          |
| 币安智能链           | EVM                   | Gas（BNB）                          |
| Avalanche（C-Chain） | EVM                   | Gas（AVAX）                         |
| Polygon              | EVM                   | Gas（MATIC）                        |
| Solana               | SVM                   | 计算单位（SOL）                     |
| 波卡                 | WASM                  | 基于权重的费用（DOT）               |
| NEAR                 | WASM                  | 存储和计算费用（NEAR）              |
| Aptos                | Move VM               | Gas（APT）                          |
| 卡尔达诺             | Plutus（基于Haskell） | 费用（ADA，基于交易大小和脚本执行） |
| Stellar              | Soroban（WASM）       | 费用（XLM，基于操作和数据存储）     |
| 瑞波（XRP Ledger）   | Hooks（自定义）       | 费用（XRP，基础费用+复杂度）        |

## 讨论

- **主流区块链数量**：调研识别了11个支持智能合约的主流区块链，但“主流”定义可能因市场动态而变化。例如，比特币虽为主流，但因不主要支持智能合约而未列入。其他区块链如Tron、EOS可能也具影响力，但未列入本次调研。
- **VM多样性**：EVM因其成熟生态而占主导地位，WASM因跨平台性受到青睐，SVM和Move
  VM则针对特定性能和安全需求。
- **费用机制差异**：EVM的Gas模型标准化但成本较高，Solana的计算单位优化了吞吐量，卡尔达诺和Stellar的费用模型更灵活但复杂。
- **局限性**：本调研为初步分析，未涵盖所有区块链（如Tezos、Algorand）。未来可扩展调研范围。

## 结论

研究表明，大约有10-15个主流区块链支持智能合约，其中11个在本调研中按VM实现和Gas机制分类。EVM是最常见的VM类型，而费用机制因平台设计而异，从传统的Gas到基于权重的费用模型不等。本表格为区块链开发者、研究者和用户提供了清晰的分类参考。

### 关键引用

- [Wikipedia - List of blockchains](https://en.wikipedia.org/wiki/List_of_blockchains)
- [TechTarget - Top 9 blockchain platforms to consider](https://www.techtarget.com/searchcio/feature/Top-9-blockchain-platforms-to-consider)
- [Blockchain Council - Top 10 blockchain platforms you need to know](https://www.blockchain-council.org/blockchain/top-10-blockchain-platforms-you-need-to-know-about/)
- [Built In - 23 blockchain platforms driving the industry](https://builtin.com/blockchain/blockchain-platforms)
- [Nervos - Comparing blockchain virtual machines](https://www.nervos.org/knowledge-base/comparing_blockchain_virtual_machines)
- [Cardano Stack Exchange - Is there a Cardano VM?](https://cardano.stackexchange.com/questions/8695/is-there-a-cardano-vm)
- [Cardano Developers - Virtual Machines Welcome](https://developers.cardano.org/en/virtual-machines/welcome/)
- [Stellar Documentation - Soroban Smart Contracts](https://soroban.stellar.org/)
- [Ripple Documentation - XRP Ledger Hooks](https://xrpl.org/hooks.html)
