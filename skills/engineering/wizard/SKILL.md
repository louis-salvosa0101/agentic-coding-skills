---
name: wizard
description: Generate an interactive bash wizard that walks a human through steps only they can perform. Use when provisioning infrastructure, setting up credentials or CI secrets, walking an unfamiliar third-party dashboard, or running a one-off migration or cutover. Don't invoke this for steps the agent can perform itself.
---

# Wizard

A **wizard** is a bash script that walks a human, step by step, through a manual procedure that's tedious to do by hand and tedious to re-explain to an AI every time. It opens each URL, says exactly what to click and copy, captures the values, writes them where they belong (`.env`, GitHub secrets), confirms at every stage, and shows how many stages are left. It might configure third-party services, run a one-off migration, or move the project from one state to another.

The delightful UX is already solved by [template.sh](template.sh): stage-by-stage progress, confirmation gates, cross-platform URL opening (including WSL), hidden secret entry, idempotent `.env` upserts, `gh secret`/`gh variable` writes, and a closing summary. **Your job is only to scope the procedure and author its stages.** The library above the `STAGES` marker is identical in every wizard; that consistency is the point: never hand-edit it.

A wizard is ephemeral by default: built for one run, saved to a scratch or `scripts/` path, deleted when the job's done. Commit it only when the user wants a repeatable setup path that should live in the repo.

## Process

### 1. Scope the procedure

Work out every manual step the human must take and every value that gets captured along the way. Read the repo first, don't ask cold:

- For setup: `.env`, `.env.example`, `.env.*`, `README`, `docker-compose*`, framework config, and `.github/workflows/*` (every `secrets.*` / `vars.*` reference is a value the wizard must produce).
- For a migration or transition: the current state, the target state, and the irreversible actions between them.

Then show the user the ordered list of stages and values to confirm.

### 2. Generate the script

Copy `template.sh` to your output location (e.g. `scripts/setup-<feature>.sh`). Keep everything above `# ── STAGES ──` untouched. Author the stages below:

```bash
# ── STAGES ──
TOTAL_STAGES=3
banner "Setup Stripe Integration"

stage "Stripe API Key"
step "Open API keys dashboard"
open_url "https://dashboard.stripe.com/apikeys"
step "Create a new secret key named 'development'"
ask_secret "Paste the secret key (starts with sk_test_)" STRIPE_SECRET_KEY
write_env STRIPE_SECRET_KEY "$STRIPE_SECRET_KEY"

stage "Webhook Secret"
step "Add local endpoint http://localhost:3000/api/webhooks"
ask_secret "Paste the signing secret (starts with whsec_)" STRIPE_WEBHOOK_SECRET
write_env STRIPE_WEBHOOK_SECRET "$STRIPE_WEBHOOK_SECRET"

summary
```

### 3. Make executable and guide the human

Make the script executable (`chmod +x scripts/setup-<feature>.sh`) and instruct the human on how to run it in their shell.
