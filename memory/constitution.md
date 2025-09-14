# Specmatic MCP Sample Constitution

## Core Principles

### I. Contract-First Development
All features begin with OpenAPI specification definition. Backend and frontend implementations must strictly adhere to contract-defined interfaces. API contracts serve as the single source of truth for inter-service communication, data models, and validation rules.

### II. Parallel Development Workflow
Development follows a contract-first approach enabling parallel execution: OpenAPI contract definition (Foundation) - serves as coordination point for parallel development; Backend and Frontend development (Parallel Execution) - backend implements against contract while frontend develops against Specmatic mock servers simultaneously; Component testing (Final Phase) - verify UI components and contract compliance independently after parallel development completion.

### III. Contract Testing (NON-NEGOTIABLE)
Specmatic MCP contract testing is mandatory for all API implementations. Both contract tests and resiliency tests must pass before code integration. UI component testing using specialized MCP agents is mandatory for frontend components. Manual testing tools are prohibited - all validation occurs through automated contract verification and component testing.

### IV. Environment-Based Component Isolation
Components must be developed and tested in isolation with parallel development support. OpenAPI contract serves as the coordination interface enabling simultaneous development. Development mode enables frontend isolation using mock servers during parallel development. Production mode connects frontend to real backend after both tracks complete. Each component validates independently against contract specifications using specialized MCP agents.

### V. Code Structure & Quality Standards
Maintain clear separation of concerns with routes, models, controllers in separate files/folders. Use descriptive variable names, implement proper error handling, follow RESTful conventions, and return appropriate HTTP status codes as defined in OpenAPI specifications.

## Technical Constraints

### Technology Stack Requirements
Implementation must use consistent technology stack as defined in project templates. API specifications must follow OpenAPI 3.0+ format for contract compatibility with Specmatic MCP.

### Development Environment Standards
Development environment must support parallel frontend and backend development with clear port separation for component isolation testing.

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
- UI component testing required using specialized MCP agents for frontend track
- Integration testing required after both tracks complete
- No manual testing tools - only automated contract verification and component testing
- Clean environment shutdown after successful test completion is mandatory

## Governance

### Constitutional Authority
This constitution supersedes all other development practices and guidelines. All feature development, code reviews, and architectural decisions must verify compliance with these principles. Any deviation requires explicit documentation and justification.

### Compliance Requirements
- All PRs must demonstrate adherence to Contract-First Development principles
- Specmatic MCP test results are mandatory for code integration approval
- UI component test results using specialized MCP agents are mandatory for frontend changes
- Parallel development workflow must be followed with proper OpenAPI contract coordination
- Component isolation testing is required using specialized MCP agents
- Project templates must be used for creating feature specifications aligned with these principles

### Amendment Process
Constitutional changes require documentation of impact, approval from project stakeholders, and migration plan for existing implementations. Version control tracks all constitutional modifications.

#### Amendment History
- **v1.1.0** (2025-09-13): Major architectural change - Transformed Article II from sequential "Ordered Development Workflow" to "Parallel Development Workflow" enabling simultaneous backend/frontend development. Enhanced Article IV component isolation with parallel development support. Updated Phase-Based Implementation Process to support parallel execution tracks. Added parallel development quality gates and compliance requirements.
- **v1.0.0** (2025-09-07): Initial constitution ratification with contract-first development principles

**Version**: 1.1.0 | **Ratified**: 2025-09-07 | **Last Amended**: 2025-09-13