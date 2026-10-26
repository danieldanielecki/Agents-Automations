# Agents Automations

This is a 30-minute conference talk about how to automate repeated work with AI agents, and how to choose a tool you can actually demo. Cursor is one tool. The through-line is the artifact a stranger can open: a hook file in a repo, a saved trigger plus a prompt, or a vendor's public workflow. The audience should leave able to point at that artifact, and unwilling to treat a chat that happened to work once as a demo.

### Agents Automation

- 30 minutes. Two live demos, plus one optional demo to cut if time slips
- How to automate repeated work, and how to choose a tool the room can see
- Daniel Danielecki
- Talk home: [danieldanielecki/Agents-Automations](https://github.com/danieldanielecki/Agents-Automations). This outline is the README
- Rough split: about 13 minutes of talk, about 14 minutes for the two live demos, about 3 minutes for the optional third

### What you should be able to do afterwards

- Sort a repeated job into a hook, a cloud agent, or a schedule or event
- Point at the file or screen a stranger would open to see why it ran
- Refuse a stage demo that only exists in one person's chat
- Leave with this repo, plus the vendor pages on the last slide

### What usually breaks on stage

- The prompt lives in one person's chat history
- The demo waits on a cloud run that does not finish
- The automation only exists in a private repo the room cannot open
- Failure looks like a spinner: no file, no trigger, no log

### How to choose a tool you can demo

- A hook is a script the agent does not have to remember. The audience sees a file. No model call required
- A cloud coding agent is a task in its own environment. The audience sees a branch, a diff, or a pull request. A live run is a bad use of the slot
- A scheduled or event automation is a trigger plus a prompt you save once. The audience sees that saved setup. Do not wait for the next fire
- If the only proof is a private screen, say so, and do not pretend the talk repo contains it

### The landscape

- [Cursor Cloud Agents](https://cursor.com/docs/cloud-agent) run in isolated VMs, clone the repo, and can open a pull request. Start one from the desktop Cloud dropdown, [cursor.com/agents](https://cursor.com/agents), Slack `@cursor`, or an `@cursor` comment on a GitHub pull request or issue, or a Bitbucket pull request. They were formerly called Background Agents. Cursor's docs say Free and Plus do not include them
- [Cursor Automations](https://cursor.com/docs/cloud-agent/automations) run those cloud agents on a schedule or on events from GitHub, GitLab, Bitbucket Cloud, Slack, Linear, Sentry, PagerDuty, and webhooks. Create one in the Agents Window, at [cursor.com/automations](https://cursor.com/automations), with the `/automate` skill, or from a Marketplace template. An automation can attach no repository, one, or several. Slack and cron default to no repository unless you attach one
- [Cursor Hooks](https://cursor.com/docs/hooks) are commands in `hooks.json`, at the project or user level. They can format after an edit, gate a shell call, or run when the agent stops. Cloud agents run `.cursor/hooks.json` from the repo once the environment is writable. Cursor's docs say it can also load Claude Code hooks
- [Claude Code](https://code.claude.com/docs/en/hooks) has its own hooks. [Cloud scheduled tasks](https://code.claude.com/docs/en/routines), formerly routines, run on Anthropic's cloud on a schedule, an API call, or a GitHub event, from [claude.ai/code/routines](https://claude.ai/code/routines) or `/schedule`, on Pro, Max, Team, and Enterprise. The [GitHub Action](https://code.claude.com/docs/en/github-actions) `anthropics/claude-code-action` runs on `@claude` or on a workflow `prompt`, including a cron schedule
- [GitHub Copilot cloud agent](https://docs.github.com/en/copilot/concepts/agents/coding-agent/about-coding-agent) researches a repo, plans, edits, and can open a pull request. You assign an issue, start it from the agents panel, or mention `@copilot` on a pull request. [Copilot automations](https://docs.github.com/en/copilot/concepts/agents/cloud-agent/about-automations) run that agent on an hourly, daily, or weekly schedule, or when an issue is created, a pull request is opened, or a pull request receives new commits. GitHub's docs say those automations are not available in public repositories
- [Codex Cloud](https://learn.chatgpt.com/docs/cloud) runs a task in an isolated environment and lets you review the diff and open a pull request while the computer sleeps. The [Codex GitHub Action](https://learn.chatgpt.com/docs/github-action) is `openai/codex-action`. [ChatGPT scheduled tasks](https://learn.chatgpt.com/docs/automations) run on a schedule, or, on eligible web and mobile plans, from a Gmail, Slack, or GitHub event. Desktop tasks that need local files need the computer on and the app running

### Demo 1 — A hook in a public repo

- Talk vs demo: live demo, about 7 minutes (8:30–15:30)
- Repo: [Ditectrev/Open-Source-Stock-Application](https://github.com/Ditectrev/Open-Source-Stock-Application)
- This is not a product tour. The stock app is only a public repo that already has the hook. Stay in `.cursor/`
- What the audience sees:
  - `.cursor/hooks.json`
  - `afterFileEdit` and `afterTabFileEdit` call `.cursor/hooks/after-file-edit.sh` (timeout 180s): Prettier on the edited file, then related Vitest tests
  - `stop` calls `.cursor/hooks/stop-quality-check.sh` (timeout 600s): `format:check`, lint, and unit tests
  - The stop hook records failures and still exits 0. The comment in the script says the hook is observational, so a red suite does not freeze the session
- What it proves: format and tests run because the edit happened, not because the agent remembered
- How to run it:
  - Show `hooks.json`, then the two script headers
  - Do not run the suite. The stop hook allows 600 seconds
  - Do not start an agent
- Fallback (no network): the three files are already open. No model call and no test run

### A trigger you can open again

- A hook watches the edit. An automation watches the clock or an event
- The next demo is a Cursor screen, not a file in this talk repo
- Say that plainly before you switch windows
- The same shape exists elsewhere: Claude Code scheduled tasks, Copilot automations (private or internal repos only), and ChatGPT scheduled tasks. You will not click those today unless the optional demo fits

### Demo 2 — Cursor Automations, no repo

- Talk vs demo: live click-through, about 7 minutes (17:00–24:00)
- There is no automation file in [Agents-Automations](https://github.com/danieldanielecki/Agents-Automations). The demo is the Automations UI at [cursor.com/automations](https://cursor.com/automations), or the same flow in the Agents Window
- What the audience sees:
  - Getting started, from the docs, matched on screen: choose a trigger, write a prompt, choose optional tools, choose no repository or one or more, then save and activate
  - One scheduled trigger (a preset or a cron expression) and one GitHub trigger (pull request opened)
  - The defaults worth saying out loud: Slack and cron start with no repository; a source-control trigger requires one; opening a pull request is a tool and is on by default for repo-backed automations
  - The three Cursor-managed cards on that page: Bugbot, Security Agents, and PR Routing & Approval. Point at the names. Do not open a run
- What it proves: the repeated job is a saved trigger plus a prompt, not a chat you have to remember
- How to run it:
  - Be logged in before you walk on. Land on an existing automation or the new-automation form
  - Do not save a new automation, and do not wait for a cloud agent. Automations bill as cloud agent usage and will eat the slot
- Fallback (no network): the Automations docs are already open on Getting started and Triggers. If [cursor.com/automations](https://cursor.com/automations) does not load, read those two lists. No cloud run

### Demo 3 — A vendor workflow, optional

- Talk vs demo: live scroll, about 3 minutes (24:00–27:00). Cut this first if Demo 1 or Demo 2 runs long
- Repo: [anthropics/claude-code-action](https://github.com/anthropics/claude-code-action). Anthropic's public examples, not a repo you maintain
- What the audience sees:
  - [`examples/claude.yml`](https://github.com/anthropics/claude-code-action/blob/main/examples/claude.yml): the job runs only when an issue, comment, or review contains `@claude`, then uses `anthropics/claude-code-action@v1`
  - [`examples/issue-triage.yml`](https://github.com/anthropics/claude-code-action/blob/main/examples/issue-triage.yml): on `issues: [opened]`, the prompt is `/label-issue`, and the job timeout is 10 minutes
- What it proves: the same idea is a workflow file in a vendor repo. Cursor is not the only place it can live
- How to run it:
  - Scroll the `on:` block in `claude.yml`, then the `prompt` in `issue-triage.yml`
  - Do not trigger Actions. The example needs an API key, and a run will not finish in the slot
- Fallback (no network): both YAML files are already open locally. No Actions run

### If time slips

- Keep Demo 1 and Demo 2
- Give the 24:00–27:00 block to the close
- One sentence: Anthropic publishes the same pattern as `examples/claude.yml` in [claude-code-action](https://github.com/anthropics/claude-code-action)
- Offer that URL verbally

### Where this talk lives

- Talk home: [danieldanielecki/Agents-Automations](https://github.com/danieldanielecki/Agents-Automations). The outline is the thing the audience clones
- The hook demo is a different public repo. The Automations demo is a Cursor screen. The optional demo is Anthropic's repo
- Slide URLs to leave up:
  - [Cursor Automations](https://cursor.com/docs/cloud-agent/automations)
  - [Cursor Hooks](https://cursor.com/docs/hooks)
  - [Claude Code scheduled tasks](https://code.claude.com/docs/en/routines)
  - [Copilot automations](https://docs.github.com/en/copilot/concepts/agents/cloud-agent/about-automations)
  - [Codex scheduled tasks](https://learn.chatgpt.com/docs/automations)

### Close

- A hook is a file that runs because the agent edited
- An automation is a trigger plus a prompt you can open again
- Choose the one a stranger can see without your chat history
- Question to leave them with: when this job runs next week and you are not in the chat, where would a stranger look to see why it ran?

### Run of show

- 0:00–2:00 talk — title, and what they should be able to do afterwards
- 2:00–5:00 talk — what usually breaks on stage
- 5:00–8:30 talk — how to choose, and the landscape
- 8:30–15:30 demo — hook file (`Open-Source-Stock-Application`)
- 15:30–17:00 talk — a trigger you can open again
- 17:00–24:00 demo — Cursor Automations, click-through, no repo
- 24:00–27:00 demo — Claude Code workflow files, or give this block to the close
- 27:00–30:00 talk — where the talk repo lives, close, and the question

### Prep

- Open `.cursor/hooks.json` and the two hook scripts in tabs. Do not open the stock app itself
- Be logged in to Cursor. Open [cursor.com/automations](https://cursor.com/automations) and the Automations docs on Getting started before you walk on
- Open `examples/claude.yml` and `examples/issue-triage.yml` from a local clone of [anthropics/claude-code-action](https://github.com/anthropics/claude-code-action)
- Network can fail. None of the three beats need a live model call, a cloud run, or a test run
- Do not save a new Cursor automation. Do not run the stock app's format, lint, and test suite. Do not start a GitHub Actions run
