---
name: storyboard
description: >
  This skill should be used when the user runs the orvey storyboard command (/orvey:storyboard in Claude Code) or asks
  for "раскадровка", "раскадровку для видео", "разложи на кадры", "кадры для клипа / рилс / рекламы", "storyboard",
  "shot list", "keyframes for Kling / Veo / Seedance" with orvey. Takes the script or the idea of the video as its argument.
argument-hint: "<the script, the idea, the voice-over or the lyrics; length and format if known>"
metadata:
  version: "1.6.2"
---

# orvey storyboard

A video planned into shots, one frame per shot with the same people, plus a board and prompts for a video model. The
orvey server's workflow `storyboard` and the `create_concepts` description are the rules; this is the short path. Use
only the orvey tools (see "Only through orvey" in `orvey-images`).

1. No script? Ask in one sentence what happens in the video. Otherwise do not ask. Keep the person's words as `brief`,
   unchanged: the planner stages what they say and adds no characters, brands or text.
2. Pictures of the characters, places or the product: `upload_reference` each, pass them in `shared.refs` and name them in
   `storyboard.ref_names` ("Аня", "кафе").
3. `create_concepts` with `brief`, `storyboard: {seconds, aspect, look, genre}` and `dry_run: true`. A product or app video,
   a feature launch, text overlays, an end card: `genre: "motion"` (motion design: the brief's on-screen text drawn
   verbatim, one idea per frame, a fixed design system). A video to follow ("в стиле этого ролика"): make contact sheets
   of it (frames every 0.5 s, 4x4 a sheet, each with its time; ffmpeg does it with its fps, scale and tile filters), `upload_reference` them and pass
   `storyboard.example: {refs, seconds, name}`. `aspect` 9:16 for Reels,
   Shorts and TikTok, 16:9 otherwise; `look: "film"` (frames for image-to-video, the default) or `"sketch"` when they want
   a classic pencil storyboard. Leave `model` out. Frames go at 1K, the cheapest; `storyboard.tier: "2K"` or `"4K"` only when the person asks.
4. Show the shots in a short list (number, size, seconds, the action, the line) with the price (`estimate.tokens`). Apply
   what the person changes (`storyboard: {id, shots: [...]}` keeping each shot's `id`).
5. Draw: `create_concepts` with `storyboard: {id}` and `wait: 40`; then `wait_for_batch` with the storyboard id until it is
   done. A sample frame goes first, the others follow it so the people stay the same.
6. Look at the board image. Redraw a weak frame with `storyboard: {id, redo: [n]}`.
7. Hand over `links.page` (edit and redraw in the studio), `links.board_pdf`, and each shot's `video` prompt with its frame
   as the start image for Kling, Veo, Seedance or Runway.
