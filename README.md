# AuditForge

AI-powered smart contract security auditor. Built with Hermes Agent + MiMo V2.5.

## What It Does

AuditForge reads Solidity source code BEFORE deployment and finds vulnerabilities:
- Reentrancy detection with cross-function tracing
- Flash loan price manipulation analysis
- Access control verification
- Gas optimization suggestions
- Upgrade safety checks

## Architecture

```
Solidity Source → AST Parser → MiMo V2.5 Reasoning → Vulnerability DB → Audit Report
```

## Why MiMo V2.5?

Rule-based tools catch known patterns. MiMo V2.5 understands Solidity semantics and traces multi-step attack vectors across function boundaries.

## License

MIT
