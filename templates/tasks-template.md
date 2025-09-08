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
3. Generate tasks by THREE-PHASE approach:
   → BACKEND PHASE: Setup, contract tests (RED), implementation (GREEN), resiliency tests pass
   → FRONTEND PHASE: Mock server setup, UI development, component tests, shutdown mocks
   → INTEGRATION PHASE: Real backend startup, frontend reconfiguration, integration tests, shutdown all
4. Apply task rules:
   → Different files = mark [P] for parallel
   → Same file = sequential (no [P])
   → Backend TDD: Tests before implementation (RED-GREEN-REFACTOR)
   → Frontend: Build against mocks, component tests (no RED-GREEN needed)
   → Always shutdown mocks when their use is over
5. Number tasks sequentially (T001, T002...) within each phase
6. Generate dependency graph with phase barriers
7. Create parallel execution examples per phase
8. Validate task completeness:
   → Backend completion gates: All contract + resiliency tests pass?
   → All entities have models?
   → All endpoints implemented and tested?
   → Mock lifecycle properly managed?
9. Return: SUCCESS (three-phase tasks ready for execution)
```

## Format: `[ID] [P?] Description`
- **[P]**: Can run in parallel (different files, no dependencies)
- Include exact file paths in descriptions

## Path Conventions
- **Single project**: `src/`, `tests/` at repository root
- **Web app**: `backend/src/`, `frontend/src/`
- **Mobile**: `api/src/`, `ios/src/` or `android/src/`
- Paths shown below assume single project - adjust based on plan.md structure

## BACKEND PHASE - Complete Before Frontend

### Phase 3.1: Backend Setup
- [ ] T001 Create backend project structure per implementation plan
- [ ] T002 Initialize [language] backend project with [framework] dependencies
- [ ] T003 [P] Configure backend linting and formatting tools

### Phase 3.2: Backend Tests First (TDD) ⚠️ MUST COMPLETE BEFORE 3.3
**CRITICAL: RED-GREEN-REFACTOR Cycle - These tests MUST be written and MUST FAIL before ANY implementation**
**NO MANUAL CURL TESTING - Use only Specialized MCP Agents**
**VERIFY: Contract tests fail because NO routes/endpoints exist yet**
**VERIFY: Resiliency tests fail because NO input validation exists yet**
- [ ] T004 [P] Deploy contract-test-runner agent: Setup Specmatic MCP contract tests (must fail initially)
- [ ] T005 [P] Deploy api-resiliency-tester agent: Setup Specmatic MCP boundary condition tests

### Phase 3.3: Backend Implementation (ONLY after tests are failing)
**GREEN Phase: Implement JUST ENOUGH to make failing tests pass**
- [ ] T006 [P] User model in backend/src/models/user.py
- [ ] T007 [P] UserService CRUD in backend/src/services/user_service.py
- [ ] T008 [P] CLI --create-user in backend/src/cli/user_commands.py
- [ ] T009 POST /api/users endpoint (make contract tests pass)
- [ ] T010 GET /api/users/{id} endpoint (make contract tests pass)
- [ ] T011 Input validation (make resiliency tests pass)
- [ ] T012 Error handling and logging (make resiliency tests pass)
**VERIFY: All contract tests now pass**
**VERIFY: All resiliency tests now pass**

### Phase 3.4: Backend Integration & Polish
**REFACTOR Phase: Clean up while keeping tests green**
- [ ] T013 Connect UserService to DB
- [ ] T014 Auth middleware
- [ ] T015 Request/response logging
- [ ] T016 CORS and security headers
- [ ] T017 [P] Performance validation tests
- [ ] T018 Deploy contract-test-runner agent: Final backend verification - ALL contract tests MUST pass
- [ ] T019 Deploy api-resiliency-tester agent: Final backend verification - ALL resiliency tests MUST pass
- [ ] T020 Remove duplication (REFACTOR while keeping tests green)
**BACKEND COMPLETION GATE: All contract and resiliency tests must pass before proceeding to frontend**

## FRONTEND PHASE - Start After Backend Complete

### Phase 4.1: Frontend Setup with Mocks
- [ ] T021 Deploy api-mock-manager agent: Start Specmatic mock server on port 9001
- [ ] T022 Create frontend project structure
- [ ] T023 Initialize frontend project with framework dependencies
- [ ] T024 Configure frontend environment: REACT_APP_API_BASE_URL=http://localhost:9001
- [ ] T025 [P] Configure frontend linting and formatting tools

### Phase 4.2: Frontend Development & Component Testing
**Build against mock API - No RED-GREEN cycle needed for UI**
- [ ] T026 [P] User registration component in frontend/src/components/UserRegistration.js
- [ ] T027 [P] User profile component in frontend/src/components/UserProfile.js
- [ ] T028 [P] Deploy ui-component-tester agent: Component test for user registration form
- [ ] T029 [P] Deploy ui-component-tester agent: Component test for user profile display
- [ ] T030 [P] Deploy ui-component-tester agent: Component test auth flow with mock server
- [ ] T031 Deploy api-mock-manager agent: Shutdown Specmatic mock servers (port 9001)

## INTEGRATION PHASE - Final Integration

### Phase 5.1: Real Backend Integration
- [ ] T032 Start real backend on port 3000
- [ ] T033 Reconfigure frontend: REACT_APP_API_BASE_URL=http://localhost:3000
- [ ] T034 Deploy ui-component-tester agent: Integration tests with real backend
- [ ] T035 [P] End-to-end workflow validation
- [ ] T036 [P] Performance tests (<200ms)
- [ ] T037 [P] Update documentation
- [ ] T038 Shutdown all services after testing complete

## Dependencies
**Backend Phase Dependencies:**
- Backend tests (T004-T005) before backend implementation (T006-T012)
- Backend models (T006) block backend services (T007)
- Backend implementation before integration (T013-T016)
- Backend completion gate: T018-T019 must pass before Frontend Phase

**Frontend Phase Dependencies:**
- Mock server (T021) before frontend development (T022-T030)
- Frontend components before component tests (T026-T027 before T028-T030)
- Mock shutdown (T031) before Integration Phase

**Integration Phase Dependencies:**
- Backend must be running (T032) before frontend reconfiguration (T033)
- Integration tests (T034) before final validation (T035-T037)

## Parallel Examples by Phase

### Backend Phase Parallel Tasks:
```
# Launch T004-T005 together:
Task: "Setup Specmatic MCP contract tests (must fail initially)"
Agent: contract-test-runner

