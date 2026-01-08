---
description:
  Build a feature from natural language description or existing spec file,
  automatically generating all artifacts and implementing the feature end-to-end.
---

The user input can be provided directly by the agent or as a command argument -
you **MUST** consider it before proceeding with the prompt (if not empty).

User input:

$ARGUMENTS

This command provides a streamlined workflow that automatically handles the
entire feature development process from specification to implementation.

## Input Detection

1. **Check if user provided a file path**:
   - If input looks like a file path (e.g., `spec.md`, `feature.md`, `./docs/my-feature.md`), 
     read that file as the specification
   - If file doesn't exist, treat input as natural language description

2. **Check for existing spec in current directory**:
   - Look for `spec.md`, `feature.md`, `specification.md` in current directory
   - If found and user didn't specify a different file, use the existing spec

3. **Otherwise, treat input as natural language description**:
   - Create spec from the description

## Execution Flow

### Phase 1: Specification (if needed)

If no spec file exists or user provided natural language:

1. If user provided natural language description:
   - Create a concise spec.md in current directory (or feature directory if detected)
   - Use project conventions and existing codebase patterns
   - Include: Overview, Functional Requirements, User Stories, Data Model (if applicable)

2. If user provided spec file path:
   - Read and validate the spec file
   - Use it as-is, or enhance if clearly incomplete

### Phase 2: Planning

1. Analyze the specification:
   - Understand functional and non-functional requirements
   - Identify entities, services, endpoints, or components needed
   - Review existing codebase structure and patterns

2. Read project constitution (if exists):
   - `.specify/memory/constitution.md` or `.cursor/rules/*.mdc` files
   - Apply project conventions and principles

3. Generate implementation plan:
   - Determine tech stack and architecture decisions
   - Design data model (if applicable)
   - Define API contracts (if applicable)
   - Create quickstart/integration scenarios (if applicable)

### Phase 3: Task Breakdown

1. Generate actionable tasks:
   - Setup tasks: Dependencies, configuration
   - Test tasks [P]: Contract tests, integration tests
   - Core tasks: Entities, services, controllers, endpoints
   - Integration tasks: Database, middleware, external services
   - Polish tasks [P]: Unit tests, documentation, optimization

2. Order tasks by dependencies:
   - Setup → Tests → Core → Integration → Polish
   - Mark parallelizable tasks with [P]
   - Ensure TDD approach (tests before implementation)

### Phase 4: Implementation

1. Execute tasks in order:
   - **Setup**: Initialize project structure, add dependencies
   - **Tests**: Write test files first (TDD)
   - **Core**: Implement entities, services, controllers
   - **Integration**: Wire up database, middleware, external services
   - **Polish**: Add unit tests, documentation, optimizations

2. Follow project conventions:
   - Read `.cursor/rules/*.mdc` files for coding standards
   - Follow existing codebase patterns
   - Apply database conventions (JPA, QueryDSL, etc.)
   - Follow API conventions (controller, service, repository patterns)

3. Progress tracking:
   - Report progress after each major phase
   - Mark completed tasks
   - Handle errors gracefully with clear messages

### Phase 5: Validation

1. Verify implementation:
   - All tasks completed
   - Tests pass
   - Code follows project conventions
   - Feature matches specification

2. Report completion:
   - Summary of implemented features
   - Files created/modified
   - Test results
   - Next steps or follow-up recommendations

## Behavior Rules

- **Auto-detect context**: If in a feature branch or feature directory, use that context
- **Respect existing code**: Don't overwrite existing implementations without explicit request
- **Follow conventions**: Always read and apply project rules from `.cursor/rules/`
- **TDD approach**: Write tests before implementation when applicable
- **Incremental progress**: Report progress at each phase
- **Error handling**: If any phase fails, stop and report with clear error message and suggestions

## File Structure

If creating new feature structure:
- Create feature directory if needed (or use current directory)
- Save spec.md, plan.md, tasks.md for reference
- Implement code following existing project structure

## Examples

**Natural language input:**
```
/build 사용자 주문 기능을 추가해줘. 주문 생성, 조회, 취소 기능이 필요하고, 
주문은 상품 목록과 총 금액을 포함해야 해.
```

**Spec file input:**
```
/build ./docs/order-feature.md
```

**Existing spec in current directory:**
```
/build
```
(Will automatically find and use spec.md in current directory)

