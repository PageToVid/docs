---
title: Recipes
parent: Guides
nav_order: 6
description: "Complete MCP conversations for the common PageToVid jobs."
---

# Recipes
{: .no_toc }

Each recipe is what you would say to an assistant connected to PageToVid, followed by the tool calls
it makes. You never have to write the calls yourself — they are shown so you know what to expect and
what to ask for.
{: .fs-5 .fw-300 }

1. TOC
{:toc}

## A 30-second ad for a website

> Make a 30-second vertical ad for stripe.com, for founders. Lead with "Get paid in minutes".

1. `get_account` — plan, credits, what is available.
2. `inspect_page` `url: https://stripe.com` `aspect_ratio: 9:16` — what the camera can point at, in
   the phone layout.
3. `create_video` `url` · `goal: ad` · `aspect_ratio: 9:16` · `target_seconds: 30` ·
   `focus: "Audience: founders. \"Get paid in minutes\""`.
4. `get_video` until `done`, then read `warnings`.
5. `get_storyboard` — check each shot frames something different and at least one does something.

## Fix one scene without starting over

> Scene 3 shows the footer while the voice talks about pricing — point it at the pricing table.

1. `get_storyboard` — find scene 3's `scene_id`.
2. `inspect_page` — find the pricing table's selector.
3. `update_storyboard` `set_shot` `scene_id` `selector` `action: spotlight`.
4. `rerender_video` — 40 credits (a render); only what changed is filmed again.

## Correct one figure

> The chart says 40% but it should be 45%.

`get_storyboard` → `update_storyboard` `set_data` with the scene's whole `data`, figure corrected →
`rerender_video`.

## A film from data, with no website

> Turn these quarterly numbers into a 20-second chart video.

`list_motions` → `create_animation` with scenes you write: a `chart` with the points, a `bignum` for
the headline figure, a `titlecard` to close. Each narrated scene lasts as long as its words.

## A presenter walking through your product

> Put a presenter in the corner who explains how to use the site, like a YouTuber. No narrator.

`create_character` → `create_video` → `update_storyboard` with `set_shot` (different, active shots),
`rewrite_narration ""` and `set_inset` (the line in quotation marks) per scene → `rerender_video`.
The full walk-through is in [A presenter in the corner](presenter).

## Generated clips, a model per scene

> Make the opening shot cinematic with Seedance, and keep the rest filmed from the site.

`update_storyboard` `set_visual` `image` with `data: { clip: true, model: "seedance-2.0-mini",
generate: "…" }` → `rerender_video`. See [AI models](ai-models).

## Re-time captions only

> The subtitles are a little behind the voice.

`rerender_video` `captions_only: true` — no new take, free once per render.

## Recurring videos from a feed

> Every time I publish a blog post, make a 30-second video of it.

`create_format` (the shape of every episode) → `validate_format` (free) → `create_show` with the
feed → `preview_episode` (free) → the show runs on its schedule, never renders the same item twice,
and holds its first episode until you confirm it.
