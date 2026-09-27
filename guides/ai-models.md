---
title: AI models
parent: Guides
nav_order: 3
description: "Which model makes a generated clip, chosen per scene: Veo, Seedance and MiniMax."
---

# AI models
{: .no_toc }

A generated clip — a scene's own clip or a presenter in the corner — is made by the model **the scene
names**. The choice is per scene, not per account: one beat can use a fast draft model and the next a
premium one.
{: .fs-5 .fw-300 }

1. TOC
{:toc}

## Choosing a model

Set `model` on an image scene's data (with `clip: true`), or on `set_inset`:

```text
update_storyboard  video_id: …
  set_data  scene 1  data: { "clip": true, "model": "seedance-2.0-mini",
                             "generate": "Cinematic close shot: morning light across a wooden desk…" }
```

Omit `model` and the clip is made by **Veo**, the house model.

## Available models

| Model id | Family | Sound | Length | Resolutions | Status |
|---|---|---|---|---|---|
| *(omitted)* | Veo 3.1 | yes | 4, 6 or 8 s | 720p | default |
| `seedance-2.0-mini` | Seedance | yes | up to 15 s | 480p, 720p | live, verified |
| `seedance-2.0-fast` | Seedance | yes | up to 15 s | 480p, 720p | available |
| `seedance-2.0` | Seedance | yes | up to 15 s | 480p–4K | available |
| `seedance-2.5` | Seedance | yes | up to 30 s | 480p, 720p | available |
| `minimax-h3` | MiniMax | yes | 4–15 s | 768p, 2K | live, verified |
| `minimax-h3-max` | MiniMax | yes | 5–15 s | 480p, 768p | live, verified |
| `wan-3.0`, `wan-3.0-prime` | Wan | yes | 2–30 s | up to 1080p | coming soon |

## What PageToVid asks the model for

You do not set a clip's length or resolution — the request is planned from the shot:

- **Length:** as long as the scene will be on screen (its narration, or its silent hold), within what
  the model can make. A clip that outlasts its scene costs a moment nobody sees; one shorter than its
  scene would freeze on its last frame, which is what this avoids.
- **Resolution:** the cheapest tier for a presenter in a corner (a quarter of the width never shows the
  difference), and at least 720p (768p on MiniMax) for a clip that fills the frame.
- **A length the model only advertises** is never asked for below the length proven on a live job; if
  a model refuses a length, it is asked again once at the proven one.
- **A character's face** goes to the model as its reference images, so a named character is the same
  person on Seedance or MiniMax as on Veo.

![Three Seedance 2.0 Mini clips from the film on the home page](../assets/films/seedance-scene-0.jpg)

## Cost and failures

A generated clip costs 4 credits on top of the 1-credit render, and is refunded if it fails. The
render never stops for a failed clip: the scene falls back to its page still and its text, and
`get_video` says so in `warnings` and `ai_report` — with the model's own reason, such as a refusal on
content grounds (change the words) or a timeout (try again).
