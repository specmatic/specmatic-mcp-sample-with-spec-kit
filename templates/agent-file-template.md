# [PROJECT NAME] Development Guidelines

Auto-generated from all feature plans. Last updated: [DATE]

## Active Technologies
[EXTRACTED FROM ALL PLAN.MD FILES]
- Specmatic MCP (contract testing - mandatory)
- Playwright MCP (UI automation testing - mandatory)

## Project Structure
```
[ACTUAL STRUCTURE FROM PLANS]
```

## Commands
[ONLY COMMANDS FOR ACTIVE TECHNOLOGIES]

# MCP Server Management (mandatory for all features)
# Parallel Development Support:
# - Backend and frontend can develop simultaneously after OpenAPI contract
# - Start Specmatic mock server on port 9001 for frontend development
# - Start backend on port 3000 (can run in parallel with frontend)  
# - Start frontend on port 4000 (can run in parallel with backend)
# Environment switching: REACT_APP_API_BASE_URL=http://localhost:9001 (dev) / http://localhost:3000 (prod)
# Backward compatibility: Run compatibility checks for existing OpenAPI specs

# Testing Commands (mandatory)
# @agent-contract-test-runner: Run Specmatic MCP contract tests
# @agent-api-resiliency-tester: Run Specmatic MCP resiliency tests
# @agent-ui-component-tester: Run Playwright MCP browser tests
# NO manual curl testing allowed

## Code Style
[LANGUAGE-SPECIFIC, ONLY FOR LANGUAGES IN USE]

## MCP Testing Requirements
- Contract-First Development: All features start with OpenAPI specification
- Parallel Development Workflow: Backend (port 3000) and Frontend (port 4000) develop simultaneously after OpenAPI contract definition
- Environment isolation: dev mode (mock port 9001) → prod mode (backend port 3000)
- OpenAPI backward compatibility checks required for existing specifications
- Incremental updates: Check for existing backend/frontend directories before scaffolding
- Mandatory: @agent-contract-test-runner + @agent-api-resiliency-tester tests must pass sequentially
- Mandatory: @agent-ui-component-tester browser testing for frontend
- Prohibited: Manual curl or Postman testing

## Recent Changes
[LAST 3 FEATURES AND WHAT THEY ADDED]

<!-- MANUAL ADDITIONS START -->
<!-- MANUAL ADDITIONS END -->