# Unit 3 — Fix Plan

## Branch Name
`fix/12-python-sqlalchemy-bug`

## Diagnosis
- **Issue**: Database connection timeout and session leak when handling concurrent transactions in SQLAlchemy repository layer.
- **Location**: `src/database/repository.py` inside the `commit_transaction` method.
- **Root Cause**: The session rollback handler fails to properly close the scoped session when an integrity error is raised, leaking open connections under load.

## Proposed Fix
1. Modify `src/database/repository.py` to wrap database transactions in a robust `try...finally` block.
2. Ensure `session.remove()` is explicitly invoked in the `finally` clause to release connection pool resources immediately upon failure.

## Test Plan
1. Run the local reproduction suite to confirm the failure:
   ```bash
   pytest tests/test_repository.py -k "test_concurrent_transactions"
