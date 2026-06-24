# JDBC Client to JPA Refactoring

## Status

Draft implementation contract.

## Objective

Replace direct `JdbcClient` persistence with JPA while preserving observable API, data, transaction, and error behavior.

## Scope

- Map existing relational tables to JPA entities.
- Replace repository queries with Spring Data JPA or explicit JPQL.
- Preserve service interfaces and API payloads.
- Maintain current transaction boundaries and ordering semantics.

## Requirements

1. Existing identifiers, column names, constraints, and indexes remain compatible.
2. Entity relationships must not introduce unbounded eager loading.
3. Queries that depend on ordering must define it explicitly.
4. Updates that require concurrency protection must retain equivalent locking.
5. Empty results and persistence failures must map to existing domain behavior.
6. Database migrations are required for any schema change; automatic schema mutation is not allowed in production.

## Implementation Sequence

1. Characterize current repository behavior with integration tests.
2. Add entities and JPA repositories without changing callers.
3. Migrate one repository operation at a time.
4. Compare generated SQL and query counts for critical paths.
5. Remove `JdbcClient` code only after parity is demonstrated.

## Verification

- Repository integration tests against the supported database
- Service and API regression tests
- Query-count checks for list and relationship-heavy operations
- Concurrency tests for state-changing operations
- Migration and rollback rehearsal when schema changes

## Acceptance Criteria

- Public behavior and persisted data remain compatible.
- No critical path introduces an N+1 query regression.
- Transactional behavior is equivalent or intentionally documented.
- Obsolete JDBC code and configuration are removed.
