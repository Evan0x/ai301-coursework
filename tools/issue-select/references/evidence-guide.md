# Evidence Guide for Repro-Check

This guide maps out where each kind of proof must reside in a reproduction package and defines what constitutes acceptable evidence.

1. **Environment Details**: Must include OS version, runtime/SDK version (e.g., Python/Node.js version), and dependency lockfiles. Lives in the top-level description or `env.txt`.
2. **Reproduction Steps**: A numbered, chronological sequence of deterministic commands or UI actions that trigger the bug from a clean state. Lives in `reproduction.md` or the primary issue comment.
3. **Observed vs. Expected Output**: Exact terminal error logs, stack traces, or screen recordings demonstrating failure, paired with the specification of what should have happened. Lives in the evidence section or attached logs.
4. **Verification of Fix/Workaround**: Terminal output or test run demonstrating that the proposed patch resolves the error without regression.
