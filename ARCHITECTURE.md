# MeetingHall Architecture

This document outlines the complete technical architecture of MeetingHall, utilizing Hexagonal Architecture and Domain-Driven Design (DDD) within a Modular Monorepo structure.

## Overall Architecture Diagram

```text
+-----------------------------------------------------------------------------------+
|                                MEETINGHALL CLIENTS                                |
|  +----------------+ +--------------------+ +-------------------+ +-------------+  |
|  | Desktop (Tauri)| | Web (Next.js)      | | API Services      | | SDK Access  |  |
|  +----------------+ +--------------------+ +-------------------+ +-------------+  |
+-----------------------------------------------------------------------------------+
                                         |
+-----------------------------------------------------------------------------------+
|                              CORE WORKFLOW ENGINE                                 |
|  [ Meeting ] -> [ Agenda ] -> [ Task ] -> [ AI Review ] -> [ Consensus ] -> ...   |
+-----------------------------------------------------------------------------------+
                                         |
+-----------------------------------------------------------------------------------+
|                              CORE BUSINESS LOGIC                                  |
|  +--------------------+   +-------------------+   +----------------------------+  |
|  | AI Collaboration   |   | Consensus Engine  |   | Plugins (Music, ERP, etc.) |  |
|  +--------------------+   +-------------------+   +----------------------------+  |
+-----------------------------------------------------------------------------------+
                                         |
+-----------------------------------------------------------------------------------+
|                                  AI ROUTER LAYER                                  |
| (Strict Abstraction: Core systems never call models directly, only the Router)    |
|  +---------+   +--------+   +----------+   +----------+   +--------------------+  |
|  | OpenAI  |   | Gemini |   | Claude   |   | Ollama   |   | MCP (Future)       |  |
|  +---------+   +--------+   +----------+   +----------+   +--------------------+  |
+-----------------------------------------------------------------------------------+
                                         |
+-----------------------------------------------------------------------------------+
|                        DATA & MEMORY (STORAGE ADAPTERS)                           |
|  +--------------------+ +-----------------------+ +----------------------------+  |
|  | Core Memory        | | Timeline Engine       | | Storage Adapter            |  |
|  | (Vector, Semantic) | | (Session State)       | | (IndexedDB / Firebase)     |  |
|  +--------------------+ +-----------------------+ +----------------------------+  |
+-----------------------------------------------------------------------------------+
Core Systems & Abstraction Layers
1. Core Workflow (core-workflow)
Defines the strict pipeline of operations: Meeting -> Agenda -> Task -> AI Review -> Consensus -> Decision -> Archive. It ensures every session follows a standardized logical path.

2. AI Router (core-router)
A crucial abstraction layer. The core-boardroom and AI Specialists never communicate with LLM providers directly. Instead, they send standardized requests to the core-router. The router then delegates the task to the appropriate adapter (OpenAI, Gemini, Claude, Ollama, or future MCPs). This ensures Business Logic remains untouched when swapping or upgrading models.

3. AI Specialists (specialists/)
Isolated persona definitions (e.g., Angela, David, Claude, Qwen). Each specialist has a defined context, operational constraints, and domain expertise, completely decoupled from the boardroom orchestrator.

4. Core Memory (core-memory)
Separated from the session timeline, this module handles context retrieval. It manages Meeting Memory (short-term context), Long-term Memory, Semantic Search, and Vector Indexing for RAG (Retrieval-Augmented Generation).

5. Plugins Ecosystem (plugins/)
Allows domain-specific expansions without bloating the core repository. Modules like music/, erp/, finance/, and legal/ can be dynamically injected into the boardroom.
