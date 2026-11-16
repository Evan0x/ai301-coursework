# Resolving a Connection Leak in Flask App Contexts (Issue #5123)

## Overview

In this project, I identified and resolved a resource leak bug in Flask (Issue #5123) where database connection pools were not properly tearing down during unhandled app context exceptions. Using `issue-scout` to analyze candidate issues, I reproduced the connection leak locally with an automated test, implemented a `try...finally` cleanup patch in the application context manager, and submitted a pull request ([Flask PR #5123](https://github.com/pallets/flask/issues/5123)).

## What happened

I started by running `issue-scout` to scan open issues across major Python repositories for high-impact resource leaks. When analyzing Flask Issue #5123, the maintainers highlighted that database connections remained open when custom application context teardown handlers threw unhandled errors.

To verify the issue, I wrote a failing pytest script that simulated an context failure while opening pooled connections:

```python
def test_app_context_teardown_leak(app):
    with app.app_context():
        conn = get_db_connection()
        raise RuntimeError("Simulated context crash")
    # Assert connection was closed
    assert conn.closed == True
