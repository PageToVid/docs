---
title: AI clips
parent: Guides
nav_order: 2
description: "Generated video clips in a PageToVid film: where they come from, choosing a model per scene, length, sound, characters, cost control and prompts that work."
---

# AI clips
{: .no_toc }

An AI clip is a few seconds of generated film, with sound, that stands in for a scene the website
cannot show — a person, a place, a feeling, a before. It sits in the film like any other scene: under
the narration and the captions, cut on the same rhythm.
{: .fs-5 .fw-300 }

<video controls preload="none" width="100%" poster="https://pagetovid.com/v/cmuh6r92i0003s61ythly8xol.jpg">
  <source src="https://pagetovid.com/v/cmuh6r92i0003s61ythly8xol.mp4" type="video/mp4">
  <a href="https://pagetovid.com/v/cmuh6r92i0003s61ythly8xol.mp4">Watch the film (MP4)</a>
</video>

1. TOC
{:toc}

## Where clips come from today

Be precise about this, because it is the most common surprise: **pasting a link does not produce
clips.** The automatic planner behind `create_video` films the site and draws motion-graphic cards;
for a beat no page can show it may add an AI **still** (about two per film at most), and it never adds
a clip. A clip is always something you ask for, in one of four ways:

| Where | How | Model |
|---|---|---|
| **Web editor** | A scene's **Video clip** button: describe the shot, and the clip replaces that scene's picture | house clip |
| **`create_animation`** | An `image` scene with `data.generate` (the shot) and `data.clip: true` | house clip, or `data.model` |
| **`update_storyboard`** | `set_visual` a scene to `image` with the same `data`, or `add_scene` with it | house clip, or `data.model` |
| **`generate_asset`** | `kind: "video"` makes one clip straight into your media bank, with no film | house clip |

A clip in your bank goes into any film at no further charge: put its asset id in an image scene as
`data.asset_id`. A **presenter** — a person talking in the corner, over the scene rather than instead
of it — is also a clip, set with `set_inset`; see [A presenter in the corner](presenter).

AI clips are a **paid-plan** feature. On a free plan a clip scene is drawn as text and the render says
so.

## Your first clip scene

Over MCP, turn one scene of an existing film into a clip:

```json
{ "name": "update_storyboard",
  "arguments": {
    "video_id": "YOUR_VIDEO_ID",
    "operations": [
      { "op": "set_visual", "scene_id": "YOUR_SCENE_ID", "visual": "image",
        "data": {
          "generate": "A founder at a kitchen table at dawn, laptop open, coffee steaming. Slow push-in. Warm window light.",
          "clip": true
        } }
    ] } }
```

Then `rerender_video`. The clip is generated during the render, charged when it is made, and kept
on the scene: the next re-render reuses it at no charge. Changing the `generate` text makes a new one.

In a storyboard you write from scratch, the scene looks the same:

```json
{ "visual": "image",
  "heading": "The old way",
  "narration": "Every morning started the same way: forty tabs and no answer.",
  "data": { "generate": "A tired designer rubbing his eyes in front of a wall of browser tabs, blue screen light, slow dolly out.",
            "clip": true } }
```

## Choosing a model per scene

Leave out `model` and the scene gets the **house clip**: Veo 3.1 Fast, 8 seconds at 720p, with sound,
for a flat 311 credits. Name a model and the scene is made by that model and charged its price, per
second at the resolution it makes:

```json
"data": { "generate": "…", "clip": true, "model": "seedance-2.0-mini" }
```

The choice is per scene, not per account: a draft-quality beat can use `seedance-2.0-mini` and the
hero shot `seedance-2.0`. Veo 3.1 Standard (`veo-3.1`) is used only when a scene names it.

