Correct flow (concise)
1️⃣  User logs in
Frontend → Backend (/auth/github)
Backend → GitHub (redirect)
2️⃣ GitHub authenticates user
User logs in on GitHub
GitHub sends code to backend
3️⃣ Backend completes login
Backend exchanges code → GitHub access token
Backend creates session token
Frontend receives session token
👉 User is now logged into your app

When user uploads a file
4️⃣ Frontend sends upload request
Includes:
File
Repo info
Authorization: Bearer SESSION_TOKEN
5️⃣ Backend authorizes request
Validates session token
Retrieves GitHub access token from TokenStore
6️⃣ Backend processes file
Validates file
Saves it temporarily
Creates a job
Starts async processing
7️⃣ Async agent/service runs
Parses document
Uses GitHub access token
Uploads result to GitHub
Updates job progress
8️⃣ Frontend tracks progress
Uses jobId + SSE

backend-java/src/main/java/com/sdlc/service/McpAgentService.java

This service class handles all communication between Java and the MCP host for executing AI agents.

PART 2: MCP Host (The AI Room)
Step 2.1: MCP receives the box
📍 File: host.py

Step 2.2: MCP finds the robot
📍 File: agent_registry.yaml

Step 2.3: MCP prepares to wake the robot
📍 File: host.py

🧩 Step 2.4: MCP runs the robot
📍 File: host.py

PART 3: AI Agent (The Robot)
Now the robot wakes up 💤➡️🤖
🧩 Step 3.1: Robot reads the message
📍 File: server.py
Now the robot knows:
requirement_text
job_id
Step 3.2: Robot builds its thinking plan
📍 File: server.py
The robot prepares a thinking board:
state = {
  "extracted_text": "...",
  "draft": None,
  "validated": None,
  "error": None,
  "attempts": 0
}

Step 3.3: Robot starts thinking
result = graph.invoke(state)
This starts the LangGraph flow.

PART 4: LangGraph (The Rule Book)
LangGraph is the robot’s instruction book.
🧩 Step 4.1: Generate step (Ask the brain)
📍 File: graph.py
The robot:
Writes a prompt
Asks the big brain (LLM)

Step 4.2: LLM thinks
📍 File: llm.py
The LLM is outside (HuggingFace):
POST https://api-inference.huggingface.co

Step 4.3: Validate step (Check work)
📍 File: graph.py
The robot:
Removes ``` marks
Tries to read JSON
Checks rules

Step 4.4: Decide step
📍 File: graph.py
Robot asks:
Valid? → STOP
Not valid?
Tried < 3 times → TRY AGAIN
Tried 3 times → ❌ FAIL

Step 4.5: Format result
📍 File: server.py

MCP Host Listens
MCP hears robot’s voice :

It reads the JSON and wraps it nicely:
ExecuteResponse(
  status="SUCCESS",
  metadata={...}
)

Java Gets the Answer
Java opens the reply:
mcpResponse.getMetadata()
It finds:
user_stories
Markdown text

Text Parsing
After clicking upload, the file, repoOwner, repoName, your secret login token is sent

Step 2.1: Controller receives the paper
📍 File: RequirementsController.java
  Checks your login token 🔐
  Checks if the file is empty ❌
  Looks at the file name & type

Step 2.2: Java checks file type
Java asks:
“Is this a PDF, DOCX, or TXT?”
If ❌ not allowed:
Unsupported file type

Step 2.3: Java saves file temporarily
Java saves file temporarily
Java puts the file in a temporary drawer 🗄️
Example:- C:\Temp\sdlc_upload_12345_requirements.pdf
Why?
So Java can read it slowly
Without blocking the user

Then Java calls:
parseFile(fileBytes, fileName, mimeType)

Step 4.4: TXT reading
TXT is already text 😊
Java simply does:
new String(fileBytes, UTF_8)

🧹 PART 5: Cleaning the text
🧩 Step 5.1: Clean messy text
Java calls:
cleanText(extractedText)
It:
Fixes line breaks
Removes too many blank lines
Trims spaces
Step 5.2: Validate text exists
Java checks:
“Did I actually read something?

PART 6: Progress update
Frontend receives:
{
  "progress": 50,
  "status": "Text extracted (15672 characters)"
}

  Apache PDFBox 📄 → A Java library that reads PDF files and extracts text from them.
  Apache POI 📘 → A Java library that reads Microsoft Word (DOCX) files and extracts text from them.

backend-java/src/main/java/com/sdlc/service/McpAgentService.java