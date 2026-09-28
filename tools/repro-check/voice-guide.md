# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads

<!-- 2-3 lines. Who is talking when you comment on an issue: your
experience level stated plainly, what you are doing in this repo, what
readers can expect from you. This is the register your rules protect. -->

I am a learner and contributor working through the repository while building my understanding of the project. I may not have all the answers, so I distinguish what I observed from what I think is happening and give enough concrete context for someone else to verify it.

## Rules I write by

<!-- 3-5 rules, drafted from the lecture's slide-12 moment. Each rule
needs a wrong/right pair from your own hand: one line you might
actually have written that breaks the rule, and the line you would
post instead. The pair is what makes a rule executable; a rule without
one is a wish.

Format each rule like this:

### Rule: <short name>

<The rule, one or two sentences.>

- Wrong: "<a line that breaks it>"
- Right: "<the line to post instead>"
-->
Rule: Say what I observed

State the concrete behavior I saw instead of presenting an assumption as a fact.

Wrong: "This is definitely a bug in the parser."
Right: "I reproduced the error when the parser receives this input."
Rule: Be specific about evidence

Point to the relevant command, output, file, or behavior instead of making a vague claim that something "doesn't work."

Wrong: "It doesn't work for me."
Right: "Running python test.py with Python 3.12 produces ValueError: ...."
Rule: Separate reproduction from interpretation

Do not claim that I confirmed the issue when I only observed a related behavior.

Wrong: "I confirmed the issue is caused by the dependency."
Right: "I reproduced the reported error with dependency version 2.4.1; I did not determine whether the dependency is the cause."
Rule: Say when I cannot reproduce it

If the reported behavior does not occur, say so directly rather than changing the conditions until I get a different failure.

Wrong: "The issue is still present, but I got a different error."
Right: "I could not reproduce the reported error using the documented steps and environment."
Rule: Keep the comment useful

Include the information someone needs to understand or verify the result, without filling the comment with unnecessary explanation.

Wrong: "I followed everything and after a bunch of troubleshooting I think maybe there could potentially be an issue here."
Right: "I followed the documented steps and could not reproduce the reported behavior."

## Things I never post

<!-- A short list. Promises you cannot keep, tones you refuse,
shortcuts you know you reach for when tired. The skill quotes this
list back at you when a draft crosses it. -->
- Claims that I reproduced an issue when my evidence shows a different or unrelated failure.
- Statements presented as facts when they are only my guesses or interpretations.
- "Works for me" without saying what environment or steps I used.
- Promises that I will investigate, test, or follow up unless I actually intend and am able to do so.
- A confident conclusion when the evidence is inconclusive.
