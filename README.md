# GitHub Copilot Prompting Guide

*A quick reference for developers using GitHub Copilot in day-to-day development.*

---

## 1. Introduction to Prompting

GitHub Copilot works best when you give it **relevant context**, not just a task.

### Simple formula

> **Good Prompt = Task + Context + Constraints + Expected Output**

- **Task** — What do you want Copilot to do?
- **Context** — What does it need to know about the code/problem?
- **Constraints** — What must it use, avoid, or preserve?
- **Expected Output** — What should Copilot return?

### Example

❌ **Bad**
> Fix this API.

✅ **Good**
> This ASP.NET Core API is slow when `pageSize > 500`. It uses EF Core and currently loads all records before filtering. Preserve the API contract and investigate whether filtering and pagination can happen at the database level. Explain the issue and provide the optimized code.

### Keep prompts efficient

**Don't write longer prompts. Write more relevant prompts.**

- Give Copilot only the context it needs.
- Use existing files/classes/patterns as context where possible.
- Break large tasks into smaller steps.
- Ask follow-up questions instead of restarting.
- Always review, test, and validate generated code.

> **Want ready-to-use examples? Jump directly to [Section 4 – Developer Prompt Examples](#4-developer-prompt-examples).**

---

## 2. Prompting Modes

- **Copilot Chat** — Ask questions, generate code, debug, explain, or refine.
- **Inline suggestions** — Use comments/natural language to guide code generation.
- **Inline Chat** — Ask Copilot to modify selected code.
- **Slash commands** — Useful shortcuts such as `/explain`, `/fix`, `/tests`, `/doc`, and `/optimize` where supported.

---

## 3. Bad vs. Good Prompts

| Use Case | ❌ Bad Prompt | ✅ Good Prompt | Benefit |
|---|---|---|---|
| **Create API** | `Create an API to get users.` | `Create a GET API in ASP.NET Core to retrieve users. Use the existing IUserService, return UserDto, support pagination, use async/await, and follow existing controller patterns.` | Less guessing; better codebase alignment |
| **Fix Bug** | `Fix this code, it's slow.` | `This method takes 8–10 sec for 6,000 Excel rows. We only need EquipmentID and AssetNo. Analyze the bottleneck and optimize it using OpenXML without changing the output.` | Gives problem, scale, technology and goal |
| **Unit Tests** | `Write unit tests for this method.` | `Create xUnit tests covering valid input, boundary values, null/invalid input, dependency failure and exceptions. Follow Arrange/Act/Assert and existing test conventions.` | Better coverage with less rework |
| **Code Review** | `Review this code.` | `Review this C# code for correctness, performance, error handling, security and maintainability. Identify issues by severity and suggest fixes.` | Focused and actionable feedback |
| **Refactoring** | `Refactor this method.` | `Refactor this method for readability while preserving behavior and the public API. Don't introduce unnecessary patterns or change exception behavior.` | Prevents unintended behavior changes |
| **SQL Optimization** | `Optimize this SQL query.` | `Optimize this SQL Server query running against 10M rows. Preserve the results. Check joins, indexes, SARGability and unnecessary scans. Provide the optimized query and index recommendations.` | Performance-focused output |

### What makes the good prompt better?

| Parameter | Bad Prompt | Good Prompt |
|---|---|---|
| Clarity | Low | High |
| Relevant context | Low | High |
| Constraints | Missing | Explicit |
| Expected output | Unclear | Defined |
| Rework required | Higher | Lower |
| Codebase alignment | Uncertain | Guided |

---

## 4. Developer Prompt Examples

Use these as **copy-and-adapt templates** for everyday development.

### 4.1 Understand Existing Code

> Explain this C# class in simple terms. Identify its main responsibility, dependencies, key methods, and the flow of data. Do not suggest changes yet.

### 4.2 Create New Code

> Create a [component/API/service] using [language/framework]. Follow the patterns used in the existing [reference class/file]. Use [required dependency/pattern]. Keep the public interface unchanged and include appropriate error handling.

### 4.3 Debug an Issue

> This code produces [actual result], but the expected result is [expected result]. Identify the root cause first, then provide the smallest fix possible. Do not change unrelated behavior.

### 4.4 Generate Unit Tests

> Generate unit tests for `[method/class]` using [testing framework]. Cover the happy path, boundary conditions, invalid/null input, exceptions, and dependency failures. Follow the existing test naming and Arrange/Act/Assert conventions.

### 4.5 Refactor Code

> Refactor this code to improve readability and maintainability while preserving its current behavior and public API. Avoid unnecessary design patterns or abstractions. Explain the key changes.

### 4.6 Optimize Performance

> Analyze this code for performance bottlenecks. The current operation takes approximately [time] for [data size]. Identify the likely bottlenecks and provide an optimized version without changing the output or business logic.

### 4.7 Optimize SQL

> Optimize this SQL Server query. It runs against approximately [row count] rows and currently takes [time]. Preserve the result set. Check joins, filtering, indexes, SARGability and unnecessary scans. Provide the optimized query and any recommended indexes.

### 4.8 Code Review

> Review this code for correctness, security, performance, error handling and maintainability. List only meaningful issues, assign each a severity (High/Medium/Low), and provide a recommended fix.

### 4.9 Generate Documentation

> Generate concise documentation for this [class/method/API]. Explain its purpose, inputs, outputs, exceptions and important usage considerations. Follow the documentation style already used in this project.

### 4.10 Understand Before Changing

> Before modifying this code, explain how it currently works, identify the relevant dependencies and describe any risks or edge cases. Then suggest the smallest change needed to achieve [requirement].

---

## 5. Quick Do's & Don'ts

### ✅ Do

- Give **relevant context**, not unnecessary information.
- Mention the **language/framework** when it isn't obvious.
- State important **business or technical constraints**.
- Reference existing code/patterns to maintain consistency.
- Ask Copilot to explain complex changes when needed.
- Review and test generated code before committing it.

### ❌ Don't

- Use vague prompts such as `make it better`.
- Expect Copilot to know undocumented business rules.
- Accept generated code without review or testing.
- Include secrets, credentials, customer PII, or other sensitive information in prompts.
- Give Copilot a huge amount of unrelated context.

---

## 6. One-Line Prompt Checklist

Before sending a prompt, ask:

> **Did I clearly state what I want, provide the relevant context, mention important constraints, and explain what output I expect?**

If yes, your prompt is probably good enough.

---

*Prepared as part of the GitHub Copilot pilot team's evaluation materials.*
