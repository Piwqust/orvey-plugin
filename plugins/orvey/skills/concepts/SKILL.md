---
name: concepts
description: >
  This skill should be used when the user runs the orvey concepts command (/orvey:concepts in Claude Code) or asks for "10 вариантов", "разные концепты",
  "разные идеи", "different directions", "a moodboard" for one brief with orvey. Takes the brief as its argument.
argument-hint: "<brief: what it is for, what is fixed>"
metadata:
  version: "1.2.0"
---

# orvey concepts

Run the concepts route of the `orvey-images` skill for the brief in the arguments.

Use only the orvey tools. If they are not in this session, stop and say how to connect orvey (see "Only through orvey"
in the `orvey-images` skill); never fall back to another image tool, a browser or the website.

1. If the brief is missing, ask in one sentence what the pictures are for and what is fixed (subject, aspect, text,
   brand colours). Otherwise do not ask; assume sensible defaults and state them.
2. Look at the references. Decide what varies: what the brief leaves open (default: the pose, the moment, the framing)
   or the **look** (when the person asks for styles or looks: one picture, different looks). Never ideas from outside the
   brief, never a look nobody gave.
3. Either let orvey write them: `create_concepts` with `brief` (the person's words), the references in `shared.refs`
   and `ideate: {n: 4}` (add `vary: "style"` for looks), `dry_run: true` first. Or write them yourself after reading
   `get_studio_info` `topic: "instructions"` `name: "creative-exploration"` and `topic: "model_instructions"`: what is
   fixed, the given look word for word at the start of every prompt (none if nobody gave one), faces large, each take
   with `title`, `idea` in the person's language and `abstraction`.
4. Fix every near-duplicate the dry run names (change the take, not the wording), then run it for real with `wait: 40`,
   `tier: "2K"` when faces matter, a `name` in the person's language and an `idempotency_key`.
5. Tell the person in two lines what the takes are, and how to choose: tick pictures in the card and press
   «Отправить агенту», or open `review_url` on a phone. Then `wait_for_batch` `until: "picked"` (`timeout` 40, repeat
   while they are choosing, at most five times).
6. When the choice arrives, say what the picked pictures share and offer the next step: a refined draft from the pick
   (`refs`), a one-variable experiment, or a final.
