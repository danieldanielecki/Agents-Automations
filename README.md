# Agents Automation

This is a 30-minute conference talk about making agent automation something you can show and defend. The through-line is work you already publish in the open: a course-production pipeline and the scripts beside it, a Cursor skill that generates the next Ditectrev book only by copying a named template and obeying a few hard rules, and editor hooks that format and test around an agent. The audience should leave with a test they can apply to their own work: a good agent demo is a visible workflow with constraints, not a prompt that happens to work once.

The public talk repo [danieldanielecki/Agents-Automations](https://github.com/danieldanielecki/Agents-Automations) is empty (created 21 Oct 2026). The three live demos are existing [Ditectrev](https://github.com/Ditectrev) repositories. [Ditectrev/ai-job-search](https://github.com/Ditectrev/ai-job-search) is a fork of [MadsLorentzen/ai-job-search](https://github.com/MadsLorentzen/ai-job-search); leave it out so the talk does not retell that author's story.

Rough split: about 13 minutes of talk, about 17 minutes of demo. If the second demo runs long, drop the third.

### Agents Automation

- 30 minutes, two or three live demos
- From a checklist of scripts to a skill the agent has to follow
- Daniel Danielecki
- Repos stay open: [github.com/danieldanielecki](https://github.com/danieldanielecki) and [github.com/Ditectrev](https://github.com/Ditectrev)

### What you should be able to do afterwards

- Point at a repeated workflow that is already written down
- Name the rules an agent is not allowed to improvise
- Put a check around the agent, instead of hoping the last message is correct
- Leave with a repo a stranger can open after the talk

### What usually breaks on stage

- The prompt lives in one person's chat history
- The "demo" is a generated file nobody can diff
- A long agent run eats the rest of the slot
- Failure looks like silence: no script, no rule, no log

### Start from a pipeline you can read

- [Automation Tools for Courses](https://github.com/Ditectrev/Automation-Tools-for-Courses) is a course-publication process, written as a numbered list
- Maintained entry points are `web-scrap-*.py` and `readme-*.py`
- The rest of the list is still a person: format, proof, publish to GitHub, Udemy, PDF, EPUB, shops
- That list is the spec. An agent that has not read it will invent a different publishing process

### Demo 1 — The course checklist

- Talk vs demo: live demo, about 6 minutes (7:00–13:00)
- Repo: [Ditectrev/Automation-Tools-for-Courses](https://github.com/Ditectrev/Automation-Tools-for-Courses)
- What the audience sees:
  - The README section "Course Publication Process": a long, explicit sequence from source questions to GitHub, Udemy, PDF, and EPUB
  - The short "Maintained scripts" list at the top
  - `readme-udemy.py` opened far enough to show a formatter, not a model
- What it proves: the automation you can audit is the thing an agent should be given
- How to run it:
  - Have the README and `readme-udemy.py` open before you walk on
  - Scroll the process in three beats: collect, format, publish. Do not read all the steps
  - Do not run the scrapers. They hit third-party sites and will not finish inside the slot
- Fallback: the README is the demo. Stay on the numbered process if the editor is slow

### Hand the agent the constraints

- A script tells the machine what to do once
- A skill tells the agent what it must repeat, and what it must refuse
- The next demo is that second artifact: [skills-books](https://github.com/Ditectrev/skills-books)
- The book is `README.md`. Slides live in `__presentation-slides/index.html`, cloned from [__presentation-slides](https://github.com/Ditectrev/__presentation-slides) and never renamed

### Demo 2 — The book skill

- Talk vs demo: live demo, about 7 minutes (16:00–23:00)
- Repo: [Ditectrev/skills-books](https://github.com/Ditectrev/skills-books)
- File: `.cursor/skills/ditectrev-books/SKILL.md` (`name: ditectrev-books`)
- What the audience sees:
  - The skill description: new Ditectrev book, study guide, course, or slides, copied from the SEO / HTML / A11Y / AZ-900 pattern
  - Hard constraints, marked as review rules:
    - Link every named tool to its official URL
    - No case-study sections
    - Close every chapter with `Summary: {Exact Chapter Title}`, never a `Conclusion` heading
    - CodeSandboxes only when the book has code snippets (HTML and A11Y yes; SEO and AZ-900 no)
  - The source table: pick one flavor before writing
- What it proves: the agent is applying a house style. It is not inventing a textbook
- How to run it:
  - Scroll those four constraints. They are the slide
  - If the agent is ready, ask it to start a tools-heavy book and stop when it chooses the SEO flavor and refuses CodeSandboxes
  - Do not generate a full book on stage. The skill file is about 45KB and a full repo will blow the clock
- Fallback: stay in the hard-constraints section. That scroll is the demo even with no model call

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
- Fallback: `hooks.json` on screen, with the two command names readable

### If you only get two demos

- Keep Demo 1 and Demo 2
- Use the saved minute for one sentence: the stock app runs Prettier and tests from hooks after the agent edits, and the stop hook does not block the session
- Offer the repo URL verbally

### Where this talk lives

- Talk home, currently empty: [danieldanielecki/Agents-Automations](https://github.com/danieldanielecki/Agents-Automations)
- Same habit as [JavaScript-Security-Engineering](https://github.com/danieldanielecki/JavaScript-Security-Engineering): the repo is what the audience clones
- Before the conference, this outline can move there. A later reveal.js pass can start from [__presentation-slides](https://github.com/Ditectrev/__presentation-slides)
- Slide URLs to leave up:
  - [Automation-Tools-for-Courses](https://github.com/Ditectrev/Automation-Tools-for-Courses)
  - [skills-books](https://github.com/Ditectrev/skills-books)
  - [Open-Source-Stock-Application](https://github.com/Ditectrev/Open-Source-Stock-Application)

### Close

- Scripts are the pipeline you can read
- Skills are the rules the agent must repeat
- Hooks are the checks that run after the agent lets go
- Question to leave them with: which repeated workflow of yours is already written down well enough that an agent should be forbidden from improvising?

### Run of show

- 0:00–2:00 talk — title, and what they should be able to do afterwards
- 2:00–5:00 talk — what usually breaks on stage
- 5:00–7:00 talk — a pipeline you can read
- 7:00–13:00 demo — course checklist (`Automation-Tools-for-Courses`)
- 13:00–16:00 talk — hand the agent the constraints
- 16:00–23:00 demo — book skill (`skills-books`)
- 23:00–27:00 demo — editor hooks (`Open-Source-Stock-Application`), or give this block back to the close
- 27:00–30:00 talk — where the talk repo lives, close, and the question

### Prep

- Clone the three demo repos. Open the README, `SKILL.md`, and `hooks.json` in tabs before the talk
- Pre-scroll Demo 2 to the hard-constraints list
- Network can fail. None of the three beats need a live model call or a test run
- Skip any live scrape, and skip the stock app's full format, lint, and test suite
