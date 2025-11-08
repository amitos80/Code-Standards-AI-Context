# 🚀 Project Name: Full-Stack Todo List

This repository contains the source code for a simple, full-stack Todo List application, built to serve as the initial implementation using our standard technology architecture.

## 🎯 Overview

The goal of this project is to demonstrate the core architectural patterns defined in our documentation (`ARCHITECTURE.md` and `GEMINI.md`) by implementing basic CRUD functionality for a task management application.

### Key Features
* **Task Management:** Create, view, and mark tasks as complete.
* **Type Safety:** End-to-end type safety enforced by TypeScript (Frontend) and Pydantic/Type Hints (Backend).
* **Component-Based UI:** Built with Next.js and styled with Tailwind CSS.

## 🏛️ Technology Stack

| Layer | Technology | Key Components |
| :--- | :--- | :--- |
| **Frontend** | **Next.js (App Router)** | TypeScript, React, Zustand (State), Tailwind CSS (Styling) |
| **Backend** | **Python** | FastAPI, Pydantic (Data Models), Uvicorn (Server) |
| **Database** | **SQLite** | Used for local development; intended for PostgreSQL in production. |

---

## ⚙️ Local Development Setup

Follow these steps to get the application running on your local machine.

### Prerequisites

* Node.js (LTS version)
* Python 3.10+
* Poetry (for Python dependency management)

### 1. Backend Setup

The backend service runs a FastAPI server responsible for the `/api/v1/tasks` endpoint.

```bash
# Navigate to the backend directory
cd backend

# Install Python dependencies using Poetry
poetry install

# Run the API server with live reload
poetry run uvicorn src.main:app --reload


## 🤖 AI Context & Project Standards (`.md` Files)

This repository, **`Code-Standards-AI-Context`**, employs a scalable, **vendor-neutral, file-based approach** to manage project standards for both human developers and multiple AI assistants (Gemini, Copilot, Claude, ChatGPT, etc.).

By using dedicated Markdown files as context pointers, we ensure all Large Language Models (LLMs) operate from a single, consistent set of rules regarding code quality, style, and architecture. This minimizes errors, enforces consistency, and prevents agents from defaulting to generic online standards.

***

### 🏛️ The Single Source of Truth

All core, non-negotiable policies are centralized into one document. This prevents policy fragmentation and ensures you only have one file to update when project standards evolve:

* **`RULES_OF_ENGAGEMENT.md`**: **The Master Policy Document.** This file contains the foundational standards for **Code Quality**, the mandatory **Test Triad** methodology, modularity rules, and technology-agnostic requirements (e.g., all data models must use `pydantic`).
* **`ARCHITECTURE.md`**: Contains all approved **Technology Stacks** and architectural patterns (e.g., Next.js vs. Vite, Python FastAPI backend, cloud-native library choices).

***

### 🔗 Agent-Specific Context Pointers

To maximize the chance that a specific AI assistant reads the correct context, we use lightweight, convention-specific pointer files. These files are brief and serve only to direct the LLM to the central policy and architecture documents.

| AI Assistant | File Path | Rationale & Purpose |
| :--- | :--- | :--- |
| **GitHub Copilot** | `.github/copilot-instructions.md` | **The official, mandatory file path** Copilot automatically includes in its chat context for project-wide instructions. |
| **All Agents (Generic)** | `AGENTS.md` | A widely recognized, multi-agent file standard often ingested by general-purpose code agents. |
| **Google Gemini** | `GEMINI.md` | Explicitly provides system context for the Gemini family of models. |
| **Anthropic Claude** | `CLAUDE.md` | Claude often prioritizes instructions found in a namesake file to define its operational scope. |
| **OpenAI (ChatGPT/Codex)** | `CHATGPT.md` | Used in projects where the tool or chat can be manually pointed to a file for initial system context. |

This file structure makes your policy management resilient and efficient: an agent reads its namesake file, is immediately redirected to the **`RULES_OF_ENGAGEMENT.md`**, and begins coding according to your standards.

***

### 📚 Further Reading on Context Management

For more information on why and how these file conventions work:

* **GitHub Copilot Instructions:** Learn how Copilot automatically reads and incorporates the `.github/copilot-instructions.md` file.
    * [Adding repository custom instructions for GitHub Copilot](https://docs.github.com/copilot/customizing-copilot/adding-custom-instructions-for-github-copilot)
* **Agent Instructions Standard:** Understanding the use of `AGENTS.md` as a generic standard for LLM-based developer tools.
    * [Custom instructions with AGENTS.md (OpenAI Developer Documentation)](https://developers.openai.com/codex/guides/agents-md)
* **LLM Prompting & Context:** Principles for effectively structuring long-context prompts for coding agents to prevent information loss.
    * [Grok-code-fast-1 Prompt Guide: Supply Context Intelligently (CometAPI)](https://www.cometapi.com/grok-code-fast-1-prompt-guide/)
