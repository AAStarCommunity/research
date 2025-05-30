基于Rust语言在Intel SGX可信执行环境下开发应用程序的可行性调研报告
1. 引言
Intel软件防护扩展（SGX）是一项硬件辅助的可信执行环境（TEE）技术，旨在保护敏感代码和数据在不可信环境中免受泄露或篡改，即使操作系统和虚拟机监控器等特权软件受到威胁也能提供安全保障 1。这项技术通过在应用程序的地址空间内创建称为飞地的隔离、受保护的内存区域来实现这一目标，敏感计算可以在其中安全地进行 1。SGX提供的关键安全优势包括基于硬件的内存加密和隔离，可以防御各种软件攻击以及某些物理攻击 1。
Rust编程语言因其内存安全特性（所有权、借用和生命周期）而日益受到关注，这些特性消除了C/C++等语言中常见的内存损坏漏洞 1。Rust不依赖垃圾回收器进行内存管理，这既提升了安全性，又保证了性能，使其成为在SGX飞地约束环境下进行系统级编程的理想选择 2。
本可行性研究旨在深入探讨使用Rust编程语言在Intel SGX环境下开发针对Windows操作系统的应用程序的技术可行性、生态成熟度以及可用资源。报告将评估现有的Rust SGX开发框架，分析其在Windows平台上的支持情况，并探讨在Chiang Mai地区获取相关技术支持的可能性。
本报告的后续部分将详细分析Rust在Intel SGX开发中的可行性和成熟度，介绍Intel SGX的架构和开发基础，探讨现有的Rust SGX开发工具包，评估GitHub上的技术示例和开源项目，研究相关的官方文档和行业标准，分析在Windows上使用Rust和SGX进行应用开发的可能性，比较不同的Rust SGX开发框架，并探索在Chiang Mai获取本地支持的潜力。
2. Rust语言在Intel SGX开发中的可行性和成熟度
针对在SGX飞地中使用Rust进行内存安全编程的研究工作，例如Rust-SGX项目，已经证明了其可行性，并且与使用Intel SGX SDK进行原生C/C++开发相比，性能开销极小（小于5%）1。Rust-SGX通过构建在Intel SGX SDK之上，利用Rust的内存安全特性来增强飞地代码的安全性 1。
目前存在多个基于Rust的SGX开发框架，例如Apache Teaclave SGX SDK（前身为Baidu Rust SGX SDK）、Fortanix Enclave Development Platform（EDP）、smartcontractkit/rust-sgx-sdk和automata-network/automata-sgx-sdk 5。这些框架的存在以及Rust编程语言论坛 (42)、Keystone Enclave论坛 (43) 和Reddit讨论 (9) 中活跃的社区参与和支持，都表明了该生态系统的日益成熟。此外，将大量第三方Rust库移植到Intel SGX环境的工作也在进行中 9，这显著降低了使用Rust开发复杂SGX应用程序的工程负担。
尽管Rust在内存安全方面具有显著优势，但SGX开发的独特性质仍然带来一些固有的复杂性和潜在挑战。开发者需要采用与传统应用开发不同的范式，显式地将应用程序划分为在飞地内运行的可信组件和在外部运行的不可信组件 4。此外，SGX生态系统本身也可能存在潜在的安全漏洞 3，即使使用Rust这样的内存安全语言，也需要谨慎的编码实践以避免内存损坏问题 7。
Rust-SGX及各种基于Rust的SDK的积极研发，以及不断壮大的社区支持，有力地证明了使用Rust进行Intel SGX开发在技术上是可行的，并且生态系统正在不断成熟。然而，开发者需要充分认识到SGX开发所特有的挑战，并在整个开发生命周期中高度关注安全性。
3. Intel SGX架构与开发基础
Intel SGX架构的核心在于其创建和管理受保护的内存区域，即飞地 2。飞地页缓存（EPC）是硬件保护的内存区域，飞地代码和数据驻留在其中，其特性在于隔离性和加密性 6。SGX硬件实现了强大的隔离机制，确保飞地的内存内容对于在飞地外部运行的任何软件（无论其权限级别如何）都是不可访问的 2。
开发Intel SGX应用程序的基本原则是将应用程序的代码和数据划分为在飞地内运行的可信组件和在外部运行的不可信组件 4。可信组件和不可信组件之间的通信通过特定的机制进行，即从不可信侧发起进入飞地的飞地调用（ECALL），以及从飞地内部发起调用到不可信环境的OCALL 9。某些Rust SGX SDK可能需要使用飞地定义语言（EDL）来定义可信和不可信代码之间的接口，指定可以在飞地边界交换的函数和数据结构 16。
除了基本的隔离和加密之外，SGX还提供其他重要的安全特性，例如安全远程证明，它允许飞地以密码学方式向远程方证明其身份和代码的完整性 6，以及数据密封，它使飞地能够安全地存储持久性数据 9。
对Intel SGX架构及其独特的开发模式的深入理解是使用Rust构建安全飞地应用程序的前提。开发者必须仔细考虑应用程序的划分以及可信/不可信边界的影响。此外，不同的Rust SGX SDK在开发流程、EDL的使用以及飞地间通信机制方面可能存在差异。开发者应熟悉所选SDK提供的约定和工具。
4. 基于Rust的Intel SGX开发工具包
目前有多种基于Rust的Intel SGX开发工具包可供选择，每个工具包都提供了一组独特的功能、设计理念以及在易用性、性能、安全性及平台支持方面的权衡。
4.1 Apache Teaclave SGX SDK (前身为Baidu Rust SGX SDK)
Apache Teaclave SGX SDK (13) 提供了一个名为sgx_tstd的Rust标准库的兼容子集，使开发者能够在飞地环境中使用熟悉的Rust功能 9。该SDK的架构包含多个crate，例如用于基本数据类型定义的sgx_types，用于SGX可信运行时系统的sgx_trts，以及用于不可信运行时系统的sgx_urts 49。SDK附带了丰富的示例代码，演示了各种SGX特性和功能在Rust中的使用，包括参数传递、字符串操作、ECALL/OCALL、密码学、本地和远程证明、数据密封、线程和文件I/O 13。虽然Teaclave SGX SDK主要面向Linux环境，但其文档中提到了Visual Studio Code等跨平台工具 (47)，暗示了在Windows上进行开发的潜力。该SDK支持在兼容的Intel处理器上进行基于硬件的SGX执行，以及在没有SGX功能的机器上进行软件模拟 9。
4.2 Fortanix Enclave Development Platform (EDP)
Fortanix EDP (5) 采用了一种独特的方法，直接从Rust代码生成和运行飞地，从而消除了对传统Intel SGX SDK的依赖，并可能提供增强的安全性和更简化的开发体验 24。EDP以安全性为中心进行设计，强调其自定义API (fortanix-sgx-abi)、最小化的用户调用接口以及旨在缓解常见SGX漏洞的其他机制 24。该平台强调易用性，并与现有的Rust代码和许多标准的Rust crate高度兼容 10。Fortanix EDP作为Rust工具链中的二级目标得到官方支持，开发者可以通过rustup等标准工具轻松访问 10。
4.3 其他相关SDK
smartcontractkit/rust-sgx-sdk (13) 专注于为使用Rust开发SGX应用程序（尤其是在智能合约领域）提供稳定且可用于生产的环境 13。其代码仓库中提供了各种示例代码，展示了不同的SGX功能和用例 13。
automata-network/automata-sgx-sdk (16) 旨在帮助用户使用Rust在Intel SGX平台上快速构建安全飞地，强调其在设计自定义飞地接口方面的灵活性以及利用Rust的包管理器Cargo进行简化的构建过程 16。sgx-scaffold项目被推荐为开发者熟悉该SDK的起点 16。
多种Rust-based SDK的出现为开发者提供了丰富的选择，每个SDK都在易用性、性能、安全性以及平台支持方面提供了不同的权衡。开发者应根据其具体的项目需求、技术专长和安全目标选择最合适的SDK。虽然Apache Teaclave SGX SDK主要面向Linux，但其成熟度和丰富的文档使其成为一个值得考虑的起点，需要进一步研究其在Windows上的具体功能。Fortanix EDP独特的Rust原生方法在安全性和与Rust项目的集成方面具有潜在优势，但也需要仔细评估其Windows支持情况。
5. GitHub技术示例和开源项目
对主要Rust SGX SDK（apache/incubator-teaclave-sgx-sdk、fortanix/rust-sgx、smartcontractkit/rust-sgx-sdk、automata-network/automata-sgx-sdk）的GitHub代码仓库进行分析可以发现，它们都提供了大量的技术示例 13。这些仓库中的samplecode目录包含了涵盖基本SGX概念和更高级用例的各种示例，例如helloworld、crypto、attestation、sealeddata和threading 13。这些示例通常都有良好的文档记录，易于理解，并提供了可运行的代码，开发者可以方便地进行修改和学习。
在GitHub上搜索“Rust SGX”和“Intel SGX Rust SDK”还可以找到其他相关的开源项目和库。例如，enclaive/enclaive-docker-rust-sgx (12) 提供专门用于构建和部署基于Rust的SGX应用程序的Docker镜像，这可以简化设置和部署过程，包括在支持Docker的Windows系统上。此外，mobilecoinofficial/docker-rust-sgx-base (14) 提供了带有SGX库的Rust基础Docker镜像，有助于实现跨平台开发工作流程。
GitHub上丰富的技术示例和开源项目表明，围绕Rust和Intel SGX开发存在一个活跃且不断增长的社区，为开发者提供了大量的学习资源和潜在的构建模块。特别是SDK仓库中提供的示例代码，对于理解如何使用相应的SDK以及在Rust中实现常见的SGX功能至关重要。此外，像Docker镜像这样专门为Rust SGX开发提供的工具，可以显著简化开发和部署过程，潜在地减轻平台特定的复杂性并促进跨平台兼容性。
6. Intel SGX官方文档和标准
Intel官方提供了全面的SGX文档，包括Intel SGX开发者指南 (18) 和Linux* OS开发者参考 (20)。这些文档详细介绍了SGX的底层架构、关键安全特性和基本的开发流程。开发者应重点关注其中关于Windows支持以及在Windows操作系统上使用SGX的任何已知限制。此外，"Intel® 64 and IA-32 Architectures Software Developer's Manual Volume 3D SGX" (30) 是Intel SGX指令集架构的权威技术参考，提供了关于飞地创建、管理和底层硬件机制的深入细节。
可信计算组织（TCG）发布了与可信计算和可信执行环境（TEE）相关的行业标准和规范 (54)。这些规范包括可信平台模块（TPM）规范 (54)，TPM提供了一个基于硬件的信任根，以及与可信存储相关的规范 (55)，这可能与需要安全持久存储的SGX应用程序相关。TCG架构概述规范 (54) 提供了对可信计算的目标和架构原则的更广泛理解。
Intel官方文档是理解SGX架构和推荐开发实践的主要权威来源。针对Windows平台的开发者应优先查阅Intel SGX SDK for Windows*的文档。虽然TCG标准提供了可信计算的更广泛背景，但开发者在使用Intel SGX时应主要关注Intel的官方文档，以获取特定于平台的实现细节和指南。
7. 使用Rust和SGX进行Windows应用开发
使用Rust编程语言和Intel SGX技术开发Windows应用程序在技术上是可行的，这主要是由于Intel提供了官方的Intel SGX SDK for Windows*，以及Rust编程语言本身和一些Rust-based SGX SDK的跨平台特性 13。
对先前识别的Rust-based SGX SDK的支持情况进行分析发现，Apache Teaclave SGX SDK虽然主要面向Linux，但在其文档中提到了Visual Studio Code作为支持的开发环境 (47)，这表明在Windows上进行开发是可能的，尽管原生支持可能有限。Fortanix EDP声称具有平台独立性 (24)，并且与跨平台的Rust工具链集成，因此也可能支持Windows，但需要进一步研究。smartcontractkit/rust-sgx-sdk和automata-network/automata-sgx-sdk的文档主要关注Linux平台 (13)。
值得注意的是，Intel提供了专门针对Windows操作系统的官方Intel SGX SDK for Windows* (31)，其中包含了在Windows上开发SGX应用程序所需的工具和库，尽管该SDK主要使用C/C++语言。
根据研究，直接在Windows上使用Rust开发SGX应用程序可能存在一些限制或特定的要求。这可能包括对特定Windows版本的需求、某些Rust crate的兼容性问题，或者与Linux相比底层SGX平台软件的差异 13。
Microsoft Azure Marketplace上提供的enclaive GmbH VM镜像 (23) 明确支持在Azure上使用Rust和SGX，这表明即使本地Windows机器上的直接开发存在一些细微差别，但在基于Windows的云基础设施上运行基于Rust的SGX应用程序是切实可行的。
虽然许多Rust SGX SDK的主要重点似乎是Linux，但有迹象表明存在Windows支持，尤其通过官方Intel SGX SDK和Visual Studio Code等跨平台开发环境。Azure Marketplace的列表表明，在基于Windows的云基础设施上运行Rust SGX应用程序是可能的。
8. Rust SGX开发框架的比较分析
对关键的Rust SGX开发框架（Apache Teaclave SGX SDK、Fortanix EDP和smartcontractkit/rust-sgx-sdk）进行比较分析，可以帮助开发者根据其具体需求做出选择。下表总结了这些框架在关键方面的优缺点：




