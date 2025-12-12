# 🧠 Code Review Assistant (LangGraph)

An **agentic code-review workflow** built using **LangGraph** that automatically reviews real GitHub Pull Requests and routes them through the correct decision path: **auto-approve**, **request fixes**, or **escalate to a senior engineer**.

This project demonstrates how to build **stateful, decision-driven LLM workflows** that operate on real engineering artifacts instead of static prompts.

---

## ✨ What This Project Does

Given a real Pull Request, the system:

1. **Analyzes the PR context** (diff, title, description, files changed, CI status)
2. **Categorizes the type of change**
3. **Assesses risk level**
4. **Routes the PR** to one of:
   - ✅ Auto-approval
   - 🛠️ Requesting fixes from the author
   - ⚠️ Escalation to a senior engineer with full context

All decisions are orchestrated using **LangGraph nodes and conditional edges**.

---

## 🏗️ Workflow Overview

### Nodes in the Graph

1. **Categorize Change**
   - Determines whether the PR is a `Bugfix`, `Feature`, `Refactor`, `Config`, or `Test`

2. **Assess Risk**
   - Evaluates impact based on:
     - Change category
     - Files touched
     - Diff size
     - CI status

3. **Auto-Approve**
   - For low-risk, well-scoped changes
   - Generates an approval response

4. **Request Fixes**
   - For medium-risk PRs
   - Produces actionable review feedback

5. **Escalate to Senior Engineer**
   - For high-risk or sensitive changes
   - Generates a structured escalation summary

---

## 🧠 State Model (Core Concept)

The LangGraph operates on a structured state, not raw prompts.

Key inputs include:
- PR diff (fetched from GitHub)
- PR title and description
- Files changed
- CI status

This grounding removes “hallucinated” decisions and makes outcomes explainab
