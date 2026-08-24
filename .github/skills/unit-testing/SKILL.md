---
name: unit-testing
description: Unit testing patterns for HTML - test structure, mocking, assertions, and coverage.
---

<!-- AUTHORING RULE: Rules and decision tables only. No narrative prose, no rationale, no ticket refs, no future work. Each section answers "what must I do?" -->

# Unit Testing - HTML

## When to Activate

- Writing tests for new or changed code
- Reviewing test coverage
- Debugging test failures
- After generating or modifying any code

## File Structure

- Location: alongside source as `[FileName].test.ts` or `[FileName].test.tsx`
- Naming: `describe('FeatureName', () => { it('should [outcome] when [condition]') })`
- Pattern: Arrange -> Act -> Assert within each test

## Rules

- Mock all external dependencies: network calls, browser APIs, storage, analytics
- Never make real network calls in unit tests
- Reset mocks between tests - no shared mutable state
- Test happy path, error paths, edge cases, and empty/null inputs
- Cover business logic in game loops, render helpers, and utility modules

## Mocking Network Calls

```ts
jest.mock('../services/apiClient');
const mockApi = jest.mocked(apiClient);
mockApi.request.mockResolvedValue({ data: { ok: true } });
```

## Mocking Browser APIs

```ts
Object.defineProperty(window, 'matchMedia', {
  writable: true,
  value: jest.fn().mockImplementation(() => ({ matches: false })),
});
```

## Mocking Storage

```ts
const storageMock = {
  getItem: jest.fn(),
  setItem: jest.fn(),
  removeItem: jest.fn(),
};
Object.defineProperty(window, 'localStorage', { value: storageMock });
```

## Test Requirements Checklist

- [ ] Happy path covered
- [ ] Each error path covered
- [ ] No real network or platform side-effect calls
- [ ] Mocks reset between tests
- [ ] Assertions verify output/state and user-visible behavior
