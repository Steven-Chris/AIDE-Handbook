# AI-Integrated Development 

Purpose: To empower developers to make the most of AI tools while setting clear boundaries for responsible usage. This guide also provides leadership with the transparency needed to manage, govern, and assess AI adoption effectively.

## Table of Contents

1. [Introduction](#1-introduction)
2. [Core Principles](#2-core-principles)
3. [AI Usage Policies](#3-ai-usage-policies)
4. [Prompt Engineering Guide](#4-prompt-engineering-guide)
5. [Governance and Auditability](#5-governance-and-auditability)
6. [Team Lead Checklist](#6-team-lead-checklist)
7. [FAQ](#7-faq)
8. [Resources](#8-resources)

---

## 1. Introduction

AI tools like GitHub Copilot and ChatGPT are transforming the way developers write, refactor, document, and test code. Used effectively, they can reduce boilerplate, increase development speed, and improve consistency. However, without clear boundaries, they can also introduce risks such as:

* Leakage of sensitive data through prompts
* Over-reliance leading to reduced understanding or poor practices
* Generation of insecure or non-compliant code
* Lack of audit trails and accountability

This guide is the single source of truth to:

* Help developers use AI **responsibly and productively**
* Define **mandatory rules** and **prohibited zones**
* Ensure **disclosure and accountability**
* Provide **leadership visibility** into how and where AI is being used

All developers are expected to adhere to this guide. Team leads are responsible for enforcement. PMs are expected to monitor and report usage patterns.

---

## 2. Core Principles

####   AI is a Tool, Not a Substitute for Expertise

* Developers are ultimately accountable for every line of code they commit.
* AI can suggest code, but **review and understanding** must come from the developer.

####   Maintain Control and Context

* Always know what the AI is doing and why.
* Never accept AI-generated code blindly. Validate its intent and correctness.

####   Prioritize Security and Privacy at Every Step

* Never expose real logs, keys, tokens, or customer data in prompts.
* Sanitize inputs and outputs to preserve compliance.

####   Disclose, Review, and Document

* Transparency is mandatory. Disclose AI assistance explicitly. This is a non-negotiable.
* Human code review is required for every AI-influenced change.

####   Use AI Where It Delivers Real Value

* Ideal use cases: boilerplate generation, test creation, minor refactors, documentation assistance.
* Avoid AI usage in high-risk or highly sensitive areas. See [AI Red Zone](#ai-red-zone-strictly-off-limits-for-prompting-or-ai-assistance).

---

## 3. AI Usage Policies

### Disclosure

All AI-assisted work **must be clearly disclosed**, without exception.

* Include a note in commit messages:

  * `feat: optimized route handler using Copilot (AI)`
* Mention AI use in PR descriptions:

  * “This test suite was generated and edited using ChatGPT (AI).”

### Peer Review Requirement

Any code written or modified with the help of AI **must be reviewed by a human developer** before being merged.

* High-risk changes (auth, payments, DB writes) must be reviewed and tested manually.
* Code cannot bypass CI/CD due to assumed AI correctness.

### AI Red Zone: Strictly Off-Limits 
Areas in code which are strictly off-limits for Prompting or AI Assistance.
**Never use AI to access, analyze, or modify:**

* Authentication and authorization logic
* Payment or billing systems
* Secrets, tokens, config files
* Any database reads/writes involving PII or financial data
* Infrastructure configurations (e.g. Terraform, K8s YAMLs)
* Raw logs or stack traces from production or staging environments

**Violation of this section will be escalated. This is a compliance and security boundary.**

---

## 4. Prompt Engineering Guide

#### General Principles

* Be specific: Describe your intent clearly.
* Add context: Show the function's purpose or file scope.
* Avoid vague language: “Make it better” → “Reduce memory usage”
* Break problems into parts: One prompt, one job.

#### Good vs Bad Prompt Examples

**1. Refactoring Code**

**Bad Prompt:**

```
Make this code better.
```

**Why it's bad:** Too vague. "Better" could mean anything: shorter, faster, cleaner, or more secure?

**Good Prompt:**

```
Refactor this JavaScript function to reduce nesting and improve readability:
function validateUser(input) { ... }
```

**Why it's good:** Specifies goal (reduce nesting) and desired outcome (improved readability).

---

**2. Adding Unit Tests**

**Bad Prompt:**

```
Write tests for this.
```

**Why it's bad:** Doesn’t mention language, framework, or expected edge cases.

**Good Prompt:**

```
Write Jest unit tests for the following Node.js function. Include tests for valid, empty, and malformed input:
function isValidEmail(email) { ... }
```

**Why it's good:** Specifies framework (Jest), scope (Node.js), and test conditions.

---

**3. Explaining Queries**

**Bad Prompt:**

```
Explain this.
```

**Why it's bad:** No context. Doesn’t specify what “this” refers to.

**Good Prompt:**

```
Explain what this SQL query does and suggest indexing strategies to improve performance:
SELECT user_id FROM orders WHERE status = 'cancelled' AND updated_at > NOW() - INTERVAL '30 days';
```

**Why it's good:** Specific, goal-oriented, and performance-focused.

---

**4. Translating Code Between Languages**

**Bad Prompt:**

```
Convert this.
```

**Why it's bad:** Ambiguous and gives the AI no direction.

**Good Prompt:**

```
Convert the following Python function to a TypeScript version using strict typing:
def calculate_total(items): ...
```

**Why it's good:** Clear source and target languages with guidance on typing.

---

**5. Documenting Code**

**Bad Prompt:**

```
Write comments.
```

**Why it's bad:** Lacks context or intent.

**Good Prompt:**

```
Add descriptive inline comments explaining the purpose and flow of this Go HTTP handler:
func handleRequest(w http.ResponseWriter, r *http.Request) { ... }
```

**Why it's good:** Indicates desired depth and context.

---

### Scrubbing Logs and Sensitive Data

**Never dump raw logs or production error outputs into AI prompts.**

#### Manual Redaction Rules

* Redact or replace:

  * Usernames, emails
  * IPs and hostnames
  * API keys, tokens
  * UUIDs
  * PII (e.g. card numbers, addresses)

#### VS Code Regex Find/Replace Cheatsheet

| Pattern Type          | Regex                                     | Replace With          |
| --------------------- | ----------------------------------------- | --------------------- |
| Email Addresses       | `[\w.-]+@[\w.-]+\.[a-zA-Z]{2,}`           | `user@example.com`    |
| IP Addresses          | `\b\d{1,3}(\.\d{1,3}){3}\b`               | `0.0.0.0`             |
| UUIDs                 | `[a-f0-9-]{36}`                           | `REDACTED_UUID`       |
| Tokens                | `"token"\s*:\s*"[^"]+"`                   | `"token": "REDACTED"` |
| Credit Card Numbers   | `\b\d{4}[- ]?\d{4}[- ]?\d{4}[- ]?\d{4}\b` | `REDACTED_CARD`       |
| DB Connection Strings | `postgresql://[^\s"']+`                   | `REDACTED_DB_URL`     |

---

## 5. Governance and Auditability

### PM and Team Lead Oversight

* PMs must monitor GitHub Copilot usage analytics monthly.
* Team leads must:

  * Define AI-free zones (e.g., `// NO_AI_ZONE` or `.noai` files)
  * Audit commits for disclosure and proper peer review
  * Escalate non-compliance when necessary

### Guardrails Enforcement

* Sensitive files must be clearly labeled with comments or annotations.
* Use standardized inline tags for visibility:

  * `// AI-GENERATED:`
  * `// REVIEW REQUIRED:`
  * `// NO_AI_ZONE:`

---

## 6. Team Lead Checklist

* Define and enforce AI-free zones
* Label sensitive files or modules clearly
* Ensure all AI-assisted commits are peer-reviewed
* Monitor team Copilot usage analytics
* Handle policy violations in alignment with infosec/compliance

---

## 7. FAQ

**Q: Can I use AI to generate unit tests?**
A: Yes, but you must review logic, edge cases, and coverage. Treat the AI output as a first draft.

**Q: Can I use AI to write documentation?**
A: Yes, for API docs, README templates, and inline comments. However, verify accuracy.

**Q: Can I paste raw logs into AI to debug?**
A: No. Logs must be scrubbed of all sensitive data and reduced to the minimal, relevant context.

**Q: Can AI help refactor critical or legacy code?**
A: Yes, with caution. Peer review and testing are mandatory.

**Q: Can AI be used to optimize performance?**
A: Yes, especially in loop optimizations or SQL queries, but always benchmark and verify. Never run AI generated SQL queries in production.

**Q: Is it okay to train AI on our proprietary codebase?**
A: No. That is out of scope for this document and requires legal review and explicit authorization.

**Q: Can AI generate code for auth, payments, or DB writes?**
A: No. These fall under the [AI Red Zone](#ai-red-zone-strictly-off-limits-for-prompting-or-ai-assistance).

**Q: Can AI be used to write migrations, Terraform configs, or infrastructure code?**
A: Not without peer review and redaction. Secrets, variables, and URLs must be handled manually.

**Q: What if I used AI but forgot to disclose it?**
A: Edit the commit/PR and notify your reviewer. Repeated lapses will be escalated.

**Q: Can I create prompt files or example prompts in the repo?**
A: No. Prompt examples live only in this document. Repos must not store AI prompts.

---

## 8. Resources

* [GitHub Copilot Documentation](https://docs.github.com/copilot)
* [OpenAI Prompting Guide](https://platform.openai.com/docs/guides/prompt-engineering)
* Internal training and onboarding material (TBD)

---

**Version**: 1.0.0
**Last Updated**: July 2025
