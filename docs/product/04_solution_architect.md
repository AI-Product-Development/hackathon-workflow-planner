# Architecture Guide

## 1. Selected Architecture Pattern:
**Pattern:** Layered Architecture

**Justification:** A layered architecture provides a clear separation of concerns, making the initial prototype easier to develop, understand, and maintain. It allows for logical grouping of functionalities (presentation, application logic, data access) and provides a solid foundation for potential future evolution towards a more distributed pattern if scalability demands increase significantly.

## 2. State Management:
**Frontend State:** React Hooks and Context API will be used for managing local component state and sharing state across components without prop drilling. For more complex global state management, a library like Zustand or Recoil could be introduced later if needed, but for the initial prototype, Hooks and Context should suffice.
**Backend State:** Backend state will be managed within the FastAPI application. Database transactions and ORM (SQLModel) will handle persistent state. In-memory caching or a dedicated caching layer (like Redis) can be considered for performance optimization if bottlenecks are identified.

## 3. Technical Stack:
**Frontend:**
*   Framework: React
*   UI Libraries: Tailwind CSS for styling, potentially a component library like Headless UI or Radix UI for unstyled, accessible components.
*   Component Strategy: Atomic Design principles will be followed to structure components into atoms, molecules, organisms, templates, and pages.
**Backend:**
*   Language/Framework: Python/FastAPI
*   Database (Initial Prototype): SQLite
*   ORM: SQLModel
*   Caching layers: None initially, will be added if performance requires.
**Authentication:** JWT (JSON Web Tokens) for stateless authentication. A simple username/password or email/password flow for the initial prototype.
**Payments (if applicable): Not applicable for the initial prototype.**
**Key Integrations:** Integration with external services will be handled via MCP servers.

## 4. Authentication & Authorization Flow:
User registration will involve providing necessary credentials. Upon successful login, a JWT will be issued by the backend and stored securely on the frontend (e.g., in HttpOnly cookies). This token will be sent with subsequent requests to authenticate the user. Authorization will be handled using middleware in FastAPI, checking the validity of the JWT and potentially user roles for access control (RBAC will be considered for future phases if different permission levels are required). Token expiration and refresh mechanisms will be implemented.

## 5. High-Level Route Design:
**Frontend Routes/Pages:**
*   `/`: Homepage with workflow input and builder.
*   `/workflows`: List of saved workflows.
*   `/workflows/:id`: Detail view and editor for a specific workflow.
*   `/integrations`: Manage connected services.
*   `/settings`: User settings.
*   `/login`, `/register`.
**Major Backend API Endpoint Categories:**
*   `/auth`: User registration, login, token refresh.
*   `/workflows`: Create, read, update, delete workflows.
*   `/parse`: Natural language parsing and step extraction.
*   `/execute`: Trigger workflow execution.
*   `/integrations`: Manage MCP server connections.
*   `/testing`: Workflow testing and debugging endpoints.

## 6. API Design Philosophy:
**Core Principles:** RESTful principles will be followed for API design, using standard HTTP methods (GET, POST, PUT, DELETE) and status codes.
**Versioning:** API versioning will be implemented from the start (e.g., `/api/v1/...`) to allow for future changes without breaking existing clients.
**Error Handling:** Standardized JSON error responses will be used, providing clear error codes and messages.

## 7. Database Design Overview:**
**Chosen Database Type:** SQLite (Initial Prototype)
**Key Data Models/Entities:**
*   `User`: Stores user information.
*   `Workflow`: Stores workflow definitions (including natural language description, structured steps, and configuration).
*   `Integration`: Stores information about connected MCP servers and their configurations.
*   `WorkflowRun`: Logs of workflow executions.
(Detailed schema will be defined by the Data Architect using SQLModel).

## 8. Deployment & Infrastructure Overview:**
**Target Hosting Environment:** Vercel for the frontend (if a separate frontend is deployed), and a cloud platform like Heroku or a basic VPS for the backend and database for the initial prototype.
**CI/CD Approach:** Basic CI/CD pipelines will be set up using platforms like GitHub Actions to automate testing and deployment upon code commits.

## Architecture Diagram (High-Level)

```mermaid
graph TD
    A[User] -->|Interacts with| B[Frontend (React)]
    B -->|API Calls| C[Backend (FastAPI)]
    C -->|ORM (SQLModel)| D[Database (SQLite)]
    C -->|Communicates with| E[MCP Servers (Integrations)]
