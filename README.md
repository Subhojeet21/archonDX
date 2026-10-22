# ArchonDX (⚡)
> **Autonomous Multi-Tenant Architecture & AI-Code Governance Engine for Salesforce DX projects**  

![License](https://img.shields.io/badge/License-MIT-blue.svg)
![Version](https://img.shields.io/badge/Version-1.0.3-emerald.svg)
![Runtime](https://img.shields.io/badge/Platform-Claude_Code_CLI_%7C_VS_Code-purple.svg)
[![Audit Scope](https://img.shields.io/badge/Audit_Scope-Governor_Limits_%7C_FLS_%7C_AI_Integrity-critical.svg)]()
[![Installs](https://img.shields.io/github/downloads/Subhojeet21/archonDX/total?color=blue&label=Installs&logo=github)](https://github.com/Subhojeet21/archonDX/releases)
[![Installs](https://img.shields.io/github/downloads/Subhojeet21/archonDX/install.sh?label=Installs&color=blue&logo=github)](https://github.com/Subhojeet21/archonDX/releases)
[![Reviews Run](https://img.shields.io/github/downloads/Subhojeet21/archonDX/version.txt?label=Reviews%20Run&color=purple&logo=claude)](https://github.com/Subhojeet21/archonDX/releases)
[![Installs](https://img.shields.io/endpoint?url=https%3A%2F%2Fraw.githubusercontent.com%2FSubhojeet21%2FarchonDX%2Fbadges%2Finstalls.json)](https://github.com/Subhojeet21/archonDX/releases)
[![Reviews Run](https://img.shields.io/endpoint?url=https%3A%2F%2Fraw.githubusercontent.com%2FSubhojeet21%2FarchonDX%2Fbadges%2Freviews.json)](https://github.com/Subhojeet21/archonDX/releases)


---

## 💡 What is ArchonDX?

**ArchonDX** is an autonomous architectural review engine designed specifically for enterprise **Salesforce DX** environments. Embedded natively into your local developer workflow via **Claude Code (CLI and VS Code extension**, it acts as a virtual core reviewer that audits staged diffs and pull requests before code is committed or merged.

Unlike traditional static linters (such as PMD or ESLint) that only inspect single files in isolation, ArchonDX evaluates **cross-class call graphs**, **runtime governor boundaries**, and **data access permissions** across your entire local codebase.

---

## 🎯 Why Use ArchonDX? (The Business & Engineering Problem)

With generative AI assistants accelerating code generation, pull request velocity has multiplied—but so have subtle architectural regressions and review burden. AI-generated code often looks clean on the surface but contains critical multi-tenant anti-patterns that pass compilation and standard CI checks like:

* **Distributed $N+1$ Database Leaks:** SOQL/DML queries nested three classes down within caller loops.
* **Security Regressions:** Missing \`WITH USER_MODE\`, bypassing Field-Level Security (FLS) or tenant sharing models.
* **Synthetic "Coverage Padding":** AI-generated unit tests with zero assertion logic (\`System.assert(true)\`), written purely to bypass the 75% deployment threshold.
* **LWC Resource Leaks:** Unsubscribed Lightning Message Service (LMS) tokens and lingering DOM listeners causing browser memory decay.

ArchonDX performs semantic, cross-file architectural audits on Apex and Lightning Web Components before code ever reaches a pull request or before a pull request is merged.

---

## 🔬 Architecture: How ArchonDX Evaluates Beyond Static Linters

Traditional linters (PMD, ESLint, SonarQube) inspect isolated Abstract Syntax Trees (ASTs). They cannot detect cross-file side effects or understand architectural intent.

```
                    ┌───────────────────────────────────┐
                    │ Local Git Working Tree / PR Diff  │
                    └─────────────────┬─────────────────┘
                                      │
                                      ▼
                    ┌───────────────────────────────────┐
                    │ ArchonDX Workspace Hydrator       │
                    │ - Filter apex and lwc components  │
                    │ - Inspects Caller Call-Stacks     │
                    └─────────────────┬─────────────────┘
                                      │
            ┌─────────────────────────┼─────────────────────────┐
            ▼                         ▼                         ▼
┌───────────────────────┐ ┌───────────────────────┐ ┌───────────────────────┐
│ Lens A: Governor &    │ │ Lens B: Data Access   │ │ Lens C: Synthetic     │
│ Scalability Boundary  │ │ & Platform Security   │ │ Code & Test Integrity │
│ - Distributed N+1     │ │ - WITH USER_MODE      │ │ - Assert-less tests   │
│ - Queueable Chaining  │ │ - Explicit Sharing    │ │ - 200+ record bulk    │
│ - Heap & Cursor Guard │ │ - Dynamic SOQL binds  │ │ - Hallucinated APIs   │
└───────────┬───────────┘ └───────────┬───────────┘ └───────────┬───────────┘
            │                         │                         │
            └─────────────────────────┼─────────────────────────┘
                                      ▼
                    ┌───────────────────────────────────┐
                    │ Deterministic Version Pre-Flight  │
                    │ (GitHub API Release Check)        │
                    └─────────────────┬─────────────────┘
                                      │
                                      ▼
                    ┌───────────────────────────────────┐
                    │ Executive Architectural Brief &   │
                    │ 1-Click Code Replacement Patches  │
                    └───────────────────────────────────┘
```

### Architectural Comparison Matrix

| Inspection Dimension | Static Analyzers (PMD / ESLint) | Standard LLM Code Reviews | ArchonDX Governance Engine |
| :--- | :--- | :--- | :--- |
| **Distributed $N+1$ Traversal** | ❌ Only flags immediate loop bodies. | ⚠️ Noisy; hallucinates syntax rules. | ✅ **Traces cross-class method invocations** from handlers to selectors. |
| **Data Security & FLS** | ⚠️ Relies on basic regex/rule files. | ⚠️ Misses enterprise user modes. | ✅ **Enforces \`WITH USER_MODE\`**, \`stripInaccessible()\`, and bind vars. |
| **Test Suite Validity** | ❌ Passes any test reaching 75% coverage. | ⚠️ Generates coverage padding. | ✅ **Detects hollow assert-less tests** and verifies 200+ record bulk bounds. |
| **LWC Lifecycle Hygiene** | ⚠️ Checks local variable state only. | ⚠️ Inconsistent Locker/LWS context. | ✅ **Audits LMS cleanup in \`disconnectedCallback()\`** and wire caching. |
| **Workspace Footprint** | Heavy config setup (\`ruleset.xml\`). | Requires custom API keys & billing. | ✅ **Zero-footprint**, runs natively via enterprise Claude sessions. |

---

## ⚡ Quick Installation

ArchonDX runs locally via Claude Code CLI and the official VS Code extension. Install it globally across all your Salesforce repositories in one command:

```bash
curl -fsSL https://github.com/Subhojeet21/archonDX/releases/latest/download/install.sh | bash
```

> **Note:** The installer deploys the compiled, tamper-resistant engine definition directly to the user profile directory. No repository files or build dependencies are added to your target projects.

---

## 💻 Usage

Navigate into **any** Salesforce DX repository on your machine:

### Runtime Target
#### 1. In Claude Code CLI (Terminal)
```bash
claude
/archon
```

To compare against your team's integration branch before raising a PR:
```bash
/archon origin/main
```

#### 2. In VS Code (Claude Code Extension)
1. Open any Salesforce DX workspace in VS Code.
2. In the Claude chat sidebar, type: `/archon`
3. Review the generated executive table and 1-click suggested refactorings.

### When to use?
#### 1. Audit Working Tree Changes (Pre-Commit)
Inspect uncommitted staged and unstaged files:
```text
/archon
```

#### 2. Audit Against Trunk Branch (Pre-PR Gate)
Evaluate your feature branch diff against \`main\` before opening a pull request:
```text
/archon origin/main
```

#### 3. Review Staged Commits Only
```text
/archon --staged
```

---

## 📄 License & Attribution

[MIT License](LICENSE) © Subhojeet Ghosh
