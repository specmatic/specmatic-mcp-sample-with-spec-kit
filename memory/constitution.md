# Specmatic MCP Sample Constitution

## Core Principles

### I. Contract-First Development
All features begin with OpenAPI specification definition. Backend and frontend implementations must strictly adhere to contract-defined interfaces. API contracts serve as the single source of truth for inter-service communication, data models, and validation rules.

### II. Parallel Development Workflow
Development follows a contract-first approach enabling parallel execution: OpenAPI contract definition (Foundation) - serves as coordination point for parallel development; Backend and Frontend development (Parallel Execution) - backend implements against contract while frontend develops against Specmatic mock servers simultaneously; Component testing (Final Phase) - verify UI components and contract compliance independently after parallel development completion.

### III. Contract Testing (NON-NEGOTIABLE)  
Specmatic MCP contract testing is mandatory for all API implementations. Both contract tests and resiliency tests must pass before code integration. UI component testing using @agent-ui-component-tester is mandatory for frontend components. Manual testing with curl or similar tools is prohibited - all validation occurs through automated contract verification and component testing.

### IV. Environment-Based Component Isolation
Components must be developed and tested in isolation with parallel development support. OpenAPI contract serves as the coordination interface enabling simultaneous development. Dev mode: Frontend connects to mock servers (port 9001) during parallel development; Prod mode: Frontend connects to real backend (port 3000) after backend completion. Each component validates independently against contract specifications using specialized MCP agents.

### V. Code Structure & Quality Standards
Maintain clear separation of concerns with routes, models, controllers in separate files/folders. Use descriptive variable names, implement proper error handling, follow RESTful conventions, and return appropriate HTTP status codes as defined in OpenAPI specifications.

## Technical Constraints

### Technology Stack Requirements
- Backend: Node.js with Express framework, in-memory data structures (no external databases)
- Frontend: React application running on port 4000 only
- API Specification: OpenAPI 3.0+ format defining all endpoints and schemas
- Environment management: Use latest stable Node.js version (nvm use stable)

### Port Configuration Standards
- Backend production server: Port 3000 (as defined in OpenAPI specification)
- Frontend development server: Port 4000 (fixed requirement)
- Specmatic mock server: Port 9001 (for frontend isolation testing)
- Environment variables: REACT_APP_API_BASE_URL for API endpoint configuration

## Development Workflow

### Phase-Based Implementation Process
1. **Contract Definition**: Create or update OpenAPI specification with all endpoints, schemas, and validation rules
2. **Parallel Development Phase**: Backend and Frontend development execute simultaneously:
   - **Backend Track**: Develop API endpoints strictly following OpenAPI contract, validate with Specmatic MCP
   - **Frontend Track**: Build UI components against Specmatic mock servers for complete isolation
3. **Integration & Component Validation**: Test UI components independently using @agent-ui-component-tester, validate contract compliance, and perform end-to-end integration testing

### Quality Gates
- OpenAPI contract definition must be complete before parallel development begins
- Contract tests must pass for backend track completion
- Resiliency tests are mandatory for all API implementations  
- UI component testing required using @agent-ui-component-tester for frontend track
- Integration testing required after both tracks complete
- No manual testing tools (curl, Postman) - only automated contract verification and component testing
- Server shutdown after successful test completion is mandatory

## Governance

### Constitutional Authority
This constitution supersedes all other development practices and guidelines. All feature development, code reviews, and architectural decisions must verify compliance with these principles. Any deviation requires explicit documentation and justification.

### Compliance Requirements
- All PRs must demonstrate adherence to Contract-First Development principles
- Specmatic MCP test results are mandatory for code integration approval
- UI component test results using @agent-ui-component-tester are mandatory for frontend changes
- Parallel development workflow must be followed with proper OpenAPI contract coordination
- Component isolation testing is required using specialized MCP agents
- Use templates/spec-template.md for creating feature specifications aligned with these principles

### Amendment Process
Constitutional changes require documentation of impact, approval from project stakeholders, and migration plan for existing implementations. Version control tracks all constitutional modifications.

**Version**: 1.0.0 | **Ratified**: 2025-09-07 | **Last Amended**: 2025-09-07