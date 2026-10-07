# Prompt 1 — Turn a repeated job into a playbook (the interview)

## When to use this
Use when you have a job you do repeatedly and want an agent to run it without you.
Do NOT use for one-off tasks, or jobs you have not done at least 3 times yourself.

## The prompt (paste as-is, then replace [job-name])

You are helping me turn a job I do repeatedly into a written playbook you can run without me.

The job is: [describe it in one line].

First, interview me. Ask one question at a time and wait for my answer. Do not write any files until you have asked at least eight questions and I have said we are done. Cover all of this:
- what triggers the job, and how often
- the inputs, and exactly where each one lives
- the steps in the order I really do them
- every decision I make, and the rule behind it
- what I check before I call it finished
- the edge cases that have gone wrong before
- the tone or standard the finished thing has to hit
- what a bad version looks like

When you could run this without me, create a folder called [job-name] and write SKILL.md inside it with these sections: Purpose (one line), When to use this, Inputs, Steps (numbered, plain language, no jargon), Decisions (if X then Y), Definition of done, Edge cases.

Then show me the whole file and ask me two questions: what did you get wrong, and what did I forget to tell you.

## Filled-in example (for reference — delete before reuse)
You are helping me turn a job I do repeatedly into a written playbook you can run without me.

The job is: write the weekly client newsletter for my design studio.

First, interview me. Ask one question at a time and wait for my answer. Do not write any files until you have asked at least eight questions and I have said we are done. Cover all of this:
- what triggers the job, and how often
... (rest identical to the template above)
