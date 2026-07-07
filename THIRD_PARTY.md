# Third-Party Technologies

MeetingHall stands on the shoulders of giants. We integrate mature third-party libraries for foundational infrastructure, keeping our focus on building the AI Boardroom experience.

## Meetily Infrastructure Integration
We are adapting the following modules from Meetily. They are strictly utilized as underlying infrastructure and heavily modified to fit MeetingHall's modular architecture.

*   **Audio Capture Module:** Handles microphone streams and OS-level audio routing.
*   **Whisper Integration:** Wrappers for running speech-to-text models.
*   **Transcript Engine:** Logic for timestamping and speaker diarization.
*   **AI Provider Layer:** Abstraction for LLM API calls.
*   **Export Engine:** Compiling final data into PDF/Markdown.

## Core Dependencies

| Technology | Purpose | License |
| :--- | :--- | :--- |
| **Tauri** | Cross-platform desktop application framework ensuring low resource overhead and native system access. | MIT / Apache 2.0 |
| **React & Next.js** | Frontend rendering, component architecture, and routing for the Boardroom UX. | MIT |
| **Tailwind CSS** | Utility-first CSS framework for rapid, consistent UI development. | MIT |
| **Firebase** | Backend-as-a-Service for Cloud Mode (Authentication, Firestore, Storage). | Apache 2.0 |
| **IndexedDB** | In-browser database for true offline persistence in Local Mode. | N/A (Web Standard) |
| **Whisper.cpp** | High-performance C/C++ port of OpenAI's Whisper for local transcription. | MIT |
| **Ollama** | Framework for running large language models locally, enabling offline AI specialists. | MIT |
