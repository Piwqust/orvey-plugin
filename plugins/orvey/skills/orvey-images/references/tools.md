# orvey MCP tools, field by field

The server's own descriptions are authoritative (`tools/list`); this is the short map.

## Orient

- `get_studio_info` `topic`: `instructions` (workflows; `name` to read one, `path` for its files), `model_instructions`
  (`model` id or the default), `models`, `frameworks`, `presets`, `learnings` (`q`), `prompting_guide`.
- `list_folders`, `create_folder` (`name`, `parent`): results go to `MCP / <program> / <task>` unless `folder` is given.

## Make

- `create_images`: `prompt` (the person's own words, any language), `aspect`, `count`, `refs` (image ids, `ast_` ids,
  data URLs or https links; the prompt calls them image 1, image 2), `ref_files`, `folder`, `name`, `wait`, `dry_run`,
  `idempotency_key`. Leave `model`, `purpose`, `tier`, `quality` out unless the person asked; a model the person named
  goes with `person_named_model: true`.
- `edit_image`: `image_id` (or `file`) + `change` in the person's words; `count` 1-4, `keep_faces`.
- `create_concepts`: `brief`, `shared` (`refs`, `aspect` ...), `ideate` (`n`, default 4; `vary`: `idea` or `style`) or your
  own `concepts`; `diversity`, `per_concept`, `dry_run`, `wait`, `name`.
- `run_experiment`: `base` request + one `vary` axis (`axis`, `values`); `per_variant` 2-3. `get_experiment`, `record_verdict`.
- `upload_reference`: `data` (base64), `url` (https), or `file`; with none of them an `upload_url` for
  `curl -sS -T shot.png '<upload_url>'`. Returns an `ast_` id.
- `run_graph`: canvases the person built in the studio; `dry_run` first.

## Look and decide

- `wait_for_batch`: `batch_id`, `until` (`done` or `picked`), `timeout`.
- `view_images`: up to 6 `ids`, or `batch_id` with `picked: true` or `keys`; `size` 512-1568.
- `search_images`: `q`, `semantic`, `similar_to`, `folder`, `tag`, `favorite`, `min_rating`, `batch`, `limit`.
- `analyze_image`: `kind` `palette`, `compare` (with `candidate`), `describe`, `critique`, `caption`.
- `annotate_image`: `rating` 1-5, `note`, `tags`, `favorite`, `folder`.

## Prompts

- `enhance_prompt` only when the person asks: `prompt`, `refs` (it looks at them), `before` (summaries of earlier
  proposals). The free lint is part of `create_images` `dry_run`.

## The studio view

- `open_studio` (`batch_id` optional) opens the full-screen studio. The view itself uses `studio_refresh` and
  `select_concepts`, which are for the page, not for you.
