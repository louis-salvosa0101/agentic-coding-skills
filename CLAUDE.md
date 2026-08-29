This repository ships a focused set of engineering skills.

Every skill under `skills/engineering/` or `skills/productivity/` must be listed in the top-level `README.md` and in `.claude-plugin/plugin.json`.

User-invoked skills use `disable-model-invocation: true` and set `policy.allow_implicit_invocation: false` in `agents/openai.yaml`. Model-invoked skills remain discoverable.

Keep retained upstream skill instructions unchanged unless a change is required by the `/setup-skills` rename or the selected-skill set.
