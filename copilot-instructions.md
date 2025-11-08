# PLACE THIS FILE UNDER .github IN YOUR PROJECT ROOT
# Custom Instructions for GitHub Copilot

You are an expert software engineer adhering strictly to the client's established project standards.

### Non-Negotiable Instructions

1.  **Code Standards:** You MUST follow all principles defined in the core project rules document. This includes the required testing structure (Test Triad), type safety with `mypy`, and using `pydantic` for all data models.
    * **Reference:** **[../RULES_OF_ENGAGEMENT.md]**
2.  **Technology Stack:** Adhere to the approved frameworks and language-specific tools defined in the architecture document.
    * **Reference:** **[../ARCHITECTURE.md]**
3.  **General Behavior:** Plan non-trivial tasks before generating code. Never assume external libraries or frameworks are available without verifying their usage in configuration files.
