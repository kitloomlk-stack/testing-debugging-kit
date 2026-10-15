# Testing & Debugging Kit

Test-first development, reliable unit and end-to-end tests, evidence-based root-cause debugging, and real-browser verification, for any language or framework.

A setup for AI coding agents, made by [Kitloom](https://kitloom.site). One source, generated for every major agent: Claude Code, OpenAI Codex, Cursor, Google Antigravity, Gemini CLI, GitHub Copilot, Windsurf (Devin), opencode and Aider.

## Install

1. Download this repository as a ZIP, or use the **Check and download** button on its Kitloom page, which checks it first.
2. Read the files. Nothing here runs on its own: the kit has no hooks and no install scripts.
3. Copy the folders and files you want into the root of your project. `AGENTS.md` is the shared instructions file; edit it to fit your project.

## What is inside

### Skills

- `tdd` — Building a feature or fixing a bug test-first with a red-green-refactor loop.
- `diagnosing-bugs` — Something is broken, throwing, failing or slow and the cause is not obvious yet.
- `debugging-and-error-recovery` — A test fails, a build breaks, or behaviour differs from what was expected.
- `parallel-debugging` — A bug has several plausible causes and you want competing hypotheses tested against evidence.
- `five-whys` — A problem keeps coming back and you need the cause you can fix, not the symptom.
- `e2e-testing-patterns` — Writing or repairing Playwright or Cypress tests, especially flaky ones.
- `browser-testing-with-devtools` — Checking behaviour in a real browser: DOM, console errors, network requests, performance.
- `kiro-verify-completion` — Before saying a fix works, tests pass or a task is done, to back the claim with fresh evidence.

### Commands

Invoke by name (for example `/tdd-cycle`).

- `tdd-cycle` — Implement a described behaviour test-first, one red-green-refactor step at a time.
- `debug` — Investigate a failure to its root cause, then fix it with a regression test.
- `flaky-test` — Diagnose and stabilise an intermittently failing test.

### Sub-agents

- `bug-investigator` — Delegate when a failure needs reproducing and tracing to a root cause without editing code.
- `test-reviewer` — Delegate to review new or changed tests for coverage gaps, brittleness and weak assertions.

### Scoped rules

- `test-files` — Conventions for writing and editing test files.
- `e2e-tests` — Stability rules for end-to-end and browser tests.
- `debugging-discipline` — Always-on rule: find the root cause with evidence before changing code.

## Where each agent finds it

| Agent | Instructions | Skills and commands | Rules | Sub-agents |
|---|---|---|---|---|
| Claude Code | `CLAUDE.md` (imports `AGENTS.md`) | `.claude/skills/` | `.claude/rules/` | `.claude/agents/` |
| OpenAI Codex | `AGENTS.md` | `.agents/skills/` | listed in `AGENTS.md` | `.codex/agents/` |
| Cursor | `AGENTS.md` | `.agents/skills/`, `.claude/skills/` | `.cursor/rules/` | `.claude/agents/` |
| Google Antigravity | `AGENTS.md` | `.agents/skills/` | `.agents/rules/` | `.agents/agents/` |
| Gemini CLI | `AGENTS.md` via `.gemini/settings.json` | `.agents/skills/`, `.gemini/commands/` | listed in `AGENTS.md` | `.gemini/agents/` |
| GitHub Copilot | `AGENTS.md` | `.agents/skills/`, `.github/prompts/` | `.github/instructions/` | `.claude/agents/` |
| Windsurf (Devin) | `AGENTS.md` | `.agents/skills/`, `.windsurf/workflows/` | `.windsurf/rules/` | — |
| opencode | `AGENTS.md` | `.agents/skills/`, `.opencode/commands/` | listed in `AGENTS.md` | `.opencode/agents/` |
| Aider | `AGENTS.md` via `.aider.conf.yml` | — | — | — |

Skills are stored twice (`.agents/skills/` and `.claude/skills/`) because Claude Code reads only its own folder. Agents that read both may list a skill twice; delete the copy you do not need.

## Credits

The skills come from these open-source repositories, each under its own licence. Their licence and a notice are kept beside every copied skill.

| Skill | Source | Licence |
|---|---|---|
| `tdd` | [mattpocock/skills](https://github.com/mattpocock/skills) at `49dd158` | MIT |
| `diagnosing-bugs` | [mattpocock/skills](https://github.com/mattpocock/skills) at `49dd158` | MIT |
| `debugging-and-error-recovery` | [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) at `aeac41d` | MIT |
| `parallel-debugging` | [wshobson/agents](https://github.com/wshobson/agents) at `46891e7` | MIT |
| `five-whys` | [wesammustafa/Claude-Code-Everything-You-Need-to-Know](https://github.com/wesammustafa/Claude-Code-Everything-You-Need-to-Know) at `b97a62b` | MIT |
| `e2e-testing-patterns` | [wshobson/agents](https://github.com/wshobson/agents) at `46891e7` | MIT |
| `browser-testing-with-devtools` | [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) at `aeac41d` | MIT |
| `kiro-verify-completion` | [gotalab/cc-sdd](https://github.com/gotalab/cc-sdd) at `e2a0c67` | MIT |

Everything else in this repository (instructions, rules, commands, sub-agents) is by Kitloom under the MIT licence.

## Use at your own risk

Read every file before you use it. Agent instructions can make an agent run commands on your machine. This kit was checked with Kitloom's pre-download check, which looks for warning signs but cannot prove anything is safe.
