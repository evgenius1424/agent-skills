---
name: audit
description: "Read-only repository audit: inventory consequential structure, judge each WHY, assess AX (agent experience), and rank recommendations. Use for architecture audits, unnecessary-abstraction hunts, codebase health or AX reviews, or planning a simplification."
---

# Audit

The audit pass is read-only. Write report files only where the user points, or to a scratch location. If the request also authorizes improvements, finish the findings and then apply the in-scope ones through the appropriate playbook. Otherwise report recommendations without changing the subject repository.

## 1. Baseline

Record the commit, the repo's own check commands (see `verify`), and whether they pass right now. A finding about behavior is only as strong as this baseline.

## 2. Sweep

Unlike other work, an audit sweeps systematically. Map the deep modules: what each one owns, its interface, and who calls it. Read the instruction docs, `GLOSSARY.md`, `docs/adr/`, and the canonical examples agents are likely to copy.

When `improve-codebase-architecture` is installed, hand it the search for deepening candidates and fold its candidates into step 3. Otherwise, look for shallow modules (interface about as complex as the body), pass-through layers, interfaces with one implementation, and features spread across many modules.

## 3. Inventory

Write a WHY block for each consequential structure, using `why`. Keep the evidence labels honest: an audit usually sees behavior and rarely intent. Where the WHY can't be found, the verdict is INVESTIGATE, not REMOVE.

## 4. AX

Treat the repo as a prompt and ask:

- Can an agent find the owning module for a typical change from names alone?
- Which canonical examples would teach a wrong pattern if copied?
- Which invariants exist only in people's heads, with no test, type or name expressing them?
- Which domain terms are ambiguous, so `GLOSSARY.md` should define them?

## 5. Rank

Order findings by (risk reduced or reasoning saved) ÷ (change risk). For each finding, give the evidence (file:line, command output), the verdict, the smallest next step, and how to verify that step.

## Done when

Every consequential structure you swept has a verdict, every claim has evidence that can be reproduced, and the audit pass added no subject changes. Preserve any pre-existing diff.
