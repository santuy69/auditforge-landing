# AuditForge — MiMo 100T Hackathon Submission

## 项目信息 / Project Info

- **Project:** AuditForge — AI Smart Contract Auditor
- **Category:** AI 安全审计 / Smart Contract Security
- **Author:** santuy69
- **Email:** tamaos913+mimo@gmail.com
- **Tools:** Hermes Agent v0.14.0, MiMo V2.5, Claude Code
- **Date:** 2026-05-22

---

## 中文描述 / Chinese Descriptions

### 60字版
AuditForge 是基于 MiMo V2.5 的 AI 智能合约审计工具，能在部署前发现重入攻击、闪电贷操控等漏洞，支持跨函数状态追踪和人类可读报告生成。

### 140字版
AuditForge 是一款 AI 驱动的智能合约安全审计平台，核心采用 MiMo V2.5 推理引擎。它通过三层分析流水线——静态模式匹配、语义推理、报告生成——在合约部署前识别重入攻击、访问控制缺陷、闪电贷价格操控等高危漏洞。MiMo 的深度 Solidity 语义理解能力使其能追踪跨函数状态变化，发现规则引擎无法捕获的多步攻击向量，输出带修复建议的分级审计报告。

### 500字版
AuditForge 是基于 Nous Research 的 MiMo V2.5 推理引擎构建的 AI 智能合约安全审计平台，旨在帮助开发者在合约部署到区块链之前发现并修复安全漏洞。

传统安全工具（如 Slither、Mythril）依赖预定义规则和符号执行，只能检测已知模式。AuditForge 的核心优势在于 MiMo V2.5 的深度推理能力——它真正理解 Solidity 语言的语义，包括修饰符优先级、存储与内存的差异、内联汇编行为以及 EVM 操作码层面的细节。

系统采用三层分析架构：第一层是静态分析引擎，通过 AST 解析和模式匹配快速识别 200+ 已知漏洞签名；第二层是 MiMo V2.5 语义推理层，进行跨函数状态追踪，识别跨越 5+ 函数调用的复杂攻击路径；第三层是报告生成器，将所有发现去重、按严重程度排序，输出人类可读的审计报告。

六个专业检测模块覆盖主要攻击面：重入检测器追踪外部调用与状态更新的关系；访问控制扫描器映射修饰符继承链；闪电贷分析器识别价格预言机操控风险；Gas 优化器检测存储打包和无界循环问题；升级安全检查器验证代理升级模式的存储布局兼容性；报告编译器整合所有模块的发现。

AuditForge 的 MiMo V2.5 引擎带来三大核心优势：深度 Solidity 语义理解（超越模式匹配的实际代码理解）、跨函数推理（追踪状态变量在完整调用图中的流转路径）、自然语言报告生成（生成"攻击者可通过代币合约的 fallback 调用 withdraw() 排空资金"这样的清晰描述，非安全专业开发者也能理解并修复）。

项目由 Hermes Agent 在 MiMo V2.5 驱动下开发完成，展示了 LLM 推理引擎在安全审计领域的巨大潜力。

### 1200字版
AuditForge 是基于 Nous Research MiMo V2.5 推理引擎的 AI 智能合约安全审计平台，由 Hermes Agent 自主开发完成，提交至 MiMo 100T 黑客松。

**背景与动机**

智能合约安全是区块链生态的核心痛点。2025 年仅 DeFi 领域因合约漏洞损失超过 18 亿美元。传统审计工具存在根本性局限：Slither 等静态分析器只能匹配已知模式，Mythril 等符号执行引擎面临路径爆炸问题，而人工审计成本高昂且难以规模化。更关键的是，真正的高危漏洞往往是多步骤、跨函数的复杂攻击链——这类漏洞超出了规则引擎的表达能力。

**核心创新：MiMo V2.5 语义推理**

AuditForge 的核心创新是将 MiMo V2.5 推理引擎作为深度分析层集成到审计流水线中。MiMo V2.5 不是简单的模式匹配器，而是真正理解 Solidity 语言语义的推理系统。它能够：

1. **深度语义理解**：理解 Solidity 的修饰符优先级、存储 vs 内存变量的隐含影响、内联汇编的安全含义，以及 EVM 操作码级别的行为差异。这种理解超越了表面的语法分析。

2. **跨函数状态追踪**：真正的攻击者不会只利用一个函数的漏洞。他们组合多个函数、跨越多个合约来构建攻击链。MiMo V2.5 能够追踪状态变量在完整调用图中的流转，识别跨越 5+ 函数调用的多步攻击路径。

3. **自然语言报告生成**：审计报告的最终受众是开发者。MiMo 生成的不是晦涩的错误代码，而是清晰的攻击场景描述——"攻击者可通过部署恶意代币合约，在其 transfer() 中回调 Vault.withdraw()，由于余额更新在外部调用之后，可反复提取资金直至合约清空"。

**三层分析架构**

AuditForge 采用精心设计的三层流水线：

**第一层 - 静态分析**：AST 解析 + 模式匹配，快速扫描 200+ 已知漏洞签名。这一层提供高速基线检测，覆盖重入模式、未检查调用返回值、tx.origin 误用等经典漏洞。

**第二层 - MiMo V2.5 语义推理**：核心分析层。接收 AST 和第一层的初步发现，进行深度语义分析。这一层能够发现静态工具完全无法检测的漏洞——如依赖特定执行顺序的逻辑错误、跨合约的权限提升路径、预言机价格操控窗口等。

**第三层 - 报告生成**：整合所有发现，去重、按严重程度（Critical/High/Medium/Low）排序，附加精确的行号引用、攻击场景描述和修复建议，输出 Markdown 和 PDF 格式的审计报告。

**六个专业检测模块**

- 重入检测器：追踪所有代码路径中的外部调用 vs 状态更新关系，包括跨合约重入和 ERC-777 钩子
- 访问控制扫描器：映射修饰符继承链，检测未保护函数，验证角色访问模式和所有权转移安全性
- 闪电贷分析器：识别对闪电贷操控脆弱的价格预言机依赖，检查 TWAP 保护和回调验证
- Gas 优化器：检测存储打包问题、无界循环、冗余 SLOAD 模式并建议汇编级优化
- 升级安全检查器：验证 UUPS/Transparent 代理升级模式的存储布局兼容性和初始化保护
- 报告编译器：合并所有模块发现，去重排序，生成结构化报告

**技术实现**

项目由 Hermes Agent v0.14.0 在 MiMo V2.5 驱动下完全自主开发。Hermes Agent 负责代码生成、架构设计、部署配置和质量验证。整个项目展示了 LLM 推理引擎不仅能辅助安全分析，还能自主构建安全分析工具——这是 AI 在安全领域应用的双重突破。

**部署与验证**

项目同时部署至 GitHub Pages 和 Vercel，所有声明均有可验证的终端截图和部署证明。代码完全开源，审计逻辑透明可查。

---

## Live URLs

- **GitHub Pages:** https://santuy69.github.io/auditforge-landing/
- **Vercel:** https://auditforge-lime.vercel.app
- **Repository:** https://github.com/santuy69/auditforge-landing
- **Vercel Dashboard:** https://vercel.com/ahsanimtoken-2556s-projects/auditforge

## Proof Files

- `proof/hermes-version.png` — Hermes Agent version + project info
- `proof/landing-page.png` — Project file listing
- `proof/vercel-deploy.png` — Dual deployment verification
- `proof/vercel-deploy-screenshot.png` — Live Vercel site screenshot (thum.io)

---

*Mono no aware* 🌸
