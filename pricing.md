---
title: Credits & pricing
nav_order: 6
description: "What a PageToVid film costs in credits: plans, packs, AI stills and clips, the per-model price table, and how to check a price before spending."
---

# Credits & pricing
{: .no_toc }

Everything in PageToVid is paid for in **credits**. A rendered film is 40 credits; AI stills and clips
are added on top, priced from what they cost to make. You can ask for any price before you spend
anything.
{: .fs-5 .fw-300 }

1. TOC
{:toc}

## The unit

| What | Credits |
|---|---|
| A rendered film — script, real-browser filming, voice-over, captions, music | **40** |
| An AI still (house image model) | **40** |
| The house AI clip — Veo 3.1 Fast, 8 seconds, 720p, with sound | **311** |
| A clip from a model you name | its price in the [model table](#clip-prices-by-model), per second at the resolution made |
| Re-timing the captions of a finished film (`captions_only`) | free once per paid render, then 40 |
| `list_models`, `quote_cost`, `inspect_page`, `get_storyboard` and every other read | free |

{: .note }
On 27 September 2026 every credit amount was multiplied by 40 at the same value: a film that cost
1 credit now costs 40, a plan that gave 25 credits now gives 1,000, and every balance was converted
in the same moment. Nothing got cheaper or dearer. The finer unit lets a clip be priced from what it
really costs instead of being rounded to whole films.

## Plans

| Plan | Monthly | Billed yearly | Credits | Films | For |
|---|---|---|---|---|---|
| **Free** | $0 | — | 120 once, at sign-up | 3 | trying it, no card needed |
| **Starter** | $19 | $190 | 1,000 a month | 25 a month | solo creators and founders |
| **Pro** | $49 | $490 | 3,000 a month | 75 a month | marketers and small teams |
| **Scale** | $99 | $990 | 8,000 a month | 200 a month | growing teams and high volume |
| **Business** | $299 | $2,990 | 30,000 a month | 750 a month | brands producing every week |
| **Agency** | $999 | $9,990 | 110,000 a month | 2,750 a month | agencies running many brands |
| **Enterprise** | from $2,500 | — | custom | custom | custom volume, invoicing, a named contact |

- **What each plan adds.** Starter adds AI stills and clips. Pro adds the REST generation API,
  video packs (several angles of one page at once) and AI revisions from timestamped notes. Scale
  adds filming pages behind a login. Business and Agency include everything Scale has.
- **Yearly** billing is ten times the monthly price — two months free.
- **Business and Agency** are the same product as Scale at a lower price per film: about $0.40
  and $0.36 a film monthly, $0.33 and $0.30 billed yearly.
- **Enterprise** starts at $2,500 a month for custom volume, invoicing and a named contact:
  write to [hello@pagetovid.com](mailto:hello@pagetovid.com).
- **Free** films carry a "Made with PageToVid" watermark, and end with a 2.5-second "Made with
  PageToVid" sting after their own closing card. Paid plans have neither the watermark nor the sting.
- A website's free allowance is **three films across all free accounts**, however many accounts ask
  for it.
- **AI stills and clips are a paid-plan feature.** On a free plan a scene that asks for one is drawn
  as text instead, and the result says so.

## Credit packs

One-off top-ups that **never expire**, on any plan:

| Pack | Price | Films |
|---|---|---|
| 40 credits | $3.90 | 1 |
| 400 credits | $29 | 10 |
| 2,000 credits | $119 | 50 |
| 8,000 credits | $399 | 200 |

A subscription is cheaper per film; a pack is for a one-off burst. Current prices and features:
[pagetovid.com/pricing](https://pagetovid.com/pricing).

## What a film costs

A film is the render plus every AI visual it generates. Three examples:

**1. A recorded film — 40 credits.** A 30-second ad for a website, filmed on the real site, with
motion-graphic cards between the recordings. No AI visuals.

```text
render                                  40
                                      ────
                                        40 credits
```

**2. A film with two AI stills and one house clip — 431 credits.**

```text
render                                  40
AI still × 2          (40 each)         80
house clip × 1        Veo 3.1 Fast     311
                                      ────
                                       431 credits
```

**3. A film with one Seedance 2.0 clip, 8 s at 720p — 506 credits.** A named model is priced per
second at the resolution it makes; the table below gives Seedance 2.0 at 466 credits for 8 s at 720p.

```text
render                                  40
seedance-2.0 × 1      8 s at 720p      466
                                      ────
                                       506 credits
```

A clip's length follows the scene it fills, so a longer scene asks the model for a longer clip and
costs more. `quote_cost` with the film's `video_id` gives the exact figure for your storyboard.

## Clip prices by model

The house clip is what a scene gets when it names no model. Name a model (`data.model` on a clip
scene, or `model` on a presenter) and the scene is charged that model's price instead.

This table is **generated from the price registry** that the render itself charges from, and is
regenerated on every price change. It is not a second copy of the prices.

| Model | Name | Kind | Credits per second | Example |
|---|---|---|---|---|
| `house` (default) | House clip (Veo 3.1 Fast) | video | flat | 311 (8 s at 720p) |
| `seedance-2.0-mini` | Seedance 2.0 Mini | video | 480p: 16/s · 720p: 31/s | 249 (8 s at 720p) |
| `seedance-2.0-fast` | Seedance 2.0 Fast | video | 480p: 23/s · 720p: 47/s | 373 (8 s at 720p) |
| `seedance-2.0` | Seedance 2.0 | video | 480p: 27/s · 720p: 58/s · 1080p: 144/s · 4k: 303/s | 466 (8 s at 720p) |
| `seedance-2.5` | Seedance 2.5 | video | 480p: 40/s · 720p: 90/s | 718 (8 s at 720p) |
| `wan-3.0-prime` | Wan 3.0 Prime | video | 480p: 26/s · 720p: 54/s · 1080p: 109/s | 435 (8 s at 720p) |
| `minimax-h3` | MiniMax H3 | video | 768p: 31/s · 2k: 50/s | 249 (8 s at 768p) |
| `minimax-h3-max` | MiniMax H3-Max | video | 480p: 19/s · 768p: 31/s | 249 (8 s at 768p) |
| `veo-3.1` | Veo 3.1 | video | 720p: 155/s · 1080p: 155/s · 4k: 233/s | 1242 (8 s at 720p) |
| `veo-3.1-fast` | Veo 3.1 Fast | video | 720p: 39/s · 1080p: 47/s · 4k: 116/s | 311 (8 s at 720p) |
| `house-image` (default) | House still (Gemini image) | image | flat | 40 |
| render | Assembling the film | video | — | 40 |

A model in this table is not necessarily available to your account at this moment: `list_models`
returns only what you can use now, and with `include_unavailable: true` also lists the others with
the reason. The house clip is a flat 311 credits — what `veo-3.1-fast` costs for the same shot, 8 seconds at
720p — and it is always that shot; naming `veo-3.1-fast` lets you choose the length and resolution,
and prices it per second.

## Check a price first

Two MCP tools price anything without spending a credit. Both are free and read-only.

### `list_models` — every model, with its price

```json
{ "name": "list_models", "arguments": { "modality": "video" } }
```

Returns each model's `id`, `display_name`, `capabilities` (lengths, resolutions, aspect ratios, sound,
reference images), `price` (`credits_per_second` per resolution and a worked `example`), and whether
**this account** can use it (`available`, `unavailable_reason`). Pass `"include_unavailable": true`
to see the models you cannot use yet, and why.

### `quote_cost` — one generation

```json
{ "name": "quote_cost",
  "arguments": { "kind": "clip", "model": "seedance-2.0", "duration_s": 8, "resolution": "720p" } }
```

```json
{ "credits": 466,
  "breakdown": [{ "item": "Seedance 2.0 × 1", "credits": 466, "detail": "8 s at 720p, 466 credits each" }],
  "warnings": [] }
```

Leave out `model` for the house clip (always 8 s at 720p, so it takes no length or resolution), use
`"kind": "image"` for a still, `"role": "inset"` for a presenter in a corner (which is made at the
model's cheapest resolution), and `count` (1–4) for several at once.

### `quote_cost` — the next re-render of a film

```json
{ "name": "quote_cost", "arguments": { "video_id": "YOUR_VIDEO_ID" } }
```

Prices the next `rerender_video` of that film: the render plus every AI visual in its storyboard that
has not been made yet. A visual already made is reused at no charge.

### When a request is refused

A resolution or model that is not offered is **refused, never silently changed**. Lengths work like
this: for a model with a fixed menu of lengths, a length between two on the menu is rounded up to the
next one, priced at that length, and the quote says so in `warnings`. A length longer than the model
makes, or outside a model's range, is refused. The refusal names what is offered in `allowed`:

| Code | When | Example `allowed` |
|---|---|---|
| `unknown_model` | the model id is not one this server runs | `["house", "seedance-2.0-mini", …]` |
| `unsupported_option` | an option the model does not take — e.g. a length for the house clip | — |
| `out_of_range` | a length or resolution outside what the model makes | `["480p", "720p"]` or `{ "min": 4, "max": 15 }` |

```json
{ "name": "quote_cost",
  "arguments": { "kind": "clip", "model": "seedance-2.0-mini", "resolution": "1080p" } }
```

```text
out_of_range — Seedance 2.0 Mini does not offer 1080p.   allowed: ["480p", "720p"]
```

## Capping what a render spends

`create_animation` takes an `ai_budget` — `max_clips`, `max_images` and `on_exceed` — and always
returns `ai_plan` with what was asked for and the estimated bill:

```json
"ai_budget": { "max_clips": 1, "max_images": 2, "on_exceed": "fallback" }
```

`refuse` (the default) creates and spends nothing when the storyboard asks for more; `fallback` renders
anyway and generates only up to the ceiling, the other scenes keeping their text; `queue` generates
them all.

## Refunds

- **A render that fails is refunded in full** — the render and every AI visual it had already
  generated. `cancel_video` on a render still running does the same.
- **An AI still or clip that fails is refunded** on its own, and the render carries on: the scene falls
  back to its page still and its text, and `get_video` says so in `warnings` and `ai_report`.
- **A film that misses its own length target** is re-rendered once for free (`get_video` reports
  `length_within_tolerance: false`).
- **A visual already made is never charged again**: re-rendering a storyboard, or moving a presenter
  to another corner, reuses the clips and stills it already has.

## Referrals and shows

- **Referral:** a new account that signs up with your link gets 200 credits once its email is
  verified. You get 200 credits when that account's first film finishes, at most 20 times a month.
  A referral past the 20th still earns commission. An invited account can make 8 free films on a
  website instead of 3, so the extra credits can be spent on the site it came to film.
  The "Make your own" button on a shared film's page carries its maker's link.
- **Commission:** you also earn a cash share of every payment a referred account makes, before tax,
  for as long as it pays: 20% on credit packs and on the Starter, Pro and Scale plans, 10% on
  Business, Agency and Enterprise. Each commission is held for 30 days, the refund window, and can
  be paid out once you have $50.
- **Money or credits:** take your available commission as cash (from $50), or as credits with a
  50% bonus, from the first cent and with no minimum.
- **Insider and Ambassador:** 3 active paying referrals make you an Insider (Starter features and
  Starter's monthly credits, free); 10 make you an Ambassador (Pro features and Pro's monthly
  credits). Each lasts while you keep that many active paying referrals.
- **Shows** (recurring videos from a feed): each episode is an ordinary render, 40 credits.
  `max_credits_per_day` caps a show's daily spend, from 40 to 2,000 credits; the default, 120, is three
  episodes a day.
