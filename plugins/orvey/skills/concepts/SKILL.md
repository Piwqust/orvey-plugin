---
name: concepts
description: >
  This skill should be used when the user runs the orvey concepts command (/orvey:concepts in Claude Code) or asks for "10 вариантов", "разные концепты",
  "разные идеи", "different directions", "a moodboard" for one brief with orvey. Takes the brief as its argument.
argument-hint: "<brief: what it is for, what is fixed>"
metadata:
  version: "1.6.2"
---

# orvey concepts

Run the concepts route for the brief in the arguments. The orvey server's instructions and the `create_concepts`
description are the rules; this is the short path. Use only the orvey tools (see "Only through orvey" in `orvey-images`).

1. No brief? Ask in one sentence what the pictures are for and what is fixed. Otherwise do not ask.
2. `create_concepts` with `brief` (the person's words), the references in `shared.refs`, `ideate: {n: 4}` (`vary: "style"`
   when they ask for different looks) and `dry_run: true`. Leave `model`, `purpose`, `tier` and `quality` out; a model the
   person named goes with `person_named_model: true`.
3. Read the dry run: the takes, near-duplicates, `estimate.tokens` and `wallet`. Fix what it flags.
4. The same call without `dry_run`, with `wait: 40`, a `name` and an `idempotency_key`: it draws the ideas the dry run showed.
5. Say in two lines what the takes are and how to choose: tick pictures in the card and send, or open `review_url`.
   Then `wait_for_batch` `until: "picked"` (`timeout` 40, at most five times).
6. When the choice arrives, say what the picks share and offer the next step: a refined picture from the pick (`refs`),
   an experiment, or a final.
