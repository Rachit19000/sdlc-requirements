2
3
Data Ingestion & Iteration: Raw text input is parsed
into structured data, incorporating a continuous
feedback loop from the client for refinement.
Parallel Tracks: The parsed data fuels two
simultaneous paths: the creation of User Stories and
the definition of a Work Breakdown Structure (WBS).
Detailed Specification: User Stories evolve into
Technical Specifications (including Functional and
Non-Functional Requirements), which drive Test Case
Generation.
Converged Planning: The Technical Specs and the
WBS serve as dual inputs into the Sprint Planning
process.
Final Output: Following Sprint Planning and utilizing
generated test cases, the workflow concludes with the
creation of a final Flow Diagram.
4
Logic Flow
5
6
7
8
9
1.  Ingestion & Iterative Parsing 
Raw text is ingested via POST /api/ingest and processed by the Parsing Service.
 A dedicated Feedback Loop allows clients to retrieve (GET) and modify (PUT) parsed data
before artifact generation.
2.  Parallel Artifact Generation
 The system branches into two parallel streams triggering the User Story Service and WBS
Service via distinct endpoints (/generate/user_story & /generate/wbs).
 Includes a secondary modification loop specifically for WBS refinement.
3.  Technical Specification Synthesis
 User Stories are transformed into structured Tech Specs & NFRs via the Tech Spec Service.
 This stage acts as the central data bridge for downstream QA and planning.
4.  Automated Planning & QA 
QA Track: Tech specs drive the Test Case Service to auto-generate validation sheets.
 Planning Track: The Sprint Planning Service merges Tech Specs with the WBS Object to
create a unified Sprint Plan Object.
5.  Visual Output 
The final Sprint Plan is rendered into a visual architecture via the Flow Diagram Service
(POST /generate/flow_diagram).
10
End to End API Data Flow Workflow  diagram
11
12
13
14