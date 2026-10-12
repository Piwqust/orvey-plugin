---
name: draw
description: >
  This skill should be used when the user runs the orvey draw command (/orvey:draw in Claude Code) or asks orvey to "нарисуй ...", "draw ...", "generate a
  picture of ..." with a clear idea of the picture. Takes the description as its argument.
argument-hint: "<what to draw> [--aspect 16:9] [--count 2] [--final] [--improve]"
metadata:
  version: "1.2.0"
---

# orvey draw

Make the picture described in the arguments with the person's orvey studio.

Use only the orvey tools. If they are not in this session, stop and say how to connect orvey (see "Only through orvey"
in the `orvey-images` skill); never fall back to another image tool, a browser or the website.

1. **The person's words are the prompt.** Send the description as they wrote it, in their language, the way a message
   goes to ChatGPT: GPT Image reads it as it is. Do not translate it, expand it or add style words. Only call attached
   pictures `image 1`, `image 2`, and take the shape and size from the options, not from extra words.
2. Options in the arguments: `--aspect`, `--count` (default 1), `--final` (`purpose: "final"`), `--model`. Without
   `--final` use `purpose: "draft"`.
3. `--improve`, or the person asks for a better prompt: call `enhance_prompt` with their words and the references in
   `refs` (it looks at them, makes the words precise and adds nothing of its own), show what it proposes and use it.
   Another call with the earlier summaries in `before` chooses differently where the words leave things open.
4. Unusual request (text in the picture, references, an exact size)? `create_images` with `dry_run: true` first and fix
   what it reports.
5. `create_images` with `wait: 40` and an `idempotency_key`. Look at the contact sheet; in one sentence per picture say
   what works and what does not.
6. Offer one next step: a change to the best (`edit_image` with what to change), other ideas (`create_concepts` with
   `ideate`), or the final.
