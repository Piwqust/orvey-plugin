---
name: draw
description: >
  This skill should be used when the user runs the orvey draw command (/orvey:draw in Claude Code) or asks orvey to "нарисуй ...", "draw ...", "generate a
  picture of ..." with a clear idea of the picture. Takes the description as its argument.
argument-hint: "<what to draw> [--aspect 16:9] [--count 2] [--model <name the person said>] [--quick] [--improve]"
metadata:
  version: "1.6.0"
---

# orvey draw

Make the picture described in the arguments with the person's orvey studio. The orvey server's instructions and tool
descriptions are the rules; this is the short path. Use only the orvey tools (see "Only through orvey" in `orvey-images`).

1. **The person's words are the prompt**: `create_images` with the description as they wrote it, in their language. Do
   not translate or add style words; only call attached pictures `image 1`, `image 2`.
2. Options: `--aspect`, `--count` (default 1). `--model` only when the person named the model: send it with
   `person_named_model: true`. `--quick`: `purpose: "draft"`. Otherwise leave `model`, `purpose`, `tier` and `quality` out.
3. `--improve`, or the person asks for a better prompt: `enhance_prompt` with their words and the references in `refs`,
   show the proposal, use it.
4. Unusual request (text in the picture, references, an exact size): `dry_run: true` first; it also shows the price in tokens.
5. Run it with `wait: 40` and an `idempotency_key`. Look at the contact sheet; one sentence per picture on what works.
6. Offer one next step: `edit_image` with the person's words, other ideas (`create_concepts` with `ideate`), or a final.
