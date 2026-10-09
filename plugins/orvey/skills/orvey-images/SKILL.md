---
name: orvey-images
description: >
  This skill should be used when the user asks to "draw", "generate an image", "make a picture", "come up with options",
  "give me concepts", "moodboard", "a banner / logo / cover / product shot / UI mockup", "нарисуй", "сгенерируй картинку",
  "придумай варианты", "концепты", "обложку", or wants to find, compare, refine or build from pictures made with the
  person's orvey image studio (the `orvey` MCP server of this plugin).
metadata:
  version: "1.0.0"
---

# orvey: pictures through the person's own studio

orvey is the person's image studio on their own provider key. Every picture is a paid request and is kept in their
library. The `orvey` MCP server of this plugin does the work; its tools return ids, signed links and a contact sheet.
Where the chat can draw interactive views (Claude, ChatGPT), results also appear as cards: pictures with progress,
a viewer, and for concepts a choice the person sends back with one button.

## Only through orvey

Every picture of this plugin is made by the person's orvey tools (`create_images`, `create_concepts`, `open_studio` ...),
so it lands in their library, costs their tokens and shows as a card in the chat. If those tools are not in this
session, **stop**: do not draw with another image generator, do not open a browser or the orvey website, do not use
computer control. Say in one line that orvey is not connected and how to connect it:

- ChatGPT / Codex: Settings → Apps → orvey → Connect (or Refresh), then a new chat;
- Claude Code: `/mcp` → orvey → Authenticate; Claude: Settings → Connectors → orvey.

## Pick the route

| The person wants | Do |
|---|---|
| options, ideas, a look, "не знаю, что хочу" | **Concepts** (below) |
| one picture they can describe | `create_images` with `purpose: "draft"`, `count` 2-4, then a final |
| to make or browse pictures by hand | `open_studio` (full-screen studio in the chat; no generation by itself) |
| something made before | `search_images` (add `semantic: true` for "по смыслу") before generating anew |
| to test one idea against another | `run_experiment` (one variable), then `record_verdict` |
| to build a page from a picture | workflow `design-to-code` (`get_studio_info topic=instructions name=design-to-code`) |

## Concepts: many different ideas, then the person chooses

1. Read `get_studio_info` with `topic: "instructions"`, `name: "creative-exploration"`, then `topic: "model_instructions"`
   (the default model is GPT Image 2.5 Sunburst). Write prompts to that guide, in English; text to draw stays in quotes.
2. Write 8-12 genuinely different concepts, each with its own prompt, `title`, `framework` and `abstraction`
   (about 4 abstract, 4 conceptual, 2 literal). Translate ideas into what the eye sees.
3. `create_concepts` with `dry_run: true` first. It costs nothing; the card shows the plan and names near-duplicates.
   Rewrite what it flags (change the idea, not the wording).
4. The same call without `dry_run`, `wait: 40`. Look at the contact sheet once; `view_images` for two or three finalists.
5. Let the person choose. In a chat with cards they tick pictures and press «Отправить агенту»: the choice arrives as
   their message. Otherwise give them `review_url` (works on a phone) and call `wait_for_batch` with `until: "picked"`.
   No person around: pick two or three yourself, furthest apart, and say why.
6. Take the pick forward: `refs: ["<image id>"]` with what to keep, one change at a time; `purpose: "final"`, `count` 1.

## Rules that save money

- `dry_run: true` on anything unusual; it shows the final prompt, the price in tokens and the folder.
- An `idempotency_key` on every call that might be retried: the same key returns the same batch, not a second bill.
- Keep `count` small until an idea works. Never loop without a stopping rule: three rounds without progress means a
  new idea, not new wording.
- Prices are tokens: 1 token = one GPT Image 2.5 Sunburst picture at 2K. Say prices in tokens, not dollars.
- Record what worked: `annotate_image` (rating, note, tags), `record_verdict` with `learnings` for experiments.

## In a terminal (Claude Code, Codex)

The terminal does not draw cards. After a batch, show the person the `review_url` and the contact sheet link, and
describe the pictures from `view_images`. Cards and the studio are drawn only in chats with views (Claude, the
ChatGPT chat). More detail, field by field: `references/tools.md`.
