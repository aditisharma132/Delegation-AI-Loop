# Prompt 3 — Wire in the proof (definition of done)

## When to use this
Use after the toolbox exists, before the playbook is trusted to run unattended.
Do NOT use as a substitute for actually running the checks — the agent must run them, not assert them.

## The prompt (paste as-is, then replace [job-name])

Add a Definition of done section to SKILL.md for [job-name].

Write between five and ten checks that are specific to this job. Every check must be verifiable with evidence outside your own opinion: a number traced to its source file, a link that loads, a screenshot of the rendered result, a test that runs, a claim matched to a quote, a count, or a value checked against a reference file. No vague quality words like clear, professional or high quality.

From now on, whenever you finish this job, before you show me anything:
1. Run every check.
2. Fix what fails.
3. Run them again.
4. Give me a one-line pass or fail for each check, with the evidence you used.
5. List anything you could not verify, and say why, instead of assuming it passed.

If more than two checks fail on the first pass, stop and tell me which part of the process caused it rather than patching the output.

If you cannot write files yourself, do not pretend you did. Print the complete file contents in the chat, tell me the exact file name and where it goes in the folder, and remind me to replace the old uploaded copy rather than adding a second one.

## Filled-in example (for reference — delete before reuse)
Add a Definition of done section to SKILL.md for weekly-newsletter.

Write between five and ten checks that are specific to this job. Every check must be verifiable with evidence outside your own opinion: the subject line is under 60 characters (evidence: character count), every link loads (evidence: HTTP status 200)...
