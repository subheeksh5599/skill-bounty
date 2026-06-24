# Solana CPI Safety

> Detect and prevent cross-program invocation vulnerabilities in Solana programs

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](../../LICENSE)
[![Live Demo](https://img.shields.io/badge/live-demo-green)](https://site-seven-ochre-61.vercel.app/chat)

## What it does

A Claude Code skill that detects four classes of CPI vulnerabilities with five runnable proof-of-concept exploits:

| Class | Risk | Detection |
|-------|------|-----------|
| **CPI return-data spoofing** | Critical | Trusting `get_return_data()` without verifying the producing program |
| **Arbitrary CPI** | High | Invoking a caller-supplied program id |
| **Stale account after CPI** | High | Reading account state after CPI without reloading |
| **PDA CPI signing** | Medium-High | Non-canonical bumps or leaked signer seeds |

## Problem it solves

Cross-program invocation is Solana's most common source of critical bugs. Return-data spoofing is the least-documented of the four classes and the hardest to catch in review — any program can write to the return-data slot, enabling oracle price injection and unauthorized control flow.

## Why it fits the bounty

- **Usefulness:** Every Solana program with a CPI needs this audit. Four vulnerability classes, one command.
- **Novelty:** No existing AI skill covers CPI return-data spoofing or arbitrary CPI detection. This is a genuinely new category.
- **Quality:** 5 runnable LiteSVM + TypeScript PoCs across all four classes. Compiled programs committed — runs with Node alone, no toolchain needed.
- **Fit:** Follows the exact solana-game-skill structure. Slots directly into the Solana AI Kit as a submodule.

## Implementation repo

https://github.com/subheeksh5599/solana-cpi-safety

## Live demo

https://site-seven-ochre-61.vercel.app/chat — describes your program's CPI calls and the AI audits it for all four vulnerability classes in real time.

## Structure

```
skill/
  SKILL.md                         # Routing entry point
  cpi-return-data-spoofing.md      # Crown jewel sub-skill
  arbitrary-cpi.md
  account-reload.md
  pda-cpi-signing.md
  poc-harness.md
  cpi-checklist.md
  rules/rust.md

agents/cpi-auditor.md
commands/audit-cpi.md
rules/rust.md
poc/                              # 5 runnable LiteSVM + TypeScript PoCs
  return-data-spoofing/           # 6 test cases (Variant A + B)
  pinocchio-return-data/          # Pinocchio crown-jewel variant
  arbitrary-cpi/
  account-reload/
  pda-cpi-signing/
```

## Commands

| Command | Purpose |
|---------|---------|
| `/audit-cpi` | Checklist-driven CPI safety review across all four vulnerability classes |

## License

MIT
