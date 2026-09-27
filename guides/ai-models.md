---
title: AI models
parent: Guides
nav_order: 5
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

Omit `model` and the clip is the **house clip**: Veo 3.1 Fast, 8 seconds at 720p, with sound. Veo 3.1
Standard is used only when a scene names `veo-3.1`.

`list_models` returns every model this account can use right now, with its lengths, resolutions and
price in credits; `include_unavailable: true` adds the others with the reason.

## Available models

Prices are not repeated here: they are in the generated
[model price table](../pricing#clip-prices-by-model), which is regenerated from the price registry on
every price change.

| Model id | Family | Sound | Length | Resolutions | Status |
|---|---|---|---|---|---|
| *(omitted)* | Veo 3.1 Fast (house clip) | yes | 8 s | 720p | default |
| `veo-3.1-fast` | Veo 3.1 Fast | yes | 4, 6 or 8 s | 720p, 1080p, 4K | live |
| `veo-3.1` | Veo 3.1 Standard | yes | 4, 6 or 8 s | 720p, 1080p, 4K | live |
| `seedance-2.0-mini` | Seedance | yes | up to 15 s | 480p, 720p | live, verified |
| `seedance-2.0-fast` | Seedance | yes | up to 15 s | 480p, 720p | available |
| `seedance-2.0` | Seedance | yes | up to 15 s | 480p, 720p, 1080p, 4K | available |
| `seedance-2.5` | Seedance | yes | up to 30 s | 480p, 720p | available |
| `minimax-h3` | MiniMax | yes | 4–15 s | 768p, 2K | live, verified |
| `minimax-h3-max` | MiniMax | yes | 5–15 s | 480p, 768p | live, verified |
| `wan-3.0-prime` | Wan | yes | 2–30 s | 480p, 720p, 1080p | priced, not yet switched on |

In a film, Veo clips are always made at 8 seconds; the other families get a length planned from the
scene, as below.

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

The house clip costs 160 credits on top of the 40-credit render; a named model costs its price in the
[table](../pricing#clip-prices-by-model), per second at the resolution made. `quote_cost` prices any
request first, for free, and refuses a length or resolution the model does not offer rather than
changing it. A clip is refunded if it fails. The
render never stops for a failed clip: the scene falls back to its page still and its text, and
`get_video` says so in `warnings` and `ai_report` — with the model's own reason, such as a refusal on
content grounds (change the words) or a timeout (try again).
