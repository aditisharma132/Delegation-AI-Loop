# SKILL.md — AI Delegation Loop

## Purpose
Turn any job the user does repeatedly into a playbook an agent can run
without them, plus a toolbox of reusable files and a verifiable
definition of done.

## When to use this
- Use when the user says they do a job repeatedly and want to delegate it.
- Use when a playbook already exists and the user reports the agent got
  something wrong — fix the playbook, not the chat.
- Do NOT use for one-off tasks, or for jobs the user has done fewer than
  3 times (they don't know their own rules yet).

## Inputs
- The job, described by the user in one line.
- The user's answers to interview questions (collected live, one at a time).
- files/01-interview-prompt.md, files/02-toolbox-prompt.md,
  files/03-proof-prompt.md (the three stage prompts).
- files/skill-template.md (skeleton for the new job's SKILL.md).

## Steps
1. Paste files/01-interview-prompt.md and replace [job-name] with a short
   kebab-case name (e.g. weekly-newsletter).
2. Interview the user: one question at a time, wait for each answer,
   minimum eight questions. Cover: trigger and frequency; inputs and
   exactly where each lives; steps in real order; every decision and the
   rule behind it; final checks; past edge cases; tone or standard;
   what a bad version looks like.
3. Only after the user says "we are done", create a folder called
   [job-name] and write SKILL.md using files/skill-template.md.
4. Show the whole SKILL.md and ask exactly two questions: what did you
   get wrong, and what did I forget to tell you. Fold answers into the file.
5. Run the job once for real. When it produces a script / template /
   email / checklist needed again, paste files/02-toolbox-prompt.md:
   save into [job-name]/files/ (descriptive name, no dates or version
   numbers), convert specifics to [placeholders] with one filled example
   underneath, update the job's SKILL.md to point at the file by name,
   add a line to files/INDEX.md.
6. Immediately run the whole job again from scratch. Report which saved
   files were used and which parts were rebuilt from nothing; propose
   rebuilt parts as next toolbox candidates.
7. Paste files/03-proof-prompt.md: add Definition of done with 5–10
   checks, each verifiable with external evidence (source file, loading
   link, rendered screenshot, passing test, matched quote, count, value
   against a reference file). No vague words like "clear" or "professional".
8. From then on, every run must pass all checks before anything is shown:
   run every check, fix failures, re-run, report one line pass/fail with
   evidence per check, list anything unverifiable instead of assuming it passed.

## Decisions
- Job done fewer than 3 times → stop; a playbook needs a stable process;
  offer to shadow 3 runs instead.
- Output is one-off, has a password/API key, or is an unapproved draft →
  never save it to the toolbox.
- More than two definition-of-done checks fail on first pass → stop and
  report which process part caused it; don't patch the output.
- Cannot write files → don't pretend: print full contents in chat, give
  exact file name and location, remind user to replace the old uploaded
  copy rather than adding a second one.
- User reports a wrong output → fix the playbook (SKILL.md, toolbox file,
  or a check), then re-run; don't just correct the single output.

## Definition of done
1. [job-name]/ contains SKILL.md with all 7 sections (Purpose, When to
   use, Inputs, Steps, Decisions, Definition of done, Edge cases).
2. Interview covered all eight mandated topics, ≥8 questions.
3. User answered both closing questions; answers folded into SKILL.md.
4. Reusable files in files/, descriptive names, no dates/versions,
   [placeholders] + one filled example.
5. SKILL.md points at each toolbox file by name, with use/don't-use rules.
6. files/INDEX.md has one line per toolbox asset (not itself).
7. Second from-scratch run used saved files instead of rebuilding.
8. Definition of done has 5–10 evidence-backed checks, zero vague words.

## Edge cases
- User pastes a job description instead of answering → a description is
  inputs, not rules; still interview.
- Inputs live somewhere inaccessible → user moves them to an agreed
  location first; record it in Inputs.
- Toolbox file outdated after a process change → update the file AND the
  SKILL.md pointer in the same pass.
- Approved draft later proves bad → keep the approval rule, add a check
  that would have caught it.
- Two jobs share a template → it lives in ONE job's files/; the other
  playbook links by relative path and says so.
