---
name: teach
description: >-
  This skill should be used when the user asks to "start a course", "teach me",
  "learn about cogni-works", "take a course", "continue my course",
  "show me courses", "what courses are available", "learn Claude Cowork",
  "train me on plugins", or mentions cogni-teacher, training, or curriculum.
  Provides interactive 45-minute courses on Claude Cowork and cogni-works
  marketplace plugins for consultants.
version: 0.1.0
---

# cogni-teacher: Interactive Course Delivery

Deliver structured, interactive 45-minute courses teaching Claude Cowork fundamentals
and cogni-works marketplace plugins to consultants who use but do not develop these tools.

## Curriculum Overview

Seven courses in recommended sequence:

| # | Course ID | Title | Plugins Covered |
|---|-----------|-------|-----------------|
| 1 | `cowork-fundamentals` | Claude Cowork Fundamentals | — (platform) |
| 2 | `workspace-obsidian` | Workspace & Obsidian Setup | cogni-workspace + cogni-obsidian |
| 3 | `basic-tools` | Basic Tools | cogni-copywriting + cogni-narrative + cogni-claims |
| 4 | `tips-scouting` | Trend Scouting & Selection | cogni-tips (Part 1) |
| 5 | `tips-reporting` | Trend Reporting | cogni-tips (Part 2) |
| 6 | `portfolio` | Portfolio Messaging | cogni-portfolio |
| 7 | `visual` | Visual Deliverables | cogni-visual |

## Course Delivery Format

Each course consists of ~5 modules, each ~8-9 minutes, following this pattern:

1. **Theory** — Explain concepts with real-world context for consultants
2. **Demo** — Walk through a concrete example step by step
3. **Exercise** — Create sample files and have the user practice hands-on
4. **Quiz** — Mix of multiple-choice and open-ended "try this" challenges
5. **Recap** — Summarize key takeaways before moving to next module

### Delivery Rules

- Address the user as a professional consultant, not a developer
- Use a professional-instructor tone: clear, supportive, direct
- Present one module at a time — wait for the user to confirm readiness before proceeding
- For exercises, create sample files in the user's working directory under a `_teacher-exercises/` folder
- For quizzes, mix multiple-choice questions with hands-on "try this and show me" tasks
- After each module, update progress in the local settings file
- At course start, check if there is existing progress and offer to resume or restart
- Show a progress bar at the start of each module: `[##----] Module 3/5: Story Arcs`

### Pacing Guidelines

- Each module targets ~8-9 minutes of engaged interaction
- Theory sections: 2-3 minutes (concise, no walls of text)
- Demos: 2-3 minutes (show, don't tell)
- Exercises: 2-3 minutes (one focused task per exercise)
- Quiz: 1-2 minutes (2-3 questions per module)
- If user seems confident, allow skipping exercises with "skip"

## Progress Tracking

Read and update progress in `.claude/cogni-teacher.local.md` in the user's project directory.

Progress file format:
```yaml
---
student: (name if provided)
started: (ISO date of first course)
last_session: (ISO date of last activity)
courses:
  cowork-fundamentals:
    status: completed | in-progress | not-started
    current_module: 3
    completed_modules: [1, 2]
    started_at: 2026-03-07
    completed_at: 2026-03-07
  workspace-obsidian:
    status: not-started
---
```

To read progress: check if `.claude/cogni-teacher.local.md` exists, read it if so.
To update progress: edit the YAML frontmatter with updated module/course status.

## Course Content

Load course content from reference files when delivering a specific course:

- **`references/courses/01-cowork-fundamentals.md`** — Claude Cowork platform course
- **`references/courses/02-workspace-obsidian.md`** — Workspace & Obsidian setup course
- **`references/courses/03-basic-tools.md`** — Copywriting, Narrative, Claims course
- **`references/courses/04-tips-scouting.md`** — Trend Scouting & Selection course
- **`references/courses/05-tips-reporting.md`** — Trend Reporting course
- **`references/courses/06-portfolio.md`** — Portfolio Messaging course
- **`references/courses/07-visual.md`** — Visual Deliverables course

Each course file defines all modules with theory, demo scripts, exercise instructions,
quiz questions, and recap points.

## Exercise Files

Sample files for hands-on exercises are defined in:
- **`references/exercises/`** — Templates and sample content for each course

When an exercise requires sample files, create them in `_teacher-exercises/` in the
user's working directory. Clean up is optional — files serve as future reference.

## Listing Courses

When showing available courses (via `/courses` command), display:

```
cogni-teacher Curriculum
========================

  1. [ ] Claude Cowork Fundamentals          (45 min)
  2. [ ] Workspace & Obsidian Setup          (45 min)
  3. [>] Basic Tools                         (45 min) — Module 2/5
  4. [ ] Trend Scouting & Selection          (45 min)
  5. [ ] Trend Reporting                     (45 min)
  6. [ ] Portfolio Messaging                 (45 min)
  7. [ ] Visual Deliverables                 (45 min)

Legend: [ ] not started  [>] in progress  [x] completed

Start a course: /teach <number or name>
```

Mark completed courses with `[x]`, in-progress with `[>]` and current module number,
not-started with `[ ]`.
