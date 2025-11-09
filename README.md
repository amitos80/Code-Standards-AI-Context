# 🤖 AI-Optimized Project Readme: The Developer's Gateway

Welcome to the project repository. This document serves as the central directory for all project rules and architectural standards. This `README.md` is optimized for quick, directive reference by both human developers and AI assistants.

---

## 🚨 MANDATE: Strict Rule Enforcement

All AI assistants (Gemini, Claude, ChatGPT, Grok, and general Agents) are mandated to **STRICTLY ENFORCE** the vendor-neutral project documents listed below. No task, code generation, or review can proceed without adherence to these files.

* **Project Rules (Mandatory): [./RULES_OF_ENGAGEMENT.md]**
    * This is the core developer pact. It enforces strict limits on file size ($\leq 500$ lines), requires the **Test Triad**, and mandates the use of **`pydantic`** for all data validation.
* **Technology Stacks (Required): [./ARCHITECTURE.md]**
    * The single source of truth for all architectural and technology choices.
* **Common Rules For All Projects: [./COMMON_RULES.md]**
    * Details implementation-specific rules: Full-stack is **React/TypeScript Frontend** and **Express.js/TypeScript Backend**. Includes strict code style and Git workflow constraints.
* **Security Policy: [./SECURITY.md]**
    * Mandatory security rules, including validation of all user inputs on client and server.

---

## ✅ QUALITY & RELIABILITY: Testing Requirements

Every new function, class, or API endpoint must be accompanied by unit tests in the `tests/` directory.

**The Test Triad (Mandatory for every feature):**
1.  A "happy path" test for expected behavior.
2.  An "edge case" test for unusual but valid inputs.
3.  A "failure case" test for expected errors or invalid inputs.

**Frameworks and Conventions:**
* **Unit Testing:** **Vitest** for unit testing.
* **Component Tests:** Testing Library.
* **E2E Tests:** Playwright.
* **Test Files:** Must use `*.test.ts` or `*.spec.ts`.
* **Naming:** Omit "should" from test names (e.g., `it("validates input")`).
* **Assertion Style:** Use `expect(VALUE).toXyz(...)` instead of storing expectations in variables.

---

## ⚙️ DEVELOPMENT WORKFLOW & CONSTRAINTS

### Build & Commands
* Typecheck/Lint: `pnpm check`
* Fix formatting: `pnpm check:fix`
* Run all tests: `pnpm test --run --no-color`
* Build for production: `pnpm build`

### Code Style Constraints
* Maximum file line limit is **200** (supersedes the 500-line architecture rule for `src/` files).
* Use JSDoc docstrings for documenting TypeScript definitions.
* **NEVER** use `@ts-expect-error` or `@ts-ignore` to suppress type errors.

### Git Workflow
* **NEVER** use `git push --force` on the `main` branch.
* **ALWAYS** run `pnpm check` before committing.

---

## 🧠 AI-SPECIFIC MANDATES (RAG & Code Generation)

All AI development related to Retrieval-Augmented Generation (RAG) must follow the specified chunking guidelines.

* **Chunking Strategy Rules: [./CHUNKING.md]**
    * For **Source Code**, split must be based on logical structures: **classes, functions, or methods** to maintain functional context.
    * Always use an **overlap** (e.g., 10-20%) between adjacent chunks to prevent context loss.
* **Code Generation Mandate: [./AGENTS.md]**
    * This is the unified mandate for all AI code generation, review, and refactoring.
    * **Behavioral Mandate:** Agents must always review the rule files before starting a task.

### Specific Assistant Instruction Files
* **Gemini Project Instructions:** **[./GEMINI.md]**
* **Claude Project Instructions:** **[./CLAUDE.md]**
* **ChatGPT Project Instructions:** **[./CHATGPT.md]**
* **GROK Project Instructions:** **[./GROK.md]**

---

## 🤝 CONTRIBUTION

* **Contributing Guide: [./CONTRIBUTING.md]**
    * We welcome **Bug fixes** and **Usability improvements**.
    * New server implementations are **not accepted**.
