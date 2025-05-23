# AI Math Chatbot Development Roadmap

This document outlines the tasks required to build the AI Math Chatbot based on the provided Product Requirements Document (AI-MATH-CHATBOT-PRD.md) and the Gemini API Documentation (gemini_api_doc.md).

## 1. Project Setup & Infrastructure

- [x] Initialize Backend project (Python/FastAPI).
- [x] Initialize Frontend project (React with TypeScript).
- [x] Set up basic project structure and dependencies (`google-genai`, `python-docx`, FastAPI, Uvicorn, SQLite driver, React, TypeScript, Tailwind CSS, Zustand, KaTeX, react-speech-recognition).
- [x] Configure environment variables for API keys (Gemini, Whisper) and backend settings.
- [x] Set up Dockerfile and Docker Compose for frontend and backend.

## 2. Frontend Development

### 2.1 Core Chat UI Layout & Structure

- [x] Implement the main container layout spanning the full viewport.
- [x] Implement the static header bar (Chatbot Title, Theme Toggle, Litter Bin icon).
- [x] Implement the conversation view scrollable area.
- [x] Implement the **initial state**: Display a welcome message ("Ask me anything about math!").
- [x] Implement the **initial positioning** of the input area: Centered horizontally and vertically in the viewport *before* the first message is sent.
- [x] Implement the **transition logic**: Move the input area to be fixed at the bottom center of the chat area *after* the first user message is sent or AI response is received.
- [x] Implement the basic multi-line `textarea` within the input area.
- [x] Implement the Send button.
- [x] Implement the Microphone (Voice Input) icon/button.
- [x] Implement the Paperclip (File Upload) icon/button.
- [x] Implement dynamic vertical resizing of the input `textarea` up to max height, then show scrollbar.
- [x] Implement animated placeholder text cycling in the input bar (e.g., "Explain the Pythagorean theorem...").

### 2.2 UI Styling & ChatGPT Aesthetic