特性
Apache Teaclave SGX SDK
Fortanix EDP
smartcontractkit/rust-sgx-sdk
开发流程
成熟，丰富的示例，可能依赖EDL
精简，以Rust为中心，无EDL
专注于稳定性，生产使用，提供示例
性能
通常良好，针对Intel SDK的优化Rust封装
由于shim层可能开销较高
可能与Teaclave相当
安全性
依赖Intel SDK，通过Rust实现内存安全
强调安全性，独立于Intel SDK
通过Rust实现内存安全
Windows支持
有一些迹象（VSCode），但主要面向Linux
需要进一步调查
主要面向Linux
文档
广泛的在线文档和Wiki
提供良好的文档
通过cargo doc生成文档
社区支持
活跃的社区，Apache孵化
不断增长的社区，Slack频道
活跃的社区
Intel SGX SDK依赖
是
否
是
EDL需求
是（可能）
否
是（可能）

选择最适合Windows项目的Rust SGX开发框架取决于对项目特定需求的仔细评估，包括性能目标、安全需求、开发者对框架的熟悉程度以及框架提供的Windows支持水平。每个框架都有一组独特的权衡，理解这些权衡对于做出符合项目目标的明智决策至关重要。一个结构良好的比较表能够为用户提供关键框架特征的并列视图，使其能够快速识别最适合其特定用例的选项。
9. 案例研究和技术博客
针对使用Rust和SGX开发Windows应用程序的公开案例研究和技术博客进行检索发现，相关资料相对有限。这可能表明，这种特定的技术组合不如Linux上的开发那样普遍或公开记录。enclaive Azure VM镜像 (23) 是一个潜在的实际部署案例，它专注于在Azure的Windows云环境中加密使用中的数据。对比较不同Rust SGX SDK的技术博客（例如 28）进行分析，可以获取一些实践见解，但其中关于Windows开发的讨论较少。虽然底层Intel SGX SDK支持Windows，但与Rust特定SDK的集成以及相关的实际案例可能不如Linux那样丰富。
10. Chiang Mai当地技术社区和研究机构
为了探索在Chiang Mai地区获取关于Rust和Intel SGX开发的本地支持和信息的可能性，需要调查当地是否存在活跃的Rust用户组、技术聚会或会议 (59)。这些社区可以作为本地Rust开发者的资源，其中一些开发者可能对安全计算技术感兴趣。此外，还需要考察Chiang Mai大学 (60) 或该地区的其他研究机构是否正在进行与安全计算、可信执行环境或Rust编程语言相关的研究项目或拥有相关专业知识的教职员工。虽然有证据表明泰国存在Rust开发社区 (59)，包括Chiang Mai，但在这个本地社区中，Rust和Intel SGX开发这一特定领域的专业知识可能有限。需要进一步的调查和交流才能确定该特定技术组合的本地支持水平。
11. 结论与建议
本可行性研究表明，使用Rust开发针对Windows操作系统的Intel SGX应用程序是可行的，Rust的内存安全特性为构建安全应用程序提供了显著的优势。虽然Rust SGX在Windows上的生态系统可能不如在Linux上成熟，但官方Intel SGX SDK for Windows*的存在以及一些Rust-based SDK的跨平台潜力为开发者提供了可行的途径。
基于以上分析，提出以下建议：
使用Rust和Intel SGX开发安全的Windows应用程序是可行的，开发者应充分利用Rust在内存安全方面的优势，以降低常见漏洞的风险。
在选择Rust SGX SDK时，应仔细评估其对Windows的支持程度。可以优先考虑那些明确提到支持Windows或基于跨平台技术构建的SDK。
开发者应查阅官方Intel SGX SDK for Windows*的文档，以获取关于Windows平台特定实现细节、要求和潜在限制的第一手信息。
建议考虑使用Microsoft Azure等云平台，这些平台提供了专门用于运行机密计算工作负载的基础设施，包括在Windows Server虚拟机上运行基于Rust的SGX应用程序。
积极参与更广泛的Rust和SGX开发社区，通过在线论坛、邮件列表和社交媒体渠道寻求支持、分享经验并了解该领域最新的进展。
无论使用何种编程语言，开发任何SGX应用程序都必须将全面的安全考虑和严格的测试纳入整个开发生命周期，以确保受保护代码和数据的机密性和完整性。
Rust为使用Intel SGX开发安全Windows应用程序提供了一个有希望的途径，它利用了Rust的内存安全特性。然而，与Linux相比，该生态系统可能不够成熟，开发者应仔细考虑SDK的选择和项目的具体要求。虽然可行，但开发者应准备好应对可能出现的更多挑战，并且可用的现成资源可能不如Linux开发那样丰富。细致的规划、深入的研究和对安全最佳实践的强烈关注对于成功的开发和部署至关重要。
Works cited
Towards Memory Safe Enclave Programming with Rust-SGX - Google Research, accessed April 5, 2025, https://research.google/pubs/towards-memory-safe-enclave-programming-with-rust-sgx/
Overview of Rust SGX SDK | Download Scientific Diagram - ResearchGate, accessed April 5, 2025, https://www.researchgate.net/figure/Overview-of-Rust-SGX-SDK_fig1_320679650
Sigy: Breaking Intel SGX Enclaves with Malicious Exceptions & Signals - arXiv, accessed April 5, 2025, https://arxiv.org/html/2404.13998v1
An Evaluation of Methods to Port Legacy Code to SGX Enclaves - CSA – IISc Bangalore, accessed April 5, 2025, https://www.csa.iisc.ac.in/~vg/papers/fse2020/fse2020_html/
State of SGX Development - Steve Weis - Medium, accessed April 5, 2025, https://sweis.medium.com/state-of-sgx-development-3db860d40284
Intel SGX Explained - Cryptology ePrint Archive, accessed April 5, 2025, https://eprint.iacr.org/2016/086.pdf
TeeRex: Discovery and Exploitation of Memory Corruption Vulnerabilities in SGX Enclaves - CASA RUB, accessed April 5, 2025, https://casa.rub.de/fileadmin/img/Publikationen_PDFs/2020_TEEREX_Discovery_and_Exploitation_of_Memory_Corruption_Vulnerabilities_in_SGX_Enclaves_Publication_ClusterofExcellence_CASA_Bochum.pdf
FSI: Digital Investiga- tion The evidence beyond the wall: memory forensics in SGX environments - S3@Eurecom, accessed April 5, 2025, https://www.s3.eurecom.fr/docs/fsi21_oliveri.pdf
Rust SGX SDK v1.0.0 released! - Reddit, accessed April 5, 2025, https://www.reddit.com/r/rust/comments/8l5rch/rust_sgx_sdk_v100_released/
SGX target is now a Rust tier 2 platform, accessed April 5, 2025, https://users.rust-lang.org/t/sgx-target-is-now-a-rust-tier-2-platform/24779
Slalom: Fast, Verifiable and Private Execution of Neural Networks in Trusted Hardware, accessed April 5, 2025, https://openreview.net/forum?id=rJVorjCcKQ
SGX-ready Enclaive Docker Image for Rust Applications and Services - GitHub, accessed April 5, 2025, https://github.com/enclaive/enclaive-docker-rust-sgx
Rust SGX SDK provides the ability to write Intel SGX ... - GitHub, accessed April 5, 2025, https://github.com/smartcontractkit/rust-sgx-sdk
mobilecoinofficial/docker-rust-sgx-base: Base image builds for Rust with SGX libraries., accessed April 5, 2025, https://github.com/mobilecoinofficial/docker-rust-sgx-base
apache/incubator-teaclave-sgx-sdk: Apache Teaclave ... - GitHub, accessed April 5, 2025, https://github.com/apache/incubator-teaclave-sgx-sdk
GitHub - automata-network/automata-sgx-sdk, accessed April 5, 2025, https://github.com/automata-network/automata-sgx-sdk
intel/linux-sgx: Intel SGX for Linux - GitHub, accessed April 5, 2025, https://github.com/intel/linux-sgx
Intel(R) Software Guard Extensions Developer Guide, accessed April 5, 2025, https://cdrdv2-public.intel.com/671581/intel-sgx-developer-guide.pdf
A beginner's guide to Intel SGX: understanding and leveraging secure enclaves - Fleek.xyz, accessed April 5, 2025, https://fleek.xyz/blog/learn/intel-sgx-beginners-guide/
Intel(R) Software Guard Extensions Developer Reference for Linux* OS, accessed April 5, 2025, https://download.01.org/intel-sgx/sgx-linux/2.8/docs/Intel_SGX_Developer_Reference_Linux_2.8_Open_Source.pdf
Intel SGX SDK Developer Reference Linux 1.9 Open Source - Scribd, accessed April 5, 2025, https://www.scribd.com/document/381636862/Intel-SGX-SDK-Developer-Reference-Linux-1-9-Open-Source
Apache Teaclave (incubating) is an open source universal secure computing platform, making computation on privacy-sensitive data safe and simple. - GitHub, accessed April 5, 2025, https://github.com/apache/incubator-teaclave
Rust* Confidential Computing Runtime Environment - Azure Marketplace, accessed April 5, 2025, https://azuremarketplace.microsoft.com/en-us/marketplace/apps/enclaivegmbh1643578052639.vm-rust-sgx?tab=overview
Enclave Development Platform - Fortanix, accessed April 5, 2025, https://www.fortanix.com/platform/runtime-encryption/enclave-development-platform
SoK: SGX.Fail: How Stuff Gets eXposed - Purdue Computer Science, accessed April 5, 2025, https://www.cs.purdue.edu/homes/clg/files/sgxfail24.pdf
Intel SGX - Fortanix, accessed April 5, 2025, https://www.fortanix.com/intel-sgx
Towards Memory Safe Enclave Programming with Rust-SGX | Request PDF - ResearchGate, accessed April 5, 2025, https://www.researchgate.net/publication/337095583_Towards_Memory_Safe_Enclave_Programming_with_Rust-SGX
Secure computation in Rust: Using Intel's SGX instructions with Teaclave and Fortanix, accessed April 5, 2025, https://blog.lambdaclass.com/secure-computation-in-rust-using-intels-sgx-instructions-with-teaclave-and-fortanix/
public.thinkonweb.com, accessed April 5, 2025, https://public.thinkonweb.com/sites/icisc2023/media?key=site/icisc2023/3-1.pdf
kib.kiev.ua, accessed April 5, 2025, https://kib.kiev.ua/x86docs/Intel/SDMs/332831-082.pdf
Intel SGX SDK Setup | Confidential Computing 101 - Enclaive, accessed April 5, 2025, https://docs.enclaive.cloud/confidential-cloud/technology-in-depth/intel-sgx/getting-started/intel-sgx-sdk-setup
How to set up Intel SGX?. Intel Software Guard Extensions (SGX)… | by Hasini Witharana | Medium, accessed April 5, 2025, https://medium.com/@hasiniwitharana/how-to-set-up-intel-sgx-21227c4ea200
Intel® Software Guard Extensions SDK for Windows* (Intel® SGX SDK for Windows*), accessed April 5, 2025, https://www.intel.com/content/www/us/en/content-details/671222/intel-software-guard-extensions-sdk-for-windows-intel-sgx-sdk-for-windows.html
Develop application enclaves with open-source solutions in Azure Confidential Computing, accessed April 5, 2025, https://learn.microsoft.com/en-us/azure/confidential-computing/enclave-development-oss
intel/intel-sgx-ssl: Intel® Software Guard Extensions SSL - GitHub, accessed April 5, 2025, https://github.com/intel/intel-sgx-ssl
Building and Maintaining a Third-Party Library Supply Chain for Productive and Secure SGX Enclave Development - Semantic Scholar, accessed April 5, 2025, https://www.semanticscholar.org/paper/Building-and-Maintaining-a-Third-Party-Library-for-Wang-Ding/62dbd6101d8dab1bcf28d8e114c48c64edc85193
Faulty Point Unit: ABI Poisoning Attacks on Intel SGX - Jo Van Bulck, accessed April 5, 2025, https://vanbulck.net/files/acsac20-fpu.pdf
Towards a Rust SDK for Keystone Enclave Application Development - SciTePress, accessed April 5, 2025, https://www.scitepress.org/Papers/2023/116119/116119.pdf
fortanix/rust-sgx: The Fortanix Rust Enclave Development ... - GitHub, accessed April 5, 2025, https://github.com/fortanix/rust-sgx
[RFC][SGX] Use Fortanix EDP instead of rust-sgx-sdk · Issue #2887 · apache/tvm - GitHub, accessed April 5, 2025, https://github.com/apache/tvm/issues/2887?ref=blog.lambdaclass.com
Jim8y/awesome-sgx: A curated list of SGX code and resources. - GitHub, accessed April 5, 2025, https://github.com/Jim8y/awesome-sgx
The Rust Programming Language Forum, accessed April 5, 2025, https://users.rust-lang.org/
Better attestation and sealing?, accessed April 5, 2025, https://groups.google.com/g/keystone-enclave-forum/c/MZWJq_Qu5fY
incubator-teaclave-sgx-sdk/release_notes.md at master - GitHub, accessed April 5, 2025, https://github.com/apache/incubator-teaclave-sgx-sdk/blob/master/release_notes.md
Rust SGX SDK v1.1.3, accessed April 5, 2025, https://apache.googlesource.com/incubator-teaclave-sgx-sdk/+/HEAD/release_notes.md
incubator-teaclave-sgx-sdk/samplecode/tr-mpc/Readme.md at master - GitHub, accessed April 5, 2025, https://github.com/apache/incubator-teaclave-sgx-sdk/blob/master/samplecode/tr-mpc/Readme.md
Home · apache/incubator-teaclave-sgx-sdk Wiki - GitHub, accessed April 5, 2025, https://github.com/apache/incubator-teaclave-sgx-sdk/wiki
Packages · apache/incubator-teaclave-sgx-sdk - GitHub, accessed April 5, 2025, https://github.com/apache/incubator-teaclave-sgx-sdk/packages
Rust SGX SDK Documents, accessed April 5, 2025, https://dingelish.github.io/
Teaclave SGX SDK Documentation | Apache Teaclave (incubating), accessed April 5, 2025, https://teaclave.apache.org/sgx-sdk-docs/
Re: [dmlc/tvm] [RFC][SGX] Use Fortanix EDP instead of rust-sgx-sdk (#2887), accessed April 5, 2025, https://lists.apache.org/thread/z4b5kgqr2m69nnfgc6v7482zjp0hpbmb
Intel® Software Guard Extensions (Intel® SGX) Developer Guide, accessed April 5, 2025, https://www.intel.com/content/www/us/en/content-details/671334/intel-software-guard-extensions-intel-sgx-developer-guide.html
Intel® 64 and IA-32 Architectures Software Developer's Manual, Vo | eBay, accessed April 5, 2025, https://www.ebay.com/itm/256693353996
Trusted Computing Group, accessed April 5, 2025, https://trustedcomputinggroup.org/
TCG Storage Architecture Core Specification - Trusted Computing Group, accessed April 5, 2025, https://trustedcomputinggroup.org/resource/tcg-storage-architecture-core-specification/
TCG Specification Architecture Overview - Trusted Computing Group, accessed April 5, 2025, https://trustedcomputinggroup.org/resource/tcg-architecture-overview-version-1-4/
Trusted Computing Group Trusted Storage Specification - SNIA.org, accessed April 5, 2025, https://www.snia.org/sites/default/files/Cox-J_TCG_Trusted_Computing_Group_Storage_Spec.pdf
TCG Software Stack (TSS) Specification - Trusted Computing Group, accessed April 5, 2025, https://trustedcomputinggroup.org/resource/tcg-software-stack-tss-specification/
Rust Web3 Jobs in Thailand, accessed April 5, 2025, https://web3.career/web3-jobs-thailand+rust
Chiang Mai University Research Collaborative | Center for Global Health and Social Responsibility, accessed April 5, 2025, https://globalhealthcenter.umn.edu/research/chiang-mai-university-research-collaborative
Faculty of Social Sciences, Chiang Mai University - Wikipedia, accessed April 5, 2025, https://en.wikipedia.org/wiki/Faculty_of_Social_Sciences,_Chiang_Mai_University
Chiang Mai University - Institution Details - UMAP USCO, accessed April 5, 2025, https://usco2.umap.org/Institution/InstitutionDetails/220
Changing Chiang Mai - Lee Kuan Yew School of Public Policy, accessed April 5, 2025, https://lkyspp.nus.edu.sg/gia/article/changing-chiang-mai
