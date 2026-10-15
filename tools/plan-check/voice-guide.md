# Voice guide: how I talk upstream

## Who I am in threads

I am a student contributor reproducing issues for a course assignment.
I am not a maintainer and I am not an expert on this repository, and I
do not write as though I were either. What readers can expect from me
is direct, specific, evidence-based comments that are honest about
what I did and did not reproduce.

## Rules I write by

### Rule: Name the behavior, not just the outcome

Say which issue I ran and what I actually observed, with the specific
symptom. A comment that only announces a result tells the maintainer
nothing they can use.

- Wrong: "I reproduced this."
- Right: "Reproduced on v2.4.1 (macOS 14, Python 3.11): `parse_config()`
  raises `KeyError: 'timeout'` on the sample config in the issue body,
  same as the traceback reported."

### Rule: Claim only what the evidence shows

The conclusion I write has to match the output I paste. If I could not
reproduce it, I say so plainly and include what happened instead, so a
negative result is still usable information.

- Wrong: "Confirmed, this is broken on my machine too."
- Right: "I could not reproduce this on v2.4.1 (Ubuntu 22.04). Running
  the steps in the issue body, the command exits 0 and writes the file
  as expected — output attached. It may depend on something in the
  reporter's environment that I did not match."

### Rule: Promise only what I am actually doing

In a claim comment I commit to the investigation and the reproduction
report, nothing beyond that. I do not offer fixes, timelines, or future
work I have not committed to.

- Wrong: "I'll take this one and have a PR up by the weekend."
- Right: "I'd like to work on reproducing this as part of a course
  assignment. I'll post a reproduction report with my environment and
  results; I'm not claiming a fix yet."

### Rule: Say it once, with the facts attached

Include the setup, the commands, and the result, and stop there. No
apologizing for asking, no restating the issue back to the thread, no
filler around the evidence.

- Wrong: "Hi! Sorry if this is a silly question and I hope I'm not
  bothering anyone, but I've been looking at this for a while and I
  think maybe possibly I might be seeing something similar? Anyway,
  here's what I did, hopefully it helps, thanks so much!"
- Right: "Steps run on v2.4.1 / Node 20.11 / Windows 11:
  `npm ci && npm run build`. Build fails at the bundle step with
  `Cannot find module './locale'` — full log below."

## Things I never post

- Claims that I reproduced a bug when the evidence shows a different
  failure.
- "Same as above" or any piggyback reproduction comment. My proof is my
  own run, in my own words.
- Promises that I will fix the bug.
- Made-up causes, explanations, or details I did not actually observe.
- Boilerplate that does not name the issue-specific behavior.
- Disrespectful or overly casual language.
