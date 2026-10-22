# Agents Automation

This is a 30-minute conference talk about making agent automation something you can show and defend. The through-line is work already published in the open: a Cursor skill that writes the next Ditectrev blog post by copying a named flavor and refusing a generic layout, a Cursor skill that generates the next Ditectrev book by copying a named template and obeying a few hard rules, and editor hooks that format and test after an agent edits. The audience should leave with a test they can apply to their own work: a good agent demo is a visible workflow with constraints, not a prompt that happens to work once.

### Agents Automation

- 30 minutes, three live demos
- A skill the agent has to follow, rules it cannot improvise, a hook that checks the edit
- Daniel Danielecki
- Repos stay open: [github.com/danieldanielecki](https://github.com/danieldanielecki) and [github.com/Ditectrev](https://github.com/Ditectrev)
- Rough split: about 13 minutes of talk, about 17 minutes of demo. If the book skill runs long, drop the hook demo

### What you should be able to do afterwards

- Point at a repeated agent workflow that is already a file in the repo
- Name the rules an agent is not allowed to improvise
- Put a check around the agent, instead of hoping the last message is correct
- Leave with repos a stranger can open after the talk

### What usually breaks on stage

- The prompt lives in one person's chat history
- The "demo" is a generated file nobody can diff
- A long agent run eats the rest of the slot
- Failure looks like silence: no skill, no rule, no log

### A skill is the workflow

- [Ditectrev/Blog](https://github.com/Ditectrev/Blog) is the open-source blog at [blog.ditectrev.com](https://blog.ditectrev.com)
- The agent artifact is `.cursor/skills/ditectrev-blog/SKILL.md` (`name: ditectrev-blog`)
- It tells the agent how to write the next post: which flavor to copy, where the MDX file goes, and what it must refuse
- Stay in that file. The demo is the skill, not a tour of the site theme

### Demo 1 — The blog skill

- Talk vs demo: live demo, about 6 minutes (6:30–12:30)
- Repo: [Ditectrev/Blog](https://github.com/Ditectrev/Blog)
- File: `.cursor/skills/ditectrev-blog/SKILL.md` (`name: ditectrev-blog`, about 29KB)
- What the audience sees:
  - The skill description: Ditectrev Blog MDX posts, in this repo's nested `data/blog` layout, when creating or updating a post
  - The source table: pick one flavor before writing. Comparison (`graphql-vs-rest`), long API comparison (JavaScript string methods), how-to (`.npmrc`), complete guide (CSS borders), migration (Jetifier / AndroidX)
  - "Do not invent a generic Medium/Substack layout." Do not use this skill for the books/courses README layout
  - Graphic rule: ask what to include before generating anything. Hero is a repo-hosted AVIF at 1400×788. Never generate the graphic first
  - Medium agent rules: after the post is live, Import a story. Never call `api.medium.com`, never ask for `MEDIUM_INTEGRATION_TOKEN`, never add a Medium GitHub Action
- What it proves: the publishing workflow is a file the agent has to follow. It is not inventing a blog post shape
- How to run it:
  - Scroll the source table, then the Medium agent rules. Those two scrolls are the slide
  - If the agent is ready, ask it to start a how-to and stop when it picks the `.npmrc` flavor and refuses the Medium API
  - Do not write a full post or generate a graphic on stage
- Fallback (no network): stay on the source table and the three "never" Medium lines. That scroll is the demo even with no model call and no live site

### Rules the agent must not improvise

- The blog skill says which workflow to copy
- The book skill says which leftovers to refuse, including when an older book still has them
- The next demo is [skills-books](https://github.com/Ditectrev/skills-books)
- The skill says the book is `README.md` and slides live in `__presentation-slides/index.html`. This repo only contains the skill and a README. Do not go looking for a generated book on stage

### Demo 2 — The book skill

- Talk vs demo: live demo, about 7 minutes (14:30–21:30)
- Repo: [Ditectrev/skills-books](https://github.com/Ditectrev/skills-books)
- File: `.cursor/skills/ditectrev-books/SKILL.md` (`name: ditectrev-books`, about 45KB)
- What the audience sees:
  - The skill description: new Ditectrev book, study guide, course, or slides, copied from the SEO / HTML / A11Y / AZ-900 pattern
  - Hard constraints, marked as review rules that override leftovers in older source repos:
    - Link every named tool to its official URL
    - No case-study sections
    - Close every chapter with `Summary: {Exact Chapter Title}`, never a `Conclusion` heading
    - CodeSandboxes only when the book has code snippets (HTML and A11Y yes; SEO and AZ-900 no)
  - The flavor choice: tools-heavy (SEO), hands-on (HTML / A11Y), or study guide (AZ-900). Pick one before writing
- What it proves: the agent is applying a house style. It is not inventing a textbook
- How to run it:
  - Scroll those four constraints. They are the slide
  - If the agent is ready, ask it to start a tools-heavy book and stop when it chooses the SEO flavor and refuses CodeSandboxes
  - Do not generate a full book on stage. The skill file is about 45KB and a full repo will blow the clock
- Fallback (no network): stay in the hard-constraints section. That scroll is the demo even with no model call

### Put a check around the agent

- A skill constrains what the agent writes
- A hook constrains what happens after it writes
- [The Open Stock](https://github.com/Ditectrev/Open-Source-Stock-Application) already has both, next to an app you can open at [theopenstock.com](https://theopenstock.com)

### Demo 3 — Hooks after the agent edits

- Talk vs demo: live demo, about 4 minutes (23:00–27:00). Cut this one first if Demo 2 runs long
- Repo: [Ditectrev/Open-Source-Stock-Application](https://github.com/Ditectrev/Open-Source-Stock-Application)
- What the audience sees:
  - `.cursor/hooks.json`
  - `afterFileEdit` and `afterTabFileEdit` call `.cursor/hooks/after-file-edit.sh` (timeout 180s): Prettier on the edited file, then related Vitest tests
  - `stop` calls `.cursor/hooks/stop-quality-check.sh` (timeout 600s): `format:check`, lint, and unit tests
  - The stop hook records failures and still exits 0. The comment in the script says the hook is observational, so a red suite does not freeze the session
- What it proves: format and tests run because the edit happened, not because the agent remembered
- How to run it:
  - Show `hooks.json`, then the two script headers
  - Do not run the full suite live. The stop hook allows 600 seconds
- Fallback (no network): `hooks.json` on screen, with the two command names readable. No test run

### If the book skill runs long

- Keep Demo 1 and Demo 2
- Use the saved minutes on the hard constraints, then go to the close
- One sentence: the stock app runs Prettier and related Vitest tests from hooks after the agent edits, and the stop hook records failures and still exits 0
- Offer the repo URL verbally

### Where this talk lives

- Talk home: [danieldanielecki/Agents-Automations](https://github.com/danieldanielecki/Agents-Automations). This outline is the README
- Same habit as [JavaScript-Security-Engineering](https://github.com/danieldanielecki/JavaScript-Security-Engineering): the repo is what the audience clones
- A later reveal.js pass can start from [__presentation-slides](https://github.com/Ditectrev/__presentation-slides)
- Slide URLs to leave up:
  - [Blog](https://github.com/Ditectrev/Blog)
  - [skills-books](https://github.com/Ditectrev/skills-books)
  - [Open-Source-Stock-Application](https://github.com/Ditectrev/Open-Source-Stock-Application)

### Close

- A skill is the workflow the agent must repeat
- Hard rules are what the agent must refuse
- Hooks are the checks that run after the agent lets go
- Question to leave them with: which repeated workflow of yours is already written down well enough that an agent should be forbidden from improvising?

### Run of show

- 0:00–2:00 talk — title, and what they should be able to do afterwards
- 2:00–5:00 talk — what usually breaks on stage
- 5:00–6:30 talk — a skill is the workflow
- 6:30–12:30 demo — blog skill (`Blog`)
- 12:30–14:30 talk — rules the agent must not improvise
- 14:30–21:30 demo — book skill (`skills-books`)
- 21:30–23:00 talk — a check after the agent lets go
- 23:00–27:00 demo — editor hooks (`Open-Source-Stock-Application`), or give this block back to the close
- 27:00–30:00 talk — where the talk repo lives, close, and the question

### Prep

- Clone the three demo repos. Open both `SKILL.md` files and `hooks.json` in tabs before the talk
- Pre-scroll Demo 1 to the source table. Pre-scroll Demo 2 to the hard-constraints list
- The blog repo is a maintained fork of a Next.js theme. Stay in `.cursor/skills/ditectrev-blog/SKILL.md`. Do not tour the theme
- Network can fail. None of the three beats need a live model call, a generated graphic, or a test run
- Skip the stock app's full format, lint, and test suite
