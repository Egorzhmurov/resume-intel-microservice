# AI Smart CV Matcher

An internal tool for HR departments to evaluate candidate resumes. It allows users to upload a candidate's resume text, set strict filters (job requirements), and automatically receive a structured verdict from the neural network on how well the candidate fits the position.

## Business Objective
Initial screening takes up to 70% of HR specialists' time. The goal of this service is to automate the routine:
1. HR pastes the resume text and specifies filters (e.g., "Middle, React, Node.js, B2 English, 3+ years experience").
2. The system processes the data through an LLM in strict JSON mode.
3. The output is a clear dashboard: Match Score, identified skills, and "red flags" (missing qualifications).

## Tech Stack
The project is implemented in a Fullstack format (client-server architecture) using npm workspaces:
* **Backend:** Node.js, Express, TypeScript
* **Frontend:** React, TypeScript, Bootstrap (for fast and strict UI layout), Vite
* **AI/LLM:** Google Gemini API / OpenAI API (Structured Outputs)
* **Validation:** Zod (on the backend)

## Core Features (MVP)

### Backend (API)
* `POST /api/matches` 
  - **Body:** `{ "resumeText": "...", "filters": { "level": "mid", "mandatorySkills": ["React", "Node.js"] } }`
  - **Response (Strict JSON):** Returns match score, matched skills, missing skills, red flags, and a final verdict. Validated by Zod before being sent to the client.

### Frontend (UI)
* **Main Screen:** A text area for pasting the resume and a section with checkboxes/inputs for configuring filters.
* **Results Screen:** A dashboard showing the Match Score and cards/lists displaying the candidate's strengths and weaknesses.

## Implementation Requirements (Definition of Done)
- The API validates requests and returns actionable 400 errors for invalid data.
- The LLM integration uses a system prompt that forces strictly typed JSON output without Markdown wrappers or extra text.
- Form submission from the frontend waits for the LLM response and renders the result cleanly.
- Loading states (spinners) and errors (if the AI API fails or returns invalid JSON) are properly handled on the frontend.
- Provider credentials (API keys) are kept strictly on the backend and never exposed to the client.

## Development Setup

The project uses npm workspaces to manage both frontend and backend dependencies from the root directory.

### Prerequisites
- Node.js installed
- API key for OpenAI or Google Gemini

### Installation
1. Clone the repository and navigate to the root folder:
```bash
git clone [repository-url]
cd [repository-folder]
