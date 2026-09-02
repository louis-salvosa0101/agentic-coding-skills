---
name: resolving-merge-conflicts
description: "Use when you need to resolve an in-progress git merge/rebase conflict."
---

1. **See the current state** of the merge/rebase. Check git history, and the conflicting files.

2. **Find the primary sources** for each conflict. Understand deeply why each change was made, and what the original intent was. Read the commit messages, check the PRs, check original issues/tickets.

3. **Resolve each hunk.** Preserve both intents where possible. Where incompatible, pick the one that better serves the destination state of the codebase. Never blindly choose `ours` or `theirs` without understanding intent; if intent is unclear, ask the user before proceeding.

4. **Run relevant tests.** After resolving all hunks, run the test suite (or the subset that covers the conflicting areas). All tests must pass before the merge/rebase is marked complete.

5. **Verify the result.** Check that the resolved code compiles/type-checks and that the intended behaviour from both branches is present in the result.

6. **Complete the merge/rebase.** Stage the resolved files and continue (`git merge --continue` or `git rebase --continue`). Write a commit message that describes what was merged and any non-trivial resolution decisions made.
