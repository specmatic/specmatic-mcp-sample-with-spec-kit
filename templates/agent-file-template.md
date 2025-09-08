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
# Start Specmatic mock server on port 9001
# Start backend on port 3000  
# Start frontend on port 4000
# Environment switching: REACT_APP_API_BASE_URL=http://localhost:9001 (dev) / http://localhost:3000 (prod)

# Testing Commands (mandatory)
# Run Specmatic MCP contract tests
# Run Specmatic MCP resiliency tests  
# Run Playwright MCP browser tests
# NO manual curl testing allowed

## Code Style
[LANGUAGE-SPECIFIC, ONLY FOR LANGUAGES IN USE]

## MCP Testing Requirements
- Contract-First Development: All features start with OpenAPI specification
- Ordered workflow: Backend (port 3000) → Frontend (port 4000) → Integration
- Environment isolation: dev mode (mock port 9001) → prod mode (backend port 3000)
- Mandatory: Specmatic MCP contract + resiliency tests must pass
- Mandatory: Playwright MCP browser testing for frontend
- Prohibited: Manual curl or Postman testing

## Recent Changes
[LAST 3 FEATURES AND WHAT THEY ADDED]

<!-- MANUAL ADDITIONS START -->
<!-- MANUAL ADDITIONS END -->