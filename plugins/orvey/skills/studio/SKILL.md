---
name: studio
description: >
  This skill should be used when the user runs the orvey studio command (/orvey:studio in Claude Code) or says "открой студию", "open the orvey studio",
  "хочу сам порисовать", "покажи мои картинки" and wants to work with orvey by hand.
argument-hint: "[batch id]"
metadata:
  version: "1.6.2"
---

# orvey studio

Open the orvey studio for the person. Use only the orvey tools (see "Only through orvey" in `orvey-images`).

1. Call `open_studio` (pass `batch_id` when the arguments or the conversation name a batch or concepts board).
2. In a chat that draws views, the studio opens full screen: the person writes, picks the model (their own choice, so it
   is drawn on that model) and generates there themselves, with the price in tokens on the button. Say so in one line and stop.
3. Where the chat cannot draw views (a terminal, Codex), say so and give the short summary the tool returned. Do not open
   the website for the person; they can open https://orvey.angleford.co themselves.
4. If the person then asks you to draw with a model they named, send it with `person_named_model: true`.
