# SKILL.md — AI Delegation Loop

## Purpose
Turn any job the user does repeatedly into a playbook an agent can run without them, plus a toolbox of reusable files and a verifiable definition of done.

## When to use this
- Use when the user says they do a job repeatedly and want to delegate it.
- Use when a playbook already exists and the user reports the agent got something wrong — fix the playbook, not the chat.
- Do NOT use for one-off tasks, or for jobs the user has done fewer than 3 times (they don't know their own rules yet).

## Inputs
- The job, described by the user in one line.
- The user's answers to interview questions (collected live, one at a time).
- files/01-interview-prompt.md, files/02-toolbox-prompt.md, files/03-proof-prompt.md (the three stage prompts).
- files/skill-template.md (skeleton for the new job's SKILL.md).

## Steps
1. Paste files/01-interview-prompt.md into the chat and replace [job-name] with a short kebab-case name (e.g. weekly-newsletter).
2. Interview the user: one question at a time, wait for each answer, minimum eight questions. Cover: trigger and frequency; inputs and exactly where each lives; steps in real order; every decision and the rule behind it; final checks; past edge cases; tone or standard; what a bad version looks like.
3. Only after the user says "we are done", create a folder called [job-name] and write SKILL.md inside it using the skeleton in files/skill-template.md.
4. Show the user the whole SKILL.md and ask exactly two questions: what did you get wrong, and what did I forget to tell you. Fold the answers into the file.
5. Run the job once for real. When it produces a script / template / email / checklist the user will need again, paste files/02-toolbox-prompt.md and execute it: save the file into [job-name]/files/ with a descriptive name (no dates, no version numbers), convert specifics to [square-bracket] placeholders with one filled-in example underneath, update the job's SKILL.md to point at the file by name, and add a line to [job-name]/files/INDEX.md.
6. Immediately run the whole job again from scratch. Report which saved files were used and which parts were rebuilt from nothing; propose anything rebuilt as the next toolbox candidate.
7. Paste files/03-proof-prompt.md and execute it: add a Definition of done section with 5–10 checks, each verifiable with external evidence (a source file, a loading link, a rendered screenshot, a passing test, a matched quote, a count, a value checked against a reference file). No vague words like "clear" or "professional".
8. From then on, every run of the job must pass all checks before anything is shown to the user: run every check, fix failures, re-run, report one line pass/fail with evidence per check, and list anything unverifiable instead of assuming it passed.

## Decisions
- If the user has not done the job at least 3 times → stop and say a playbook needs a stable process first; offer to shadow 3 runs instead.
- If an output is one-off, contains a password/API key, or is an unapproved draft → do NOT save it to the toolbox, no exceptions.
- If more than two definition-of-done checks fail on the first pass → stop and report which part of the process caused it; do not patch the output.
- If the agent (this one) cannot write files → do not pretend it did: print complete file contents in chat, state the exact file name and folder location, and remind the user to replace the old uploaded copy rather than adding a second one.
- If the user reports a wrong output in chat → fix the playbook (SKILL.md, toolbox file, or a check), then re-run the job; do not just correct the single output.

## Definition of done
1. A [job-name]/ folder exists containing SKILL.md with all required sections (Purpose, When to use this, Inputs, Steps, Decisions, Definition of done, Edge cases). Evidence: the file is shown in full to the user.
2. The interview covered all eight mandated topics with at least eight questions. Evidence: question log in chat history.
3. The user answered the two closing questions (what did you get wrong / what did you forget) and answers were folded into SKILL.md. Evidence: diff or rewritten sections shown.
4. Every reusable file lives in [job-name]/files/ with a descriptive name, no dates or version numbers, specifics converted to [placeholders] with one filled-in example underneath. Evidence: file listing + one opened file.
5. The job's SKILL.md points at each toolbox file by name and states when to use it and when not to. Evidence: grep the SKILL.md for the file names.
6. [job-name]/files/INDEX.md has one line per saved toolbox asset: name, purpose, date. INDEX.md does not list itself. Evidence: open INDEX.md, compare rows to the asset files excluding INDEX.md.
7. A second from-scratch run used the saved files instead of rebuilding them. Evidence: the run report naming files used vs. rebuilt.
8. Definition of done for the job has 5–10 checks, each with external evidence named, zero vague quality words. Evidence: read the section; any use of "clear/professional/high quality" fails.

## Edge cases
- User tries to skip the interview and paste a job description instead → a pasted description is inputs, not rules; still interview.
- Job inputs live in places the agent cannot access (private inbox, local-only files) → user must move inputs into an agreed location first; record that location in Inputs.
- Toolbox file becomes outdated after a process change → update the file AND the SKILL.md pointer in the same pass, never one without the other.
- User approves a draft that later proves bad → the approval rule stays, but add a new definition-of-done check that would have caught it.
- Two jobs share a template → the template lives in ONE job's files/; the other playbook links to it by relative path and says so.
