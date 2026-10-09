---
name: draw
description: >
  This skill should be used when the user runs the orvey draw command (/orvey:draw in Claude Code) or asks orvey to "нарисуй ...", "draw ...", "generate a
  picture of ..." with a clear idea of the picture. Takes the description as its argument.
argument-hint: "<what to draw> [--aspect 16:9] [--count 2] [--final]"
metadata:
  version: "1.0.0"
---

# orvey draw

Make the picture described in the arguments with the person's orvey studio.

Use only the orvey tools. If they are not in this session, stop and say how to connect orvey (see "Only through orvey"
in the `orvey-images` skill); never fall back to another image tool, a browser or the website.

1. Read `get_studio_info` `topic: "model_instructions"` once per session and write an English prompt (or a `spec`) to
   it: subject, setting, composition, light, style; text to draw in quotes in its own language; what to avoid.
2. Options in the arguments: `--aspect`, `--count` (default 2), `--final` (`purpose: "final"`, `count` 1), `--model`.
   Without `--final` use `purpose: "draft"`.
3. Unusual request (text in the picture, references, an exact size)? `create_images` with `dry_run: true` first and fix
   what it reports.
4. `create_images` with `wait: 40` and an `idempotency_key`. Look at the contact sheet; in one sentence per picture say
   what works and what does not.
5. Offer one next step: a variation of the best (`refs` + what to keep), a different idea, or the final.
