# Team Workflow

1. Call `get_context` before starting any task.
2. Implement changes in the product repo.
3. Call `update_graph` after significant decisions or contract updates.
4. Run `validate` in CI before merge.
5. Use `handoff` when passing work to another agent or teammate.
