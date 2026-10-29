# Acceptance test plan

No application tests have been implemented yet. Experiment 4 Section 6.2 defines AT01–AT13 and their expected evidence.

Prioritise vendor isolation (AT03), atomic mixed-vendor checkout (AT05), competing reservations and duplicate requests (AT06), and failure/expiry/late-event races (AT07). Run concurrency checks against PostgreSQL using independent database connections, not a SQLite-only test setup.

For each implemented test, record the requirement ID, fixture data, preconditions, action and assertion. Keep hypothetical acceptance criteria separate from executed results.
