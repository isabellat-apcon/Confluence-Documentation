# Engineering Workflow Overview

## Purpose

We need a consistent way for engineers to work in GitHub, document decisions, and understand how changes move through our projects.

The goal is to reduce confusion, avoid everyone creating their own process, and make it easier to scale across multiple projects.

---

## Recommended System

We should use four simple tools:

| Tool                 | Purpose                                    |
| -------------------- | ------------------------------------------ |
| Pull Request         | How code changes are reviewed and merged   |
| RFC                  | How major ideas or changes are proposed    |
| ADR                  | How final technical decisions are recorded |
| Engineering Handbook | Where team standards and processes live    |

---

## 1. Pull Requests

Pull Requests should be used for normal code changes.

This includes bug fixes, features, refactors, documentation updates, and maintenance work.

Basic workflow:

```text
Issue → Branch → Pull Request → Review → Merge
```

A Pull Request should answer:

```text
What changed?
Why did it change?
How was it tested?
```

This keeps code changes visible, reviewed, and consistent.

---

## 2. RFCs

RFC stands for Request for Comments.

An RFC is used before making a major technical or process decision.

Use an RFC when the change affects multiple projects, architecture, infrastructure, security, or long-term team standards.

RFCs help the team discuss options before committing to a direction.

A simple RFC should explain:

```text
What problem are we solving?
What is the proposed solution?
What are the risks or tradeoffs?
What decision are we making?
```

---

## 3. ADRs

ADR stands for Architecture Decision Record.

An ADR records an important decision after it has been made.

The purpose is to help future engineers understand why we chose a certain approach.

An ADR should explain:

```text
What decision was made?
Why was it made?
What tradeoffs were considered?
```

RFCs help us discuss decisions.
ADRs help us remember decisions.

---

## 4. Engineering Handbook

The Engineering Handbook is the team’s source of truth for how we work.

It should include things like:

```text
GitHub workflow
Branch naming
Pull Request expectations
Review rules
RFC process
ADR process
Documentation standards
Release process
```

This gives engineers one place to look instead of relying on tribal knowledge.

---

## Simple Rule of Thumb

```text
Changing code? Use a Pull Request.
Proposing a big change? Use an RFC.
Recording a decision? Use an ADR.
Documenting team standards? Use the Engineering Handbook.
```

---
