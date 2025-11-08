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
