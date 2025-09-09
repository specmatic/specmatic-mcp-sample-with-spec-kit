# Specmatic MCP Sample Project

This project demonstrates **contract-first development** using **[spec-kit](https://github.com/github/spec-kit)** where OpenAPI specifications evolve organically through feature development. Each feature analyzes existing contracts for reuse before extending the API, using **Specmatic MCP** as intelligent guardrails throughout the process.

## 🚀 Quick Start

```bash
# Configure MCP servers
claude mcp add specmatic npx "specmatic-mcp@latest"
claude mcp add playwright npx "@playwright/mcp@latest"

# Open project
claude
```

**Try the spec-kit workflow:**
```
/specify product listing page
- each product has name, description, price and category, all of these properties are mandatory
- category can be only "food", "gadget", "book" or "other"
- default sort order is alphabetical by name
- users should be able to filter by category
- no pagination required, just show all available products as per category filter
```

```
/plan Build the backend used nodeJS with in memory storage and frontend using React
```

```
/tasks To build a MVP version of this feature
```

```
implement T001-T006
```

Execute tasks in small chunks or all at once. The gated tasks make it easy to pause/resume without losing context.

## 📦 Specmatic MCP Resources

- 📦 **NPM Package**: [specmatic-mcp](https://www.npmjs.com/package/specmatic-mcp) - Easy NPM installation
- 📂 **Source Code**: [specmatic/specmatic-mcp-server](https://github.com/specmatic/specmatic-mcp-server) - GitHub repository

> **Note:** This project uses Claude Code for demo purposes, however you can use any coding agent of your choice and make necessary changes accordingly.

## 🎯 What This Template Demonstrates

This template shows **API Design First methodology** in action. Starting from **zero** (no pre-existing contracts), observe how:

- **Contract-first development** works using the spec-kit workflow: `/specify` → `/plan` → `/tasks` → implement  
- OpenAPI specifications **evolve organically** through feature development
- Existing API operations are **analyzed for reuse** before extending contracts
- Teams can work **independently** after agreeing on the contract
- **Specmatic MCP** provides intelligent guardrails throughout the process
- Frontend and backend stay **synchronized** with the evolving API specification

### ✅ Prerequisites

**Install Claude Code** (if not already installed):
Follow installation instructions at [https://docs.anthropic.com/claude/docs/claude-code](https://docs.anthropic.com/claude/docs/claude-code)

### 🔄 Optional Reset
**Reset the project to try again** (optional - Claude Code command available):
```
/reset-sample-project
```


## 📁 Project Structure

```
specmatic-mcp-sample-with-spec-kit/
├── api_spec.yaml         # OpenAPI specification (evolves with each feature)
├── specs/               # Feature specifications and plans
│   ├── 001-product-listing/
│   │   ├── spec.md     # Feature specification  
│   │   ├── plan.md     # Implementation plan
│   │   └── tasks.md    # Generated tasks
│   └── 002-next-feature/
├── backend/             # Node.js/Express API implementation (generated)
├── frontend/           # React frontend application (generated) 
├── memory/             # Project constitution and guidelines
│   └── constitution.md
├── templates/          # Spec-kit templates for feature development
└── .claude/           # Spec-kit commands (specify, plan, tasks)
```

## 🎯 Key Benefits Demonstrated

### Contract-First Development
- OpenAPI specifications evolve organically through feature development
- Each feature analyzes existing contracts for reuse before extending
- Both frontend and backend are built to conform to the evolving contract
- Smart contract analysis prevents API bloat and promotes reuse

### True Test-Driven Development
- Contract tests MUST fail before any backend implementation exists
- Backend routes/endpoints implemented only to make failing tests pass
- Resiliency tests MUST fail before input validation is added
- Follows strict RED-GREEN-REFACTOR cycle throughout

### Independent Development
- Backend implemented first against failing contract tests
- Frontend developed using Specmatic's mock server (port 9001) in parallel
- No coordination needed - contract serves as the agreement between teams

### Automatic Validation
- Specmatic MCP automatically validates backend implementations
- Contract tests ensure API compliance
- Resiliency tests verify error handling and boundary conditions

### Zero Dependencies
- Specmatic runs as an MCP server through NPX
- No need to add Specmatic dependencies to your project
- Clean project structure with minimal tooling overhead

## 🔧 How It Works

1. **Spec-Kit Workflow**: Features developed through `specify` → `plan` → `tasks` → `implement` cycles

2. **Smart Contract Evolution**:
   - First feature creates initial OpenAPI specification at repository root
   - Subsequent features analyze existing contracts for reuse opportunities  
   - Only extends API when existing operations cannot support new features
   - Prevents API bloat through intelligent contract analysis

3. **Specmatic MCP Integration**:
   - Provides contract testing capabilities for evolving specifications
   - Offers mock server functionality for isolated frontend development
   - Validates implementations against the current contract state
   - Runs resiliency tests for error scenarios

4. **Constitutional Governance**:
   - All development follows constitutional principles in `/memory/constitution.md`
   - Ensures consistent, high-quality feature development
   - Maintains contract-first discipline throughout the process

## 🏗️ Architecture Diagrams

### Production Setup
```
┌─────────────────┐                                  ┌─────────────────┐
│                 │ ────── HTTP Requests ──────────► │                 │
│    Frontend     │                                  │    Backend      │
│   (React App)   │        ┌─────────────────┐       │ (Express API)   │
│                 │        │  api_spec.yaml  │       │                 │
│   Port: 4000    │        │ (Evolved OpenAPI)│       │   Port: 3000    │
│                 │        └─────────────────┘       │                 │
|                 |                                  |                 |
│                 │ ◄────── HTTP Responses ───────── │                 │
└─────────────────┘                                  └─────────────────┘
```

### Development Setup - Frontend
```
┌─────────────────┐                     ┌─────────────────┐
│                 │                     │                 │
│    Frontend     │     Mock Requests   │ Specmatic Mock  │
│   (React App)   │ ◄─────────────────► │    Server       │
│                 │                     │                 │
│   Port: 4000    │                     │   Port: 9001    │
└─────────────────┘                     └─────────┬───────┘
                                                  │
                                                  │ Based on
                                                  │
                                                  ▼
                                     ┌─────────────────────┐
                                     │                     │
                                     │   api_spec.yaml     │
                                     │  (Evolved OpenAPI)  │
                                     │                     │
                                     └─────────────────────┘
```

### Development Setup - Backend
```
┌─────────────────┐                       ┌─────────────────┐
│                 │                       │                 │
│ Specmatic MCP   │ ───► Contract   ───►  │    Backend      │
│    Tools        │      Testing          │ (Express API)   │
│                 │                       │                 │
│ (via NPX)       │ ───► Resiliency ───►  │   Port: 3000    │
└─────────┬───────┘      Testing          └─────────────────┘
          │
          │ Validates against
          │
          ▼
┌─────────────────────┐
│                     │
│   api_spec.yaml     │
│  (Evolved OpenAPI)  │
│                     │
└─────────────────────┘
```

## 🎨 Contract Evolution Example

As features are developed, the API evolves organically:

**Feature 1** (`001-product-listing`):
- Creates initial `api_spec.yaml` with GET /products endpoint
- Includes product filtering by type (book, food, gadget, other)

**Feature 2** (`002-product-creation`):
- Analyzes existing contract → No POST endpoint exists
- Extends `api_spec.yaml` with POST /products and validation schemas

**Feature 3** (`003-product-search`):
- Analyzes existing contract → GET /products with query params might suffice  
- **Reuses existing endpoint** instead of creating new ones

The complete API specification emerges through this thoughtful, feature-driven evolution.

## 🏗️ API Design First Workflow

1. **Feature Specification**: Use `/specify` to create feature requirements and user stories
2. **Contract Analysis**: Use `/plan` to analyze existing contracts and extend only if needed  
3. **Task Generation**: Use `/tasks` to break down implementation into concrete steps
4. **Backend-First Implementation** (RED-GREEN-REFACTOR):
   - **RED**: Contract tests MUST FAIL (no routes/endpoints exist yet)
   - **GREEN**: Implement just enough backend code to make contract tests pass
   - **RED**: Resiliency tests MUST FAIL (no input validation exists yet)  
   - **GREEN**: Add input validation to make resiliency tests pass
   - **REFACTOR**: Clean up implementation while keeping tests green
5. **Frontend Implementation**: Develop UI against Specmatic mock servers (port 9001) in parallel
6. **Integration**: Switch frontend to real backend (port 3000) and verify end-to-end
7. **Iteration**: Repeat for next feature, building on the evolved contract base

## 📚 Learn More

- [Spec-Kit](https://github.com/github/spec-kit) - Methodology for API Design First development
- [Specmatic MCP Server](https://github.com/specmatic/specmatic-mcp-server) - MCP server for contract testing and service virtualization

---

**Ready to see spec-kit contract evolution in action? Just ask Claude to build your first feature!**
