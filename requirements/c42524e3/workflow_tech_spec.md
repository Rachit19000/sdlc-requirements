# Technical Specification

## 1. System Overview

**Project Name:** File Upload and Processing System

**Description:** A system that allows users to upload files, authenticate via GitHub, and process the files using an AI agent.

**Architecture Pattern:** Microservices

### Key Design Decisions

- Use GitHub OAuth for authentication
- Implement asynchronous processing for file uploads
- Utilize LangGraph for AI processing

## 2. Data Model

### Entity: User

| Field | Type | Description |
|-------|------|-------------|
| id | UUID | Unique identifier for the user |
| github_access_token | String | GitHub access token for the user |
| session_token | String | Session token for the user's current session |

**Relationships:** One-to-Many with Job

### Entity: Job

| Field | Type | Description |
|-------|------|-------------|
| id | UUID | Unique identifier for the job |
| user_id | UUID | Foreign key to the User entity |
| status | String | Current status of the job (e.g., pending, processing, completed) |
| progress | Integer | Percentage of job completion |

**Relationships:** One-to-One with File

### Entity: File

| Field | Type | Description |
|-------|------|-------------|
| id | UUID | Unique identifier for the file |
| job_id | UUID | Foreign key to the Job entity |
| file_path | String | Path to the temporary file on the server |
| file_type | String | Type of the file (e.g., PDF, DOCX, TXT) |

**Relationships:** One-to-One with User

## 3. API Design

| Method | Path | Description |
|--------|------|-------------|
| POST | `/auth/github` | User logs in using GitHub |
| POST | `/file/upload` | User uploads a file |
| GET | `/job/{job_id}` | Frontend tracks progress of the file processing |

### POST `/auth/github`

User logs in using GitHub

**Request Body:** github_code: String

**Response Body:** session_token: String

### POST `/file/upload`

User uploads a file

**Request Body:** file: File, repo_info: Object, authorization: Bearer SESSION_TOKEN

**Response Body:** job_id: UUID

### GET `/job/{job_id}`

Frontend tracks progress of the file processing

**Response Body:** progress: Integer, status: String

## 4. Component Breakdown

### AuthenticationService

**Responsibility:** Handles user authentication and session management

**Depends on:** UserRepository

### FileService

**Responsibility:** Handles file uploads, validation, and temporary storage

**Depends on:** JobService, UserRepository

### JobService

**Responsibility:** Manages job creation, status updates, and progress tracking

**Depends on:** FileService, McpAgentService

### McpAgentService

**Responsibility:** Handles communication with the MCP host for AI processing

**Depends on:** AgentRegistry, LangGraphService

### LangGraphService

**Responsibility:** Manages the execution of AI processing steps

**Depends on:** McpAgentService

## 5. Non-Functional Requirements

- **Performance:** API endpoints should respond within 2 seconds under normal load
- **Security:** Implement OAuth2 for authentication, use HTTPS, and encrypt sensitive data
- **Scalability:** Design for horizontal scalability by using load balancers and auto-scaling groups
- **Availability:** Ensure 99.9% uptime with redundant systems and failover mechanisms

## 6. Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | React |
| Backend | Java Spring Boot |
| Database | PostgreSQL |
| Infrastructure | AWS |

## 7. Risks & Mitigations

| Risk | Impact | Mitigation |
|------|--------|------------|
| OAuth2 token expiration | User sessions may be interrupted | Implement token refresh mechanisms and use short-lived tokens |
| AI processing failures | File processing may fail | Implement retries and fallback mechanisms for AI processing steps |

## 8. Open Questions

- What is the exact format of the 'repo_info' object?
- How should we handle large files (>100MB)?
- What are the specific requirements for the 'LangGraphService'?
