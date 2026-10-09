---
name: studio
description: >
  This skill should be used when the user runs the orvey studio command (/orvey:studio in Claude Code) or says "открой студию", "open the orvey studio",
  "хочу сам порисовать", "покажи мои картинки" and wants to work with orvey by hand.
argument-hint: "[batch id]"
metadata:
  version: "1.0.0"
---

# orvey studio

Open the orvey studio for the person.

Use only the orvey tools. If they are not in this session, stop and say how to connect orvey (see "Only through orvey"
in the `orvey-images` skill); never fall back to another image tool, a browser or the website.

1. Call `open_studio` (pass `batch_id` when the arguments or the conversation name a batch or concepts board).
2. In a chat that draws views, the studio opens full screen: a composer with the price in tokens on the button, the feed
   of recent batches, the gallery with search by words or by meaning, and concept boards. Say so in one line and stop;
   generating there is the person's own action.
3. Where the chat cannot draw views (a terminal, Codex), say so and give the short summary the tool returned. Do not
   open the website in a browser for the person; they can open https://orvey.angleford.co themselves if they want.
