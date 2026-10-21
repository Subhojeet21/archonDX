# ArchonDX (⚡)
> **Autonomous Multi-Tenant Architecture & AI-Code Governance Engine for Salesforce DX**  
> **Innovator & Lead Architect:** Subhojeet Ghosh (Principal Software Engineer & Salesforce Architect)

![License](https://img.shields.io/badge/License-MIT-blue.svg)
![Version](https://img.shields.io/badge/Version-1.0.0-emerald.svg)
![Runtime](https://img.shields.io/badge/Platform-Claude_Code_CLI_%7C_VS_Code-purple.svg)
![Governance](https://img.shields.io/badge/Governance-Governor_Boundaries_%7C_FLS_%7C_Synthetic_Code-critical.svg)

---

## 🏛️ Executive Summary

Modern enterprise engineering teams face a growing dilemma: **AI coding assistants increase raw velocity, but disproportionately increase the architectural review burden.** 

Senior architects spend up to 30% of their sprints checking for subtle multi-tenant issues like distributed $N+1$ SOQL queries, unasserted "coverage-padding" test classes, and data leakage across transaction boundaries.

**ArchonDX** is an autonomous governance engine created by **Subhojeet Ghosh**. Operating directly within Claude Code (CLI and VS Code), ArchonDX performs semantic, cross-file architectural audits on Apex and Lightning Web Components before code ever reaches a pull request.

---

## 🚀 Key Architectural Capabilities

| Inspection Area | Traditional Linters (PMD / ESLint) | ArchonDX Governance Engine |
| :--- | :--- | :--- |
| **Governor Limit Defense** | Flags direct SOQL inside immediate loops. | Detects **distributed $N+1$ calls** across trigger handlers, services, and selector tiers. |
| **Data Access & Security** | Checks basic rule files. | Enforces **explicit sharing** and runtime `WITH USER_MODE` / `Security.stripInaccessible()` integrity. |
| **AI Slop & Coverage Padding** | Counts line coverage (passes hollow tests). | Flags **assert-less unit tests**, verifies 200+ record bulkification, and catches hallucinated API methods. |
| **LWC Lifecycle Hygiene** | Evaluates local syntax only. | Verifies reactive memory cleanup in `disconnectedCallback()` and audits wire caching constraints. |

---

## ⚡ 1-Line Quick Installation

To install ArchonDX globally on your machine (works across all Salesforce repositories):

```bash
curl -fsSL https://raw.githubusercontent.com/Subhojeet21/archonDX-public/main/install.sh | bash
```

---

## 💻 Usage

Navigate into **any** Salesforce DX repository on your machine:

### 1. In Claude Code CLI (Terminal)
```bash
claude
/archon
```

To compare against your team's integration branch before raising a PR:
```bash
/archon origin/main
```

### 2. In VS Code (Claude Code Extension)
1. Open any Salesforce DX workspace in VS Code.
2. In the Claude chat sidebar, type: `/archon`
3. Review the generated executive table and 1-click suggested refactorings.

---

## 📄 License & Attribution

Designed, architected, and innovated by **Subhojeet Ghosh**. Distributed under the MIT License with mandatory author attribution notices preserved in all build artifacts and execution headers.
