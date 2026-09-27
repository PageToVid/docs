---
title: What's new
nav_order: 7
description: "Everything added to PageToVid's MCP server and API in September 2026, with the tool that does each."
---

# What's new
{: .no_toc }

PageToVid's MCP server grew from 38 to 73 tools in September 2026. This page lists what was added
and which tool does it. Every tool is documented in the [tool reference](mcp/tools.md), which is
generated from the server itself.

1. TOC
{:toc}

## Know the price before you spend

- **`list_models`** lists every clip and still model with what it can do and its price in credits.
- **`quote_cost`** prices one generation, or the next re-render of a video, and spends nothing.
- **`dry_run: true`** on `create_video`, `create_animation`, `rerender_video` and `generate_asset`
  returns the quote instead of starting anything.
- **`max_credits`** on the same tools refuses with `budget_exceeded` before anything is charged.

See [Credits & pricing](pricing.md).

## Choose the model, or let PageToVid choose

- Name a model per clip (`model`), or use **`model: "auto"`** with
  **`optimize`**: `quality`, `balanced`, `speed` or `cost`. The reason for each choice comes back
  in `models_used`.
- Clip controls, sent only where the model accepts them: `duration_s`, `resolution`,
  `aspect_ratio` (including 21:9), `first_frame` and `last_frame`, `seed`, `negative_prompt`,
  `camera` and `shot`.
- **`best_of: 2–4`** generates several candidates, grades each one, and keeps the best.
  Every candidate is charged.

## Films that fix themselves

- A number is never split across two captions, long silences are trimmed, and a caption that
  would leave the frame is recut.
- **`quality_gate`** on `create_video` and `rerender_video` can hold a film under a score.
  **`release_video`** publishes a held film.
- **`ai_mode`** on `create_video`: `none`, `assist`, or `rich`, where the planner may add AI stills
  and clips within `ai_budget`.

## Sound and languages

- **`translate_video`** makes the same film in up to six languages. Quotes stay word for word,
  numbers are formatted for each language, and filmed scenes are re-recorded on the site's own
  localised page where it has one.
- **Per-scene voice, speed and emotion** (`set_scene_voice`).
- **`pronunciations`**: a lexicon for the voice only. Captions keep the written form.
- **`[pause 500ms]`** markers in narration become real silence.
- **`list_voices`** includes a real sample of every voice in every language.
- Arabic (captions right to left), Hindi, Korean, Polish, Turkish and Swedish narration.
- **`upload_asset`** brings your own logo, footage or music; use a track with
  `music: "asset:<id>"`.

## One storyboard, every format

- **`outputs`**: `16:9`, `9:16`, `1:1` and `4:5` from one storyboard, each shape as a sibling
  video.
- **`draft: true`**: a free, low-resolution preview marked DRAFT, rate-limited.
- **`callback_url`**, **`set_webhook`** and **`rotate_webhook_secret`**: a signed event when a
  render ends.

## Reuse instead of paying twice

- **Objects** (`create_object`, `import_objects`, `list_objects`, `update_object`,
  `delete_object`): a product, logo or place, reused in every generation.
- **Scene library** (`save_scene`, `list_scenes`, `copy_scene`, and the storyboard operation
  `add_scene_from_library`): a finished scene with its footage, reused at no AI cost.
- **Characters** gained `update_character` and `delete_character`.
- **Undo**: `list_revisions` and `restore_revision` put a storyboard back as it was before any
  edit.

## Brand and defaults

- **`set_brand_kit`** and **`get_brand_kit`** hold a site's logo, colours, font (including an
  uploaded one), watermark, and default voice, music and look.
- **`set_account_defaults`** sets your own defaults.
- Every option resolves from account to brand kit to format to video to scene, and
  `get_storyboard` shows where each value came from.
- **`list_options`** returns every choice in one call.

## Frames and timeline

- **`get_timeline`** gives the exact start and end of every scene, the words, and the music.
- **`get_frames`** returns stills of the finished film.

## Teams

- **Members, roles and site scopes:** `invite_member`, `list_members`, `update_member`,
  `remove_member`.
- **One wallet** per workspace, with a monthly cap per member.
- **Review links** for people without an account (`create_review_link`).
- **Approvals:** `request_approval`, `approve`, `request_changes`.
- **Comments and an audit log:** `list_comments`, `add_comment`, `get_audit_log`.
- Seats per plan: Pro 3, Scale 5, Business 15, Agency unlimited.