Task: "Setup Specmatic MCP boundary condition tests"  
Agent: api-resiliency-tester

# Launch T006-T008 together (different files):
Task: "User model in backend/src/models/user.py"
Task: "UserService CRUD in backend/src/services/user_service.py" 
Task: "CLI --create-user in backend/src/cli/user_commands.py"
```

### Frontend Phase Parallel Tasks:
```
# Launch T028-T030 together:
Task: "Component test for user registration form"
Agent: ui-component-tester

Task: "Component test for user profile display"
Agent: ui-component-tester

Task: "Component test auth flow with mock server"
Agent: ui-component-tester
```

## Notes
- [P] tasks = different files, no dependencies within same phase
- **Backend Phase**: Verify tests fail before implementing (RED-GREEN-REFACTOR)
- **Frontend Phase**: Build against mocks, no RED-GREEN needed for UI components
- **Integration Phase**: Real backend + frontend integration
- Always shutdown mocks when their use is over
- Commit after each task
- Avoid: vague tasks, same file conflicts
- **Phase barriers**: Complete backend fully before frontend, complete frontend before integration

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
   - Each story → ui-component-tester agent: Component test [P] (if frontend)
   - Each story → contract test [P] (via Specmatic MCP)
   - Quickstart scenarios → validation tasks
   - Environment switching → api-mock-manager agent tasks (dev/prod mode)

4. **Ordering**:
   - **Backend Phase**: Setup → Tests (RED) → Models → Services → Endpoints (GREEN) → Integration & Polish (REFACTOR)
   - **Frontend Phase**: Mock setup → Components → Component tests → Mock shutdown
   - **Integration Phase**: Real backend → Frontend reconfiguration → Integration tests → Shutdown all
   - Dependencies block parallel execution within phases
   - Phase completion gates block progression to next phase

## Validation Checklist
*GATE: Checked by main() before returning*

- [ ] All contracts have corresponding Specmatic MCP tests in Backend Phase
- [ ] All entities have model tasks in Backend Phase
- [ ] Backend tests come before backend implementation (RED-GREEN-REFACTOR)
- [ ] Backend completion gate: Contract and resiliency tests must pass before Frontend Phase
- [ ] Frontend phase uses mock servers properly with shutdown when done
- [ ] Integration phase properly coordinates backend startup and frontend reconfiguration
- [ ] Parallel tasks truly independent within each phase
- [ ] Each task specifies exact file path
- [ ] No task modifies same file as another [P] task
- [ ] Mock lifecycle properly managed (startup → use → shutdown)
- [ ] Three-phase barrier dependencies enforced