# Specmatic MCP Sample Constitution

## Core Principles

### I. Contract-First Development
All features begin with OpenAPI specification definition. Backend and frontend implementations must strictly adhere to contract-defined interfaces. API contracts serve as the single source of truth for inter-service communication, data models, and validation rules.

### II. Ordered Development Workflow
Development follows a strict three-phase approach: Backend development (First Priority) - implement against OpenAPI contract; Frontend development (Second Priority) - develop against Specmatic mock servers; Component testing (Third Priority) - verify UI components and contract compliance independently.

### III. Contract Testing (NON-NEGOTIABLE)  
Specmatic MCP contract testing is mandatory for all API implementations. Both contract tests and resiliency tests must pass before code integration. UI component testing using ui-component-tester agent is mandatory for frontend components. Manual testing with curl or similar tools is prohibited - all validation occurs through automated contract verification and component testing.

### IV. Environment-Based Component Isolation
Components must be developed and tested in isolation before integration. Dev mode: Frontend connects to mock servers (port 9001); Prod mode: Frontend connects to real backend (port 3000). Each component validates independently against contract specifications using specialized MCP agents.

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
2. **Backend Implementation**: Develop API endpoints strictly following OpenAPI contract, validate with Specmatic MCP
3. **Frontend Mock Development**: Build UI components against Specmatic mock servers for complete isolation
4. **Component Validation**: Test UI components independently using ui-component-tester agent and validate contract compliance

### Quality Gates
- Contract tests must pass before any code integration
- Resiliency tests are mandatory for all API implementations  
- UI component testing required using ui-component-tester agent
- No manual testing tools (curl, Postman) - only automated contract verification and component testing
- Server shutdown after successful test completion is mandatory

## Governance

### Constitutional Authority
This constitution supersedes all other development practices and guidelines. All feature development, code reviews, and architectural decisions must verify compliance with these principles. Any deviation requires explicit documentation and justification.

### Compliance Requirements
- All PRs must demonstrate adherence to Contract-First Development principles
- Specmatic MCP test results are mandatory for code integration approval
- UI component test results using ui-component-tester agent are mandatory for frontend changes
- Phase-based workflow must be followed without exception
- Component isolation testing is required using specialized MCP agents
- Use templates/spec-template.md for creating feature specifications aligned with these principles

### Amendment Process
Constitutional changes require documentation of impact, approval from project stakeholders, and migration plan for existing implementations. Version control tracks all constitutional modifications.

**Version**: 1.0.0 | **Ratified**: 2025-09-07 | **Last Amended**: 2025-09-07