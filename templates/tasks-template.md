# Tasks: [FEATURE NAME]

**Input**: Design documents from `/specs/[###-feature-name]/`
**Prerequisites**: plan.md (required), research.md, data-model.md, contracts/

## Execution Flow (main)
```
1. Load plan.md from feature directory
   → If not found: ERROR "No implementation plan found"
   → Extract: tech stack, libraries, structure
2. Load optional design documents:
   → data-model.md: Extract entities → model tasks
   → contracts/: Each file → Specmatic MCP contract test task
   → research.md: Extract decisions → setup tasks
3. Generate tasks by category:
   → Setup: project init, dependencies, linting
   → Tests: Specmatic MCP contract tests, Playwright MCP browser tests, integration tests
   → Core: models, services, CLI commands
   → Integration: DB, middleware, logging
   → Polish: unit tests, performance, docs
4. Apply task rules:
   → Different files = mark [P] for parallel
   → Same file = sequential (no [P])
   → Tests before implementation (TDD)
5. Number tasks sequentially (T001, T002...)
6. Generate dependency graph
7. Create parallel execution examples
8. Validate task completeness:
   → All contracts have Specmatic MCP tests (contract + resiliency)?
   → All entities have models?
   → All endpoints implemented?
9. Return: SUCCESS (tasks ready for execution)
```

## Format: `[ID] [P?] Description`
- **[P]**: Can run in parallel (different files, no dependencies)
- Include exact file paths in descriptions

## Path Conventions
- **Single project**: `src/`, `tests/` at repository root
- **Web app**: `backend/src/`, `frontend/src/`
- **Mobile**: `api/src/`, `ios/src/` or `android/src/`
- Paths shown below assume single project - adjust based on plan.md structure

## Phase 3.1: Setup
- [ ] T001 Create project structure per implementation plan
- [ ] T002 Initialize [language] project with [framework] dependencies
- [ ] T003 [P] Configure linting and formatting tools

## Phase 3.2: Tests First (TDD) ⚠️ MUST COMPLETE BEFORE 3.3
**CRITICAL: RED-GREEN-REFACTOR Cycle - These tests MUST be written and MUST FAIL before ANY implementation**
**NO MANUAL CURL TESTING - Use only Specialized MCP Agents**
**VERIFY: Contract tests fail because NO routes/endpoints exist yet**
**VERIFY: Resiliency tests fail because NO input validation exists yet**
- [ ] T004 [P] Deploy contract-test-runner agent: Setup Specmatic MCP contract tests (must fail initially)
- [ ] T005 [P] Deploy api-resiliency-tester agent: Setup Specmatic MCP boundary condition tests
- [ ] T006 [P] Deploy api-mock-manager agent: Start Specmatic mock server on port 9001
- [ ] T007 [P] Configure frontend environment: REACT_APP_API_BASE_URL=http://localhost:9001
- [ ] T008 [P] Deploy Playwright MCP: Browser test for user registration flow
- [ ] T009 [P] Deploy Playwright MCP: Integration test auth flow with mock server

## Phase 3.3: Core Implementation (ONLY after tests are failing)
**GREEN Phase: Implement JUST ENOUGH to make failing tests pass**
- [ ] T010 [P] User model in src/models/user.py
- [ ] T011 [P] UserService CRUD in src/services/user_service.py
- [ ] T012 [P] CLI --create-user in src/cli/user_commands.py
- [ ] T013 POST /api/users endpoint (make contract tests pass)
- [ ] T014 GET /api/users/{id} endpoint (make contract tests pass)
- [ ] T015 Input validation (make resiliency tests pass)
- [ ] T016 Error handling and logging (make resiliency tests pass)
**VERIFY: All contract tests now pass**
**VERIFY: All resiliency tests now pass**

## Phase 3.4: Integration
- [ ] T017 Connect UserService to DB
- [ ] T018 Auth middleware
- [ ] T019 Request/response logging
- [ ] T020 CORS and security headers
- [ ] T021 Deploy api-mock-manager agent: Stop Specmatic mock servers (port 9001)
- [ ] T022 Start real backend on port 3000
- [ ] T023 Reconfigure frontend: REACT_APP_API_BASE_URL=http://localhost:3000
- [ ] T024 Deploy Playwright MCP: Run end-to-end integration tests

## Phase 3.5: Polish & Validation
**REFACTOR Phase: Clean up while keeping tests green**
- [ ] T025 [P] Unit tests for validation in tests/unit/test_validation.py
- [ ] T026 Deploy contract-test-runner agent: Final verification - ALL contract tests MUST pass
- [ ] T027 Deploy api-resiliency-tester agent: Final verification - ALL resiliency tests MUST pass
- [ ] T028 Performance tests (<200ms)
- [ ] T029 [P] Update docs/api.md
- [ ] T030 Remove duplication (REFACTOR while keeping tests green)
- [ ] T031 Deploy api-mock-manager agent: Shutdown all servers after tests complete

## Dependencies
- Tests (T004-T009) before implementation (T010-T016)
- T010 blocks T011, T017
- T018 blocks T020
- Implementation before integration (T017-T024)
- Integration before polish (T025-T031)

## Parallel Example
```
# Launch T004-T007 together with specialized agents:
Task: "Setup Specmatic MCP contract tests (must fail initially)"
Agent: contract-test-runner

Task: "Setup Specmatic MCP boundary condition tests"  
Agent: api-resiliency-tester

Task: "Start Specmatic mock server on port 9001"
Agent: api-mock-manager

Task: "Playwright MCP browser test for user registration flow"
Agent: Playwright MCP
```

## Notes
- [P] tasks = different files, no dependencies
- Verify tests fail before implementing
- Commit after each task
- Avoid: vague tasks, same file conflicts

## Task Generation Rules
*Applied during main() execution*

1. **From Contracts**:
   - Each contract file → contract-test-runner agent: Specmatic MCP contract test task [P]
   - Each contract file → api-resiliency-tester agent: Specmatic MCP resiliency test task [P]
   - Each endpoint → implementation task
   
2. **From Data Model**:
   - Each entity → model creation task [P]
   - Relationships → service layer tasks
   
3. **From User Stories**:
   - Each story → Playwright MCP: Browser test [P] (if frontend)
   - Each story → integration test [P]
   - Quickstart scenarios → validation tasks
   - Environment switching → api-mock-manager agent tasks (dev/prod mode)

4. **Ordering**:
   - Setup → Tests → Models → Services → Endpoints → Polish
   - Dependencies block parallel execution

## Validation Checklist
*GATE: Checked by main() before returning*

- [ ] All contracts have corresponding Specmatic MCP tests
- [ ] All entities have model tasks
- [ ] All tests come before implementation
- [ ] Parallel tasks truly independent
- [ ] Each task specifies exact file path
- [ ] No task modifies same file as another [P] task