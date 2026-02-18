# User Stories: File Upload and Processing System

**Total User Stories:** 19
**Estimated Effort:** 32 days

## Sprint Week 1: Foundation

### US1: User logs in
The system should allow a user to log in using GitHub.

**Acceptance Criteria:**
- AC1

**Linked FRs:** FR1

### US2: User uploads a file
The system should allow a user to upload a file.

**Acceptance Criteria:**
- AC2

**Linked FRs:** FR2

### US3: Backend authorizes request
The backend should validate the session token and retrieve the GitHub access token.

**Acceptance Criteria:**
- AC3

**Linked FRs:** FR3

## Sprint Week 2: Processing

### US4: Backend processes file
The backend should validate the file, save it temporarily, create a job, and start async processing.

**Acceptance Criteria:**
- AC2

**Linked FRs:** FR4

### US5: Async agent/service runs
The async agent/service should parse the document, use the GitHub access token, upload the result to GitHub, and update the job progress.

**Acceptance Criteria:**
- AC4

**Linked FRs:** FR5

## Sprint Week 3: Robot Preparation

### US6: Frontend tracks progress
The frontend should track the progress of the file processing using the job ID and Server-Sent Events (SSE).

**Acceptance Criteria:**
- AC5

**Linked FRs:** FR6

### US7: MCP Host receives the box
The MCP host should receive the file and prepare to process it.

**Acceptance Criteria:**
- AC6

**Linked FRs:** FR7

### US8: MCP Host finds the robot
The MCP host should find the AI agent (robot) to process the file.

**Acceptance Criteria:**
- AC7

**Linked FRs:** FR8

### US9: MCP Host prepares to wake the robot
The MCP host should prepare to run the AI agent (robot) to process the file.

**Acceptance Criteria:**
- AC8

**Linked FRs:** FR9

## Sprint Week 4: Final Processing

### US10: MCP Host runs the robot
The MCP host should run the AI agent (robot) to process the file.

**Acceptance Criteria:**
- AC9

**Linked FRs:** FR10

### US11: Robot reads the message
The AI agent (robot) should read the message containing the file details.

**Acceptance Criteria:**
- AC10

**Linked FRs:** FR11

### US12: Robot builds its thinking plan
The AI agent (robot) should prepare a thinking plan to process the file.

**Acceptance Criteria:**
- AC11

**Linked FRs:** FR12

### US13: Robot starts thinking
The AI agent (robot) should start the thinking process using the LangGraph flow.

**Acceptance Criteria:**
- AC12

**Linked FRs:** FR13

### US14: LLM thinks
The Large Language Model (LLM) should think about the processing steps.

**Acceptance Criteria:**
- AC13

**Linked FRs:** FR14

### US15: Validate step
The AI agent (robot) should validate the processing steps.

**Acceptance Criteria:**
- AC14

**Linked FRs:** FR15

### US16: Decide step
The AI agent (robot) should decide whether the processing steps are valid or not.

**Acceptance Criteria:**
- AC15

**Linked FRs:** FR16

### US17: Format result
The AI agent (robot) should format the result of the processing.

**Acceptance Criteria:**
- AC16

**Linked FRs:** FR17

### US18: Clean messy text
The backend should clean the extracted text from the file.

**Acceptance Criteria:**
- AC17

**Linked FRs:** FR18

### US19: Validate text exists
The backend should validate that the text has been successfully extracted from the file.

**Acceptance Criteria:**
- AC18

**Linked FRs:** FR19
