# Interview Coach

**Practise explaining your own code before a real interviewer asks.** Your AI agent reads your repository and runs a mock technical interview about it. It asks one question at a time, grounded in your actual files, grades your answers honestly and turns the gaps into a study plan.

Built for developers whose portfolio projects were written with AI help: if a project is on your resume, you need to be able to walk through it.

```
You:   /mock-interview
Coach: Mock interview: Takeaway (junior engineer, 6 questions, practice mode)
       Question 3 of 6 (code walkthrough):
       In worker/worker.ts, claimNext() selects a queued item and then updates it
       with .eq("status", "queued") again. Why check the status twice?
You:   …
Coach: Partial. A strong answer covers:
       - two workers could select the same row; the second check makes the claim atomic
       - if the update matches no row, someone else already claimed it
       Study: worker/worker.ts, claimNext()
```

## Install

### Claude Code

```
/plugin marketplace add mb1720827-ui/interview-coach
/plugin install interview-coach@interview-coach
```

Open your project and say **"interview me on this repo"**, or type **`/mock-interview`**.

### Other agents (Codex, Cursor, Gemini CLI…)

> **"Follow https://github.com/mb1720827-ui/interview-coach/blob/main/AGENTS.md and interview me on this repo."**

## What a session covers

| Area | What you're asked |
|---|---|
| Pitch | The 60-second explanation of what it is and who it's for |
| Architecture | How data flows through the system |
| Code walkthrough | Real functions in your files: what they do, and why they're written that way |
| Trade-offs | Why this database, library or pattern, and what else you could have used |
| What-if | Failures, duplicates, attacks: what happens and how you'd debug it |
| Security, testing, scaling | Where data could leak, what's tested, what breaks first |
| Experience | The hardest bug and how you found it |

**Modes:**
- **Practice** (default): feedback after every answer, with "Strong", "Partial" or "Missed", what a strong answer includes, and the file to study. Say "teach me" on any question to learn it from your own code.
- **Realistic:** no feedback until the end, like a real interview.

**At the end:**
- a scorecard by area
- the 3 topics to study first, with files and an exercise
- an honest 60-second pitch for the project
- a list of the parts you couldn't defend

**Progress** is saved in `~/.interview-coach/<repo>.md`, so the next session starts with your weak topics.

## Design

- **Read-only.** The coach never changes your repository.
- **Grounded.** Every code question names a file and function that really exist, and model answers must match your codebase, not a generic tutorial.
- **Honest grading.** Vague answers count as Partial, and the generated pitch can't claim users or numbers the code doesn't support.

## License

MIT