- **Which models exist, and which you can use now:** `list_models` (free).
- **What each costs:** the generated table in [Credits & pricing](../pricing#clip-prices-by-model).
- **How the families differ:** [AI models](ai-models).

## Length and resolution

You do not set a clip's length or resolution in a film — they are planned from the shot, within what
the model makes:

- **Length** is how long the scene will be on screen: its narration at about 110 words a minute plus a
  breath, or its `duration_seconds` if it is silent. A model with a fixed menu of lengths gets the
  shortest one that covers the scene. The house clip is always 8 seconds.
- **Resolution** follows how big the clip is drawn: at least 720p (768p on MiniMax) for a clip that
  fills the frame, the model's cheapest tier for a presenter in a corner.
- **A scene longer than the model's maximum** holds the clip's last frame for the rest of the scene,
  and the render says so. Shorten the narration, or pick a model with longer clips.
- **Nothing is silently changed at quote time.** `quote_cost` refuses a length or resolution the model
  does not offer, with the ones it does in `allowed`. During a render, if a model refuses a length it
  advertises, it is asked once more at 5 seconds, the length every model has proven, and `ai_report`
  records it.

## Sound

Every clip is generated with its own sound. Under a narrated scene it plays as a quiet bed beneath the
voice; in a scene with **empty narration** it plays at full volume and carries the scene. A line in
quotation marks inside `generate` is spoken by the person in the shot, and a silent scene is held until
their last word, measured from the clip itself, so nobody is cut off mid-sentence.

## The same face in every clip

A [character](characters) is a name and one to three reference images. Add `data.character` to a
clip scene and those images go to the model with the prompt, so the same person appears in every
shot, whichever model makes it:

```json
"data": { "generate": "Ada walks into a bright co-working space and waves at the camera.",
          "clip": true, "character": "Ada, the founder" }
```

## Site films keep the site

A clip replaces a scene's picture. In a film of a website, the site is the subject, so PageToVid keeps
**at least half of the scenes as real recordings** of the site (one in four in a 9:16 film, never fewer
than two in a film of four scenes or more). The planner builds to that floor and the storyboard review
flags a film that falls below it: add clips in place of drawn cards, not in place of every recording.
Films you write with `create_animation` film no page, so they have no floor — a film can be all clips.

## Writing a clip prompt

A clip is one shot, a few seconds long. Prompts that work describe one:

| Do | Why |
|---|---|
| **One subject, one action.** "A barista slides a cup across the counter." | Several actions in eight seconds come out as a blur of half-actions. |
| **Name the camera move.** Slow push-in, dolly out, handheld follow, static wide. | Without one, most models drift aimlessly. |
| **Name the light and the mood.** Warm morning window light; cold office fluorescents. | It sets the look faster than any adjective. |
| **Say where we are.** A small bakery at opening time; a crowded train. | A subject with no place floats. |
| **Put speech in quotation marks.** He says: "Two minutes, that's all it took." | A quoted line is spoken; keep it short, one sentence. |
| **No on-screen text, logos, UI or brand names.** | Generators draw text badly, and a fake logo or a mangled interface costs trust. Show the real product with a recording; let the clip carry the feeling. |

For the same person across scenes use a character rather than re-describing them: a description drifts
from shot to shot, reference images do not.

## Keeping the cost in hand

- **Price first:** `quote_cost` prices one clip (`kind`, `model`, `duration_s`, `resolution`), or with a
  `video_id` the next re-render of a whole film — render plus every visual not made yet. Free.
- **Cap it:** `create_animation`'s `ai_budget` sets `max_clips` and `max_images` for the render, and
  `ai_plan` in the response shows the bill before anything is made.
- **Draft cheap, finish sharp:** iterate on `seedance-2.0-mini`, then switch the one hero scene to a
  bigger model.
- **Reuse:** a clip already made is kept on its scene and in your bank; re-rendering, moving a
  presenter or using a bank clip via `data.asset_id` costs nothing more.

## When a clip fails

The render never stops for a failed clip. The clip is refunded, the scene falls back to its page still
and its text, and `get_video` says so in `warnings` and `ai_report`, with the model's own reason: a
refusal on content grounds means change the words, a timeout means try again.