- [x] Configure **Tailwind CSS** for styling.
- [x] Implement the overall minimalist, clean, content-focused style.
- [x] Implement the **Light Mode** color palette (White background, light gray bubbles/sidebar, black text, white input bar).
- [x] Implement the **Dark Mode** color palette (#202123 background, #343541 bubbles/sidebar/input bar, white text).
- [x] Implement the Theme Toggle button functionality to switch between light and dark modes.
- [x] Apply the chosen clean sans-serif font (e.g., Inter, system default) and ensure consistent typography and font sizes.
- [x] Implement consistent spacing and padding using an 8px grid system. Ensure generous padding within user message bubbles.
- [x] Select and integrate a clean, consistent icon set (e.g., Heroicons, Feather Icons) for buttons (Send, Stop, Mic, Paperclip, Copy, Edit, Regenerate, Theme Toggle, Litter Bin, Sidebar Toggle, File Remove 'x').
- [x] Style user messages: Right-aligned, **wrapped in a bubble** with distinct background color per theme.
- [x] Style AI messages: Left-aligned, **NOT wrapped in a bubble**, text block width slightly wider than the input bar's max width, standard text color per theme.
- [x] Integrate and style **KaTeX** for rendering LaTeX math equations inline and in display blocks seamlessly within message areas.
- [x] Style code blocks generated by the AI: Monospace font, syntax highlighting, distinct background (per theme), and integrated "Copy" button.
- [x] Style the input area components (textarea, buttons, file chips) according to the ChatGPT aesthetic for both light and dark modes.
- [x] Style the sidebar (fixed width on desktop, collapsible, off-canvas on mobile) and its elements ("New Chat" button, chat history items, active chat highlight).

### 2.3 Message Display & Interaction

- [x] Implement rendering of user messages.
- [x] Implement rendering of AI messages.
- [x] Implement Markdown rendering support within messages (bold, italics, lists, links, bullet points).
- [x] Add hover/touch behavior for user message buttons (Copy, Edit, Regenerate).
- [x] Add hover/touch behavior for AI message buttons (Copy, Regenerate).
- [x] Implement "Copy" functionality for user and AI messages (using JS Clipboard API).
- [x] Implement "Edit" functionality for user messages (replaces input content with message text).
- [x] Implement "Regenerate" functionality for user/AI messages (resends the associated prompt to the backend).

### 2.4 Input Features & Feedback

- [x] Implement Send button state logic (enabled when text input or file staged, disabled otherwise).
- [x] Implement Send button transformation to spinning "Stop" icon during AI generation.
- [x] Implement "Stop" button click handler to interrupt AI generation (sends signal to backend).
- [x] Implement "Thinking..." loading indicator message displayed as a temporary AI message.
- [x] Integrate **`react-speech-recognition`** for voice input.
- [x] Handle browser microphone permission requests gracefully.
- [x] Implement visual indicator during voice recording (e.g., pulsing mic icon).
- [x] Implement mechanism to stop voice recording (click or auto-pause).
- [x] Display transcribed voice input directly into the text input field for user review/editing.
- [x] Implement file selection via the Paperclip button (trigger OS file picker).
- [x] Implement client-side file type validation (`.pdf`, `.png`, `.jpg`, `.jpeg`, `.webp`, `.heic`, `.heif`, `.txt`, `.docx`).
- [x] Implement client-side file size validation (e.g., based on 20MB inline limit).
- [x] Display selected file(s) as chips *inside* the input bar with filename and remove ('x') button. Style chips appropriately.
- [x] Implement remove ('x') button logic for staged files.

### 2.5 Chat History Sidebar

- [x] Implement the collapsible sidebar component structure.
- [x] Implement the sidebar toggle button.
- [x] Implement the "New Chat" button functionality (clear view, save old chat, start new).
- [x] Implement the scrollable list area for chat history items.
- [x] Display chat history items with truncated titles (e.g., first user message).
- [x] Implement highlight the currently active chat session in the sidebar.
- [x] Implement click handler for chat history items to load previous sessions from the backend.
- [x] Implement UI for renaming chat sessions (e.g., on hover, double-click, trigger backend update).
- [x] Implement UI for deleting chat sessions (e.g., on hover, trigger backend update).
- [x] Implement confirmation dialog for chat deletion.
- [x] Implement the "Litter Bin" icon functionality in the header to clear the *current* chat view *without* saving it to history (with confirmation dialog).

### 2.6 Responsiveness & Accessibility

- [x] Implement CSS/Tailwind for responsiveness (mobile: sidebar off-canvas accessed via hamburger menu; tablet/desktop: sidebar visible/collapsible).
- [x] Implement semantic HTML structure for accessibility (A11y).
- [x] Ensure full keyboard navigation for all interactive elements (buttons, inputs, chat history items).
- [x] Implement logical focus management during interactions (initial focus on input, sidebar toggle, modals, message buttons).
- [x] Add appropriate ARIA attributes for screen reader support (labels, live regions for messages, announcements for loading/errors). Ensure KaTeX output is accessible.
- [x] Test and ensure adequate color contrast meets WCAG AA ratios in both light and dark modes.
- [x] Test UI reflow and functionality with browser zoom up to 200%.
- [x] Associate labels with form controls (can be visually hidden if needed).

### 2.7 User Feedback & Error Display

- [x] Implement visual feedback for copy actions (icon changes copy -> tick, toast message "Copied!").
- [x] Implement display logic for input-related error messages (e.g., file size/type) near the input bar.
- [x] Implement display logic for general/API error messages (as AI message or prominent toasts).
- [x] Implement user-friendly messages for specific backend/API errors (e.g., content filtered, file processing failed, network error).

## 3. Backend Development

### 3.1 Server Setup & Routing

- [x] Set up FastAPI application instance.
- [x] Define API endpoints for:
    - `/chat/stream` (POST for new messages, handling text/file refs, sending streaming data via SSE)
    - `/chat/history` (GET for listing chats)
    - `/chat/history/{chat_id}` (GET for loading specific chat messages)
    - `/chat/history` (POST for creating new chat implicitly via first message)
    - `/chat/history/{chat_id}` (PUT for renaming chat title)
    - `/chat/history/{chat_id}` (DELETE for deleting chat session and its messages)
    - `/stt` (POST for handling audio transcription via Whisper)
    - `/interrupt` (POST to signal AI generation interruption - if feasible to implement cancellation)

### 3.2 Core Chat Logic

- [x] Implement logic to receive user messages (text, file references, voice transcription).
- [x] Maintain conversation history state per chat session (retrieve from DB for context).
- [x] Implement logic to construct the prompt for Gemini API (system instruction, history, current user message, file context).
- [x] Implement logic to send prompt to Gemini API using the `google-genai` SDK.
- [x] Implement Server-Sent Events (SSE) endpoint to stream AI responses token-by-token to the frontend.
- [x] Implement logic to store conversation turns (user prompt, AI response) in the SQLite database, associating them with the correct chat session.
- [x] Handle interruption signal from frontend (attempt to close SSE connection or manage generation state).

### 3.3 Database Integration (SQLite)

- [x] Design SQLite database schema for `chats` (chat_id PK, title TEXT, create_time DATETIME) and `messages` tables (message_id PK, chat_id FK, role TEXT CHECK(role IN ('user', 'model')), content TEXT, timestamp DATETIME).
- [x] Implement database connection and session management for FastAPI.
- [x] Implement CRUD operations for `chats` (create on first message, list, get title, update title, delete).
- [x] Implement CRUD operations for `messages` (add message, get all messages for a chat_id ordered by timestamp).

### 3.4 File Handling & Processing

- [x] Implement logic to handle file references passed from the frontend (determine if it's PDF/Image needing Gemini processing or TXT/DOCX needing preprocessing).
- [x] Implement server-side file size checking *before* processing/uploading to Gemini Files API.
- [x] For `.txt` files: Read file content on the backend.
- [x] For `.docx` files: Use `python-docx` library to extract text content. Handle potential extraction errors.
- [x] Prepare file content (raw bytes for PDF/Image, extracted text for TXT/DOCX) to be passed to the Gemini API integration layer.

### 3.5 Speech-to-Text (Whisper API)

- [x] Implement endpoint `/stt` to receive audio blob/data from frontend.
- [x] Integrate with Hugging Face URL endpoint and API.
- [x] Send audio data for transcription.
- [x] Return the transcription text result to the frontend.
- [x] Handle potential errors during the transcription API call (network, API limits, invalid audio).

### 3.6 Error Handling & Security

- [x] Implement robust backend error handling (API errors, file processing errors, DB errors, STT errors). Return appropriate HTTP status codes and user-friendly error messages.
- [x] Log detailed errors server-side for debugging.
- [x] Sanitize all incoming user inputs (text prompts, file metadata) to prevent injection attacks.
- [x] Implement basic rate limiting on key API endpoints (`/chat/stream`, `/stt`) to prevent abuse.
- [x] Securely manage API keys (Gemini, Whisper) using environment variables or a secrets management solution.
- [x] Validate file MIME types passed from frontend before attempting processing.

## 4. API Integration (Google Gen AI SDK)

- [x] Instantiate `google.genai.Client` in the backend service layer.
- [x] Configure the client to use `gemini-2.5-flash-preview-04-17` model.
- [x] Implement text generation using `client.models.generate_content_stream` for streaming responses.
    - Reference: `gemini_api_doc.md - Streaming output`.
- [x] (Alternative) Use `client.chats.create`, `chat.send_message_stream` for managing chat history within the SDK, ensuring history persistence aligns with DB storage. Choose one consistent approach (manual history management + `generate_content_stream` or SDK chat object).
    - Reference: `gemini_api_doc.md - Multi-turn conversations` (Streaming section).
- [x] Integrate System Instructions using `config=types.GenerateContentConfig(system_instruction="You are an AI Math Chatbot...")` or equivalent in chat creation.
    - Reference: `gemini_api_doc.md - System instructions`.
- [x] Implement multimodal input handling for PDF and Image files received from the backend file processing layer:
    - [x] Determine if file size allows inline data (<20MB request size): Use `types.Part.from_bytes(data=file_bytes, mime_type=...)` in the `contents` list.
        - Reference: `gemini_api_doc.md - Image input - Pass image data inline`, `gemini_api_doc.md - Document understanding - PDF input - As inline data`.
    - [x] If file is large (>20MB request size, up to 2GB): Use **Gemini Files API** (`client.files.upload(file=file_path_or_bytes, config=dict(mime_type=...))`) to upload the file. Pass the returned `File` object (e.g., `uploaded_file`) in the `contents` list along with the text prompt.
        - Reference: `gemini_api_doc.md - Document understanding - Large PDFs stored locally`/`Large PDFs from URLs`, `gemini_api_doc.md - Image understanding - Upload an image file`, `gemini_api_doc.md - Files API`.
    - [x] Note and handle the 48-hour TTL of Files API uploads. The application won't have long-term storage for these unless explicitly added.
- [x] For TXT/DOCX, pass the extracted text content using `types.Part.from_text(...)` in the `contents` list.
- [x] Structure the `contents` argument correctly for API calls, combining text prompts, chat history (if managed manually), and file parts (`types.Part` within `types.Content`).
    - Reference: SDK docs - "How to structure `contents` argument for `generate_content`".
- [x] (Optional/Enhancement) Implement JSON structured output using `response_mime_type='application/json'` and `response_schema` for specific types of math problems if advanced parsing is needed (not required by PRD).
    - Reference: `gemini_api_doc.md - Thinking with structured output`, `gemini_api_doc.md - JSON Response Schema`.
- [x] Implement Gemini API error handling using `try...except google.genai.errors.APIError as e:`. Extract relevant error details (`e.message`, potentially `e.code`) to return to the frontend.
    - Reference: `gemini_api_doc.md - Error Handling`.
- [x] (Optional) Use `client.models.count_tokens` for logging or potential validation before sending large requests.
    - Reference: `gemini_api_doc.md - Count Tokens and Compute Tokens`.

## 5. Testing

- [ ] Write unit tests for backend utility functions (e.g., text extraction from DOCX), API request construction, DB operations.
- [ ] Write unit tests for frontend components and state management (Zustand stores). Test UI rendering based on state, button interactions.
- [ ] Write integration tests for frontend-backend communication: sending messages, file metadata, receiving SSE streams, receiving STT results, handling history operations.
- [ ] Write integration tests for backend-Gemini API interaction: Mock the `google-genai` client to simulate successful responses (text, stream), error responses, and test handling of different input types (text, inline files, Files API references).
- [ ] Write end-to-end tests using a testing framework (e.g., Playwright, Cypress) to simulate key user flows:
    - Initial load and centered input bar -> Send text message -> Input bar moves to bottom -> Receive streaming response.
    - Upload PDF/Image/TXT/DOCX -> Send related query -> Receive response based on file context.
    - Use voice input -> Edit transcription -> Send query -> Receive response.
    - Create new chat -> Interact -> Switch to old chat -> Rename/Delete chat.
    - Test theme switching.
    - Test copy/edit/regenerate buttons.
- [ ] Perform manual testing for responsiveness on different screen sizes (mobile, tablet, desktop).
- [ ] Perform manual testing for accessibility using screen readers and keyboard navigation.
- [ ] Test all error handling scenarios thoroughly (network disconnects, API failures, invalid files, mic permissions denied).

## 6. Deployment

- [ ] Finalize Dockerfiles for optimal build size and runtime for frontend (e.g., multi-stage build serving static files via Nginx) and backend (Python environment).
- [ ] Finalize Docker Compose configuration for local development and testing, including volume mounts for the SQLite DB if persistence is desired locally.
- [ ] Test building and running the complete application stack locally using Docker Compose.
- [ ] Create comprehensive documentation for setting up the environment (API keys) and running the application via Docker Compose.
- [ ] (Optional) Prepare deployment configurations (e.g., Kubernetes manifests, Cloud Run service YAML) if targeting a specific cloud platform.

## 7. Other Considerations

- [ ] Conduct a final review of security measures (input validation, output encoding, API key handling, rate limiting).
- [ ] Add comments and documentation to the codebase.
- [ ] Create a README file detailing the project setup, features, limitations, and how to run it.
- [ ] Monitor API usage and associated costs during development and testing.
- [ ] Clearly document known limitations: No user authentication, SQLite's scalability limits, 48hr TTL for Gemini Files API uploads (no long-term file storage integrated), synchronous backend processing.

---

**Milestones:**

- [ ] **Milestone 1:** Initial UI & Basic Text Chat (Frontend layout including centered input bar and transition, basic styling, Backend endpoint, Gemini Text Streaming via SSE, DB Save/Load basic history)
- [ ] **Milestone 2:** Styling & History Management (Implement full ChatGPT aesthetic - themes, fonts, spacing, icons; Sidebar UI, New/Load/Rename/Delete chat logic, Clear current chat)
- [ ] **Milestone 3:** File Upload Integration (Frontend file staging UI, Backend processing for TXT/DOCX, Gemini integration for PDF/Image using inline/Files API)
- [ ] **Milestone 4:** Voice Input & Interactions (Frontend Mic UI & STT integration, Message interaction buttons - Copy/Edit/Regenerate)
- [ ] **Milestone 5:** Testing, Refinement & Dockerization (Comprehensive testing, Error Handling polish, Accessibility checks, Finalize Docker setup)

---

**Technical Notes:**

*   **Gemini Model:** Using `gemini-2.5-flash-preview-04-17`. Leverage its long context, multimodal understanding, and default "thinking" capabilities.
*   **Input Bar Position:** Starts centered H/V, moves to fixed bottom after first interaction.
*   **Styling:** Strictly adhere to ChatGPT aesthetic guidelines (colors, fonts, spacing, minimalist design) defined in PRD.
*   **File Handling:** Differentiate between inline file data (<~20MB total request) using `types.Part.from_bytes` and larger files (up to 2GB per file, 20GB per project) using the **Gemini Files API** (`client.files.upload`). Files uploaded via the Files API only persist for 48 hours.
*   **Document/Image Tokens:** Each document page or image tile costs 258 tokens (check specific model details for tiling/resizing). Max 3600 pages/images per request.
*   **Audio Tokens:** Each second of audio costs 32 tokens. Max 9.5 hours total audio per request (relevant if switching STT to Gemini).
*   **Speech-to-Text:** Using OpenAI Whisper API as per PRD. Requires separate API key and integration.
*   **Streaming:** Implement Server-Sent Events (SSE) on the backend for streaming text from Gemini (`generate_content_stream` or `chat.send_message_stream`) to the frontend. Frontend uses Fetch API with Readable Streams.
*   **Database:** SQLite is file-based. Suitable for single-instance/local use.
*   **Concurrency:** Backend processing is synchronous. High load may cause delays.
*   **API Keys:** Must be managed securely via environment variables.
*   **No Authentication:** User identity and history persistence are tied to the local database instance.