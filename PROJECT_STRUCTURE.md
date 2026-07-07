// 📂 File Location: PROJECT_STRUCTURE.md
# Project Structure

MeetingHall follows a modular monorepo structure, strictly separating infrastructure, domain logic, configuration, and API access.

```text
meetinghall/
├── apps/
│   ├── desktop/                # Tauri desktop application
│   ├── web/                    # Next.js web application
│   └── api/                    # API services for external integrations
│
├── packages/
│   ├── core-boardroom/         # Orchestrates multi-agent interactions
│   ├── core-workflow/          # Manages the pipeline: Meeting -> Agenda -> Consensus
│   ├── core-router/            # Abstraction layer for AI Adapters (OpenAI, Gemini, etc.)
│   ├── core-consensus/         # Algorithms for debate resolution and decision making
│   ├── core-memory/            # Vector indexing, semantic search, and long-term knowledge
│   ├── core-timeline/          # Tracks meeting states and session history
│   │
│   ├── specialists/            # AI Persona definitions
│   │   ├── Angela/
│   │   ├── David/
│   │   ├── Claude/
│   │   ├── Gemini/
│   │   └── Qwen/
│   │
│   ├── infra-audio/            # Infrastructure: Audio capture (Meetily adapted)
│   ├── infra-transcript/       # Infrastructure: Whisper parsing (Meetily adapted)
│   ├── infra-llm/              # Infrastructure: Low-level model formatting
│   │
│   ├── storage-adapter/        # Data persistence (Local/Cloud bridging)
│   │
│   ├── plugins/                # Domain-specific extensibility
│   │   ├── music/
│   │   ├── erp/
│   │   ├── finance/
│   │   └── legal/
│   │
│   ├── ui-components/          # Shared frontend elements (React/Tailwind)
│   └── sdk/                    # Software Development Kit for third-party access
│
├── config/                     # Centralized configurations
│   ├── providers.json          # AI Provider settings
│   ├── roles.json              # Access control roles
│   └── permissions.json        # Security and API policies
│
├── docs/                       # Architecture, Vision, and Developer Guides
├── scripts/                    # Build, deployment, and testing utilities
└── README.md
