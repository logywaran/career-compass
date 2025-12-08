Career Compass – AI Job Match & Career Assistant

Career Compass is a hybrid AI + Rule-Engine career guidance application designed for students and early professionals to analyze their job readiness using a resume and a job description.

Unlike typical AI tools that rely solely on LLM outputs, Career Compass deliberately separates responsibilities:

• Skill extraction & scoring → Deterministic Java Rule Engine (accurate and explainable)
• Natural language insights & chatbot → AI (LLM via Ollama) controlled by strict prompts
• Career guidance grounding → RAG using curated knowledge snippets

This design guarantees consistent scoring, realistic career advice, and prevents hallucinated skill claims from the AI.



🚀 SETUP & EXECUTION 

Follow these steps exactly to run the application locally.

✅ Prerequisites

Install the following:

• Java 17+
• Maven 3.8+
• Ollama (local LLM runtime)
• Git


✅ Step 1 — Clone Repository

Clone the repository and move into the project directory:

git clone <YOUR_GITHUB_REPO_URL>
cd career-compass

✅ Step 2 — Install & Pull LLM Model (Ollama)

Install Ollama:

https://ollama.com/download

Pull the required AI model:

ollama pull gemma3:1b

Verify installation:

ollama list

Confirm you see:

gemma3:1b

✅ Step 3 — Start Ollama Server

Start Ollama:

ollama serve

Ollama runs locally on:

http://localhost:11434

You can verify it is active by opening the URL above.

✅ Step 4 — Run Spring Boot Backend

From the project root directory:

mvn spring-boot:run

Backend will start on:

http://localhost:8081

✅ Step 5 — Open the Frontend (Static HTML)

The frontend is served directly from Spring Boot’s static folder — no separate frontend server is required.

Open these URLs in your browser:

Home
http://localhost:8081/home.html

Resume Input
http://localhost:8081/resume.html

Job Description Input
http://localhost:8081/job.html

Results Page
http://localhost:8081/results.html

AI Career Assistant (Chatbot)
http://localhost:8081/chatbot.html

✅ Step 6 — Application Workflow

1️⃣ Paste or upload your resume on the Resume page
2️⃣ Paste the job description on the Job page
3️⃣ Click Analyze on the Results page

The system performs:

✅ Skill extraction
✅ Resume vs JD matching
✅ Deterministic score calculation
✅ Gap analysis
✅ AI tip generation

The results page displays:

• Overall match score
• Matched skills
• Missing skills
• Actionable resume improvement tip

✅ Step 7 — Career Chatbot

Open:

http://localhost:8081/chatbot.html

Ask questions such as:

• “What skills should I learn next?”
• “Am I ready for frontend development?”
• “How can I improve my resume?”

The chatbot responses are generated using:

✅ Verified skill-context only
✅ RAG career knowledge base snippets
✅ Strict rule-based prompt constraints

This prevents hallucinated advice and keeps guidance realistic and job-focused.

⚙️ SYSTEM ARCHITECTURE

Career Compass uses a Hybrid AI + Rule-Engine Model:

Resume + Job Description
↓
Spring Boot Parsing Layer
↓
Java Rule Engine (Single Source of Truth)
↓
Verified Skill Lists + Match Score
↓
AI Layer (LLM via Ollama)
↓
Insights • Tips • Chatbot Answers

🔹 Core Design Rules

• Java rule engine controls all skill matching and scoring logic
• AI NEVER decides skills or score
• AI derives responses strictly from verified backend data

🧠 AI & RAG DESIGN
✅ Skill Safety Rules

AI may claim the user has a skill ONLY if it exists in:

• resumeSkills
• matchedSkills

Skills appearing only in missingSkills are ALWAYS treated as learning gaps.

✅ RAG (Retrieval-Augmented Generation)

Career guidance snippets are stored in:

CareerKnowledgeBase.java

Snippets are retrieved based on:

• Missing skills
• Role focus (backend, frontend, data, etc.)
• Keywords from the user’s chatbot question

Retrieved snippets are injected into AI prompts to ensure:

✅ Grounded advice
✅ Practical learning guidance
✅ Domain-specific roadmaps


⚙️ TECH STACK

Backend
• Java 17
• Spring Boot REST API
• Maven

AI & RAG
• Ollama local runtime
• Gemma 3 (1B) LLM
• Prompt-constrained AI output validation
• Custom lightweight Retrieval-Augmented Generation (CareerKnowledgeBase)

Frontend
• HTML
• CSS
• Vanilla JavaScript

Data & Storage
• In-memory session storage (browser + backend)
• No database used (POC design)

Tools & Runtime
• PDFBox (PDF resume text extraction)
• REST APIs (JSON communication)
• Git version control

🔨 MAJOR FEATURES

✅ Resume vs JD skill matching
✅ Deterministic match scoring (0–100)
✅ Clear gap explanation
✅ Personalized resume improvement tips
✅ Career chatbot with strict skill verification + RAG grounding
✅ Fallback logic + validation layer preventing hallucinations

📁 CORE BACKEND FILES

AiService.java – AI prompts, RAG injection, hallucination safeguards
MatchService.java – Rule engine skill matching & deterministic scoring
CareerKnowledgeBase.java – RAG knowledge snippet store
AnalysisRequest.java – Resume + JD input DTO
AnalysisResponse.java – Skill profile and scoring results DTO
AiSkillProfile.java – Structured parsing model for AI extraction

🌐 FRONTEND FILES

home.html – Landing page
resume.html – Resume input
job.html – Job description input
results.html – Skill score and analysis report UI
chatbot.html – RAG-based career assistant

Frontend built using:

HTML • CSS • Vanilla JavaScript
All pages communicate via REST APIs with the backend.

🧪 API ENDPOINTS

/api/analyze
→ Performs resume vs job skill analysis and match scoring

/api/ask
→ Processes chatbot career questions using RAG + AI prompts

⚠️ CHALLENGES SOLVED
1. AI Skill Hallucination

AI previously invented skills implied by the JD
✅ Solved using verified-data-only prompts

2. Inconsistent AI Scoring

Pure LLM scoring produced unstable results
✅ Solved by replacing scoring entirely with Java rule-engine

3. Generic Career Advice

Early chatbot answers lacked depth
✅ Solved using RAG career knowledge grounding

4. LLM Over-Verbosity

Initial chatbot tone was chatty and repetitive
✅ Minimized using strict formatting and response style constraints

⚠️ CURRENT LIMITATIONS

• Local-only AI inference via Ollama
• Session storage used instead of database persistence
• No PDF resume extraction (text input only)
• Chatbot tone tuning still ongoing
• Single LLM provider only

✅ FUTURE ENHANCEMENTS

• Cloud LLM integration (Gemini / OpenAI)
• Persistent user accounts and profiles
• PDF resume ingestion and semantic parsing
• UI redesign & animations
• Multi-job tracking dashboards
