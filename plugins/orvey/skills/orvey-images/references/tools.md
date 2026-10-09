# orvey MCP tools, field by field

The server's own descriptions are authoritative (`tools/list`); this is the short map.

## Orient

- `get_studio_info` `topic`: `instructions` (workflows; `name` to read one, `path` for its files), `model_instructions`
  (`model` id or the default), `models`, `frameworks` (24 named ways to say an idea), `presets`, `learnings` (`q`),
  `prompting_guide`.
- `list_folders`, `create_folder` (`name`, `parent`): results go to `MCP / <program> / <task>` unless `folder` is given.

## Make

- `create_images`: `prompt` or `spec` {subject, setting, composition, camera, lighting, style, palette, materials,
  mood, details, text, avoid, keep}; `model`, `aspect` (1:1, 16:9, 9:16, 4:3, 3:4, 3:2, 2:3, 4:5, 5:4, 21:9, 16:10),
  `count`, `purpose` (`draft` cheap, `final` best), `quality`, `tier` (1K/2K/4K), `refs` (image or asset ids; the prompt
  calls them image 1, image 2 ...), `folder`, `wait` (seconds, up to about 50), `dry_run`, `idempotency_key`.
- `create_concepts`: `brief`, `concepts` [{title, idea, prompt, framework, abstraction}] or `ideate: {n}`,
  `diversity: {select: n}`, `per_concept`, `dry_run`, `wait`, `name`.
- `run_experiment`: `base` request + one `vary` axis with values; `per_variant` 2-3. `get_experiment`, `record_verdict`.
- `upload_reference`: base64 or data URL → `ast_` id for `refs` or for `analyze_image kind=compare`.
- `run_graph`: canvases the person built in the studio; `dry_run` first.

## Look and decide

- `wait_for_batch`: `batch_id`, `until` (`done` | `picked`), `timeout`. Returns picks with notes when picked.
- `view_images`: up to 6 `ids`, or `batch_id` with `picked: true` or `keys`.
- `search_images`: `q`, `semantic`, `similar_to`, `folder`, `tag`, `favorite`, `min_rating`, `batch`, `limit`.
- `analyze_image`: `kind` `palette` (free hex + CSS variables), `compare` (free, reference vs `candidate`),
  `describe`, `critique`, `caption` (vision model calls).
- `annotate_image`: `rating` 1-5, `note`, `tags`, `favorite`, `folder`.

## Prompts

- `check_prompt` (free lint), `enhance_prompt` (one text call), `vary_prompt` (one-axis versions).

## The studio view

- `open_studio` (`batch_id` optional) opens the full-screen studio for the person. The view itself uses app-only
  tools (`studio_refresh`, `select_concepts`) that the model does not see.
