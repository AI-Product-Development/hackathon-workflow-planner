# Tech Stack

This document outlines the technology stack chosen for the natural language workflow creation tool MVP, based on the Architecture Guide, Database Design, and API Design Specification.

## Frontend

*   **React:** A JavaScript library for building user interfaces. Chosen for its component-based architecture and declarative programming model.
*   **Tailwind CSS:** A utility-first CSS framework for rapidly building custom designs.
*   **Headless UI or Radix UI (Potential):** Unstyled, accessible UI component libraries that can be used with Tailwind CSS for building common UI elements like dialogs, dropdowns, etc.

## Backend

*   **Python:** The primary programming language for the backend.
*   **FastAPI:** A modern, fast (high-performance) web framework for building APIs with Python 3.7+ based on standard Python type hints.
*   **SQLModel:** A library for interacting with SQL databases, designed to be simple, compatible, and robust. It seamlessly integrates Pydantic and SQLAlchemy.
*   **SQLite:** A C library that implements a small, fast, self-contained, high-reliability, full-featured, SQL database engine. Used for the initial prototype due to its simplicity and file-based nature.
*   **`sqlite+aiosqlite`:** An asynchronous driver for SQLite, enabling asynchronous database operations within FastAPI.
*   **Pydantic:** A library for data validation and settings management using Python type hints. Integrated with FastAPI for request and response data validation and serialization.
*   **JWT Libraries (`python-jose[cryptography]`, `passlib[bcrypt]`):** Libraries used for implementing JSON Web Token-based authentication and password hashing.

## Integrations

*   **MCP Servers:** External services and tools will be integrated using the Model Context Protocol (MCP). The backend will communicate with various MCP servers to execute workflow actions and access resources.

## Deployment & Infrastructure

*   **Vercel (Frontend - Potential):** A platform for frontend frameworks and static sites, offering seamless deployment and scaling.
*   **Heroku or Basic VPS (Backend - Potential):** Potential platforms for deploying the FastAPI backend and hosting the SQLite database file for the prototype.
*   **GitHub Actions:** A CI/CD platform for automating build, test, and deployment pipelines.

This tech stack provides a solid foundation for building the MVP, balancing rapid development with performance and scalability considerations for future growth.
