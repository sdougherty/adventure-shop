# Adventure Shop

## AGENTS.md Usage

AGENTS.md files are hierarchical. AI agents must follow this resolution order:

1. Look for an AGENTS.md file in the current working directory
2. If not found, traverse up to the parent directory
3. Continue traversing parent directories until an AGENTS.md file is found
4. Apply the instructions from the nearest AGENTS.md file

This allows for directory-specific instructions that can override or extend project-level guidance.

## Documentation

The `docs/` directory in the project root contains project-level documentation. Documentation directories are hierarchical. AI agents must follow this resolution order:

1. Look for a `docs/` subdirectory in the current working directory
2. If not found, traverse up to the parent directory
3. Continue traversing parent directories until a `docs/` directory is found

### Documentation Structure

All `docs/` directories consist of the following subdirectories:

#### specs/
Contains all specifications and requirements:
- Business requirements
- Business rules and logic
- Domain-specific information
- Functional requirements
- Non-functional requirements
- Research and findings

#### decisions/
Contains architecture decision records (ADRs). AI agents must:
- Follow decisions as additional technical and non-technical standards
- AI agents may challenge a prior decision if circumstances have changed, but must do so by prompting the user for confirmation before proceeding

#### plans/
Contains implementation plans for features. AI agents will:
- Write out the plan for each app
- Document the tasks required to complete features

## Project Structure

This repository is a monorepo containing multiple applications.

```
adventure-shop/
├── apps/
│   └── <app-name>/
│       ├── src/                # Application source code
│       └── tests/              # Application tests
│       └── docs/               # Application documentation
│           ├── decisions/      # Architecture decisions
│           ├── plans/          # Feature implementation plans
│           └── specs/          # Requirements and specifications
├── libs/                       # Shared libraries and packages
├── docs/                       # Project documentation
│   ├── decisions/              # Architecture decisions
│   ├── plans/                  # Feature implementation plans
│   └── specs/                  # Requirements and specifications
├── .github/                    # GitHub workflows and configuration
├── AGENTS.md                   # This file
├── CLAUDE.md                   # Claude Code instructions
└── README.md                   # Project readme
```

## Applications

All applications are located in the `apps/` directory. Each application follows a consistent structure:

- `src/` - Contains the application source code
- `tests/` - Contains the application test files

## Tech Stack

### Front-end Web Applications

- **Framework:** Next.js with App Router
- **Language:** TypeScript
- **Build/Task Runner:** Nx (with Next.js/React, Jest, Playwright plugins)
- **Linting:** ESLint
- **Formatting:** Prettier
- **Package Manager:** pnpm
- **Unit Testing:** Jest with React Testing Library
- **E2E Testing:** Playwright (required for all front-end apps)

### Back-end Services

- **Language:** Java 25
- **Framework:** Spring Reactive Stack (Spring WebFlux)
- **Build/Task Runner:** Gradle
- **API Documentation:** OpenAPI specs required for all RESTful APIs (must be kept up-to-date)

### Infrastructure

- **Containers:** Docker with Alpine-based images
- **Orchestration:** Docker Compose
- **Database:** PostgreSQL (running in Docker)

## Development Guidelines

- Each app is self-contained with its own source and test directories
- Tests should mirror the structure of the source code they test
- Shared code used by two or more apps must be extracted to a dedicated package in the `libs/` directory
- All applications must be containerized using lightweight Alpine-based Docker images
- Use Docker Compose for local development and service orchestration
- Front-end apps must use ESLint and Prettier for code quality
- Use pnpm for all JavaScript/TypeScript package management
