---
name: concepts
description: >
  This skill should be used when the user runs the orvey concepts command (/orvey:concepts in Claude Code) or asks for "10 вариантов", "разные концепты",
  "different directions", "a moodboard" for one brief with orvey. Takes the brief as its argument.
argument-hint: "<brief: what it is for, what is fixed>"
metadata:
  version: "1.0.0"
---

# orvey concepts

Run the concepts route of the `orvey-images` skill for the brief in the arguments.

Use only the orvey tools. If they are not in this session, stop and say how to connect orvey (see "Only through orvey"
in the `orvey-images` skill); never fall back to another image tool, a browser or the website.

1. If the brief is missing, ask in one sentence what the pictures are for and what is fixed (subject, aspect, text,
   brand colours). Otherwise do not ask; assume sensible defaults and state them.
2. Load `get_studio_info` `topic: "instructions"` `name: "creative-exploration"` and `topic: "model_instructions"`.
3. Write 10 different concepts (about 4 abstract, 4 conceptual, 2 literal), each with `title`, `framework`,
   `abstraction`, an English prompt written to the model guide, and `idea` in the person's language.
4. `create_concepts` with `dry_run: true`, fix every near-duplicate it names, then run it for real with `wait: 40`,
   a `name` in the person's language and an `idempotency_key`.
5. Tell the person in two lines what the ten directions are, and how to choose: tick pictures in the card and press
   «Отправить агенту», or open `review_url` on a phone. Then `wait_for_batch` `until: "picked"` (`timeout` 40, repeat
   while they are choosing, at most five times).
6. When the choice arrives, say what the picked pictures share and offer the next step: a refined draft from the pick
   (`refs`), a one-variable experiment, or a final.
