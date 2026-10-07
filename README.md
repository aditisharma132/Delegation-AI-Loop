# delegation_ai

Turn any job you do repeatedly into a playbook a local AI agent can run
without you. One agent, plain Markdown playbooks, no orchestrator, no
custom code.

## System map

<img width="1155" height="665" alt="{D269E130-4568-4BDE-98F1-61FE44EBEC3E}" src="https://github.com/user-attachments/assets/408942ba-24bd-4da1-9474-e651f79b441e" />
(markmap.md)

The diagram above is generated from `markmap.md`. To regenerate after the
system changes:

## How it works

The loop has three stages. Each stage is driven by a saved prompt — you
never retype the method, only the job name.

1. **Interview** (`files/01-interview-prompt.md`) — the agent asks you
   one question at a time (minimum eight) about a repeated job: trigger,
   inputs, real step order, decisions and their rules, final checks,
   edge cases, tone, and what a bad version looks like. No files are
   written until you say you are done. Output: `[job-name]/SKILL.md`.
2. **Toolbox** (`files/02-toolbox-prompt.md`) — every reusable output
   (template, script, checklist) is saved into `[job-name]/files/`,
   converted to `[placeholders]` with one filled-in example underneath,
   and linked back into the job's SKILL.md so nothing is built twice.
3. **Proof** (`files/03-proof-prompt.md`) — a Definition of done with
   5–10 checks, each verifiable with external evidence (a source file,
   a loading link, a passing test, a count). The agent must run every
   check and report pass/fail with evidence before showing you anything.

When the agent gets something wrong, you do not fix the output — you fix
the playbook and re-run the job.

## Requirements

- Gemini CLI (`npm i -g @google/gemini-cli`) or any agent that can read
  and edit local files (Claude Code works identically).
- A Google account (free tier) or a Gemini API key.

## Quick start

```powershell
npm install -g @google/gemini-cli
gemini
```

Then, replacing `resume-to-latex` with your own kebab-case job name:

```
@SKILL.md Follow it for job-name: resume-to-latex
```

Answer the interview questions one at a time. When the draft playbook
appears, answer its two closing questions (what did it get wrong / what
did you forget). Then run the job for real and let stages 2 and 3 build
the toolbox and the proof.

## Folder structure

```
delegation_ai/
├── README.md          ← this file
├── SKILL.md           ← the master loop (runs every job)
├── files/             ← the three stage prompts + template + index
└── [job-name]/        ← created by the agent, one per delegated job
    ├── SKILL.md       ← that job's playbook
    └── files/         ← its toolbox, built during stage 2
```

Keep the top level read-only in daily use. New jobs are siblings of
`SKILL.md`, never inside it.

## Rules

- Only delegate jobs you have done at least 3 times and will do again.
- Never save one-off outputs, unapproved drafts, or anything containing
  passwords, API keys, or other people's personal data (resumes, IDs).
- Toolbox files use descriptive names only — no dates, no version numbers.
- If a job produces a wrong result, edit the playbook, then re-run. Do
  not patch outputs in chat.
- Back up this folder (git works well). It *is* the system.

## Troubleshooting

- **Long "Thinking..." stalls (2–5 min, repeatedly):** free-tier
  throttling. Cancel with `esc`, relaunch with the model pinned:
  `gemini -m gemini-2.5-flash`. If it persists, check quota at
  aistudio.google.com/apikey.
- **Agent can't find a file:** run `dir` in the folder; SKILL.md and
  files\ must match the paths referenced inside SKILL.md exactly.
- **Agent jumps straight to writing files:** it skipped the interview.
  Tell it to follow SKILL.md from step 1 and ask the questions first.

## Not yet (deliberately)

- **Orchestrator / custom frontend:** the playbook is the orchestrator.
  Revisit only when jobs run unattended on a schedule or non-technical
  people need to run them.
- **Decision models (Jev/Laya):** reserved for stage 4 — fast routing and
  escalation gates. Only wire one in after a specific decision has been
  executed by the playbook 20+ times and thresholds can be calibrated on
  logged outcomes.
