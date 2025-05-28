# Task list
## Duration
30 days
## Result
Report and conclusion of AAStar price logic and docs.

## Format
PhD research format, under 6000 words.

## Payroll
160U

## Target: Industy Price investigation

Target:comparing industry AA providers product and price, get a research and 
guide AAStar open source products price strategy.

## Scope
10 AA providers in industry
suggestion:

|                         |                                         |                                          |                                      |                                    |                                         |                                              |                                             |                                             |
| ----------------------- | --------------------------------------- | ---------------------------------------- | ------------------------------------ | ---------------------------------- | --------------------------------------- | -------------------------------------------- | ------------------------------------------- | ------------------------------------------- |
| **Feature/Solution**    | **Pimlico**                             | **ZeroDev**                              | **Alchemy**                          | **Biconomy**                       | **Coinbase**                            | **Particle Network**                         | **Stackup**                                 | **AAStar**                                  |
| Main Features           | Bundler and Paymaster Infrastructure    | Modular Smart Accounts and Plugin System | Full-stack AA Toolkit                | Modular Cross-chain Smart Accounts | Ecosystem-specific AA Solution          | Cross-chain Unified Account and Balance      | Enterprise-grade Smart Account Solution     | A Community & Decentralized Account for All |
| Core Products           | Alto Bundler, Verifying/ERC20 Paymaster | Kernel Smart Account, Plugin System      | Account Kit, Rundler, Gas Manager    | Modular Smart Account, MEE         | Verifying Paymaster, Bundler API        | Universal Accounts, Omnichain Paymaster      | Enterprise Smart Wallet, Paymaster API      | SuperPaymaster, AirAccount, and COS72       |
| Smart Account Standard  | Universal                               | ERC-7579                                 | ERC-6900                             | ERC-7579                           | Universal                               | Proprietary+ERC-4337                         | Universal                                   | ERC-4337 EIP-7702                           |
| Cross-chain Capability  | Medium (Multi-chain Deployment)         | Medium (Multi-chain Deployment)          | Medium (Multi-chain Deployment)      | High (MEE)                         | Low (Base-focused)                      | Very High (Universal Account)                | Medium (Multi-chain Deployment)             | Limited, Future                             |
| ERC20 Gas Payment       | Full Support                            | Full Support                             | Full Support                         | Full Support                       | Partial Support                         | Full Support                                 | Full Support                                | Support                                     |
| Gas Sponsorship Method  | API Key, Webhook Policies               | Meta-infrastructure Proxy                | Gas Manager, Policy Engine           | Paymaster API, Policies            | Base Ecosystem Optimized                | Chain Abstraction Layer Sponsorship          | API Key, Enterprise Policies                | Hold SBT and Sponsored Seamlessly           |
| Open Source Status      | Highly Open Source                      | Highly Open Source                       | Partially Open Source                | Highly Open Source                 | Partially Open Source                   | Progressively Opening                        | Partially Open Source                       | Open Source                                 |
| Development Complexity  | Low-Medium                              | Medium                                   | Medium-High                          | Medium                             | Low                                     | Medium                                       | Medium-High                                 | Low                                         |
| Core SDK                | permissionless.js                       | @zerodev/sdk                             | @alchemy/aa-core                     | @biconomy/account                  | @coinbase/various-sdks                  | @particle-network/aa-sdk                     | userop.js                                   | AAStar SDK                                  |
| PassKey Support         | Via Integration                         | Native Support                           | Via Plugins                          | Via Modules                        | Via Integration                         | Via Auth Service                             | Native Support                              | Native Support                              |
| Suitable Use Cases      | Infrastructure Support                  | Consumer Apps, Gaming                    | Enterprise Apps, Complex DeFi        | Cross-chain Apps, DeFi             | Base Ecosystem Apps                     | Cross-chain Apps, Bitcoin L2                 | Enterprise Collaboration Apps               | Ethereum, Layer2(SuperChain and more)       |
| User Count (BundleBear) | N/A (Infrastructure)                    | ~900K Accounts                           | ~7.3M Light Accounts                 | ~224K Accounts                     | ~36K Accounts                           | ~200K+ on Bitcoin L2                         | ~34K Accounts                               | Infra, beginning                            |
| Advantages              | High Performance, Reliability           | Modularity, Gas Efficiency               | Complete Toolkit, Enterprise Support | Cross-chain Capability, Modularity | Base Ecosystem Integration, Ease of Use | Cross-chain Unified Account, Bitcoin Support | Enterprise Security, Collaboration Features | Dual Signature and Web2 UX                  |
| Disadvantages           | Infrastructure Only                     | Plugin System Learning Curve             | Some Features Not Open Source        | Infrastructure Dependencies        | Ecosystem Limitations                   | Newer Solution                               | Enterprise Focus, Generality                | Still on developing                         |



## Resource
1. Most of them use CUs or SAAS model, but we use open source model.

## SAAS
Order the API and platform service and pay monthly.
Also they get a 10% or less service fee per transaction sponsorship.
and you should pay monthly or pay as your quotation using.

https://docs.pimlico.io/guides/pricing




## CUs
The logic is sell the computing service in cloud with their own service abilities like AA RPC and more.

Compute units are a measure of the total computational resources your apps are using on Alchemy. You can think of this as how you would pay Amazon for compute usage on AWS. Some queries are lightweight and fast to run (e.g., eth_blockNumber) and others can be more intense (e.g., large eth_getLogs queries). Each method is assigned a quantity of compute units, derived from global average durations of each method.
https://www.alchemy.com/pricing

| Method                   | CUThroughput | CU   |
| :----------------------- | :----------- | :--- |
| getNFTMetadata           | 80           | 10   |
| getContractMetadata      | 160          | 10   |
| getCollectionMetadata    | 240          | 10   |
| getNFTsForOwner          | 480          | 100  |
| getContractsForOwner     | 320          | 100  |
| getCollectionsForOwner   | 360          | 100  |
| getNFTsForContract       | 480          | 50   |
| getOwnersForNFT          | 80           | 10   |
| getOwnersForContract     | 480          | 20   |
| getFloorPrice            | 80           | 10   |
| getNFTSales              | 160          | 10   |
| computeRarity            | 80           | 10   |
| summarizeNFTAttributes   | 80           | 10   |
| isHolderOfContract       | 80           | 10   |
| searchContractMetadata   | 480          | 50   |
| getNFTMetadataBatch      | 480          | 100  |
| getContractMetadataBatch | 480          | 100  |
| getSpamContracts         | 480          | 10   |
| isSpamContract           | 80           | 10   |
| isAirdropNFT             | 80           | 10   |
| invalidateContract       | 80           | 80   |
| refreshNftMetadata       | 40           | 10   |
| reingestContract         | 480          | 480  |
| reportSpam               | 0            | 10   |


https://www.alchemy.com/docs/reference/compute-units

## Other model?

## AAStar price model