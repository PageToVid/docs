---
title: REST API
nav_order: 5
description: "Create and track PageToVid videos over HTTP."
---

# REST API
{: .no_toc }

One POST creates and renders a video; one GET reports progress and returns the files. The full,
interactive reference lives on [pagetovid.com/developers](https://pagetovid.com/developers).
{: .fs-5 .fw-300 }

1. TOC
{:toc}

## Authentication

Create an API key in your [account](https://pagetovid.com/account) and send it as a Bearer token.
A key spends your credits: keep it in your secret manager, never in a repository or a URL.

```http
Authorization: Bearer cp_live_xxxxxxxxxxxxxxxx
```

Base URL `https://pagetovid.com` · a rendered video costs 40 credits — see [Credits & pricing](pricing).

The generation API is included from the **Pro** plan. On Free and Starter, `POST /api/v1/videos`
answers `402` with code `UPGRADE_REQUIRED`. The web app and the [MCP server](mcp/) work on every plan.

## Create a video

```bash
curl -X POST https://pagetovid.com/api/v1/videos \
  -H "Authorization: Bearer $PAGETOVID_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "url": "https://stripe.com",
    "goal": "ad",
    "aspect": "16:9",
    "language": "en",
    "targetSeconds": 30
  }'
```

It returns at once with an id; rendering runs asynchronously and takes a few minutes.

- `aspect` is `16:9`, `9:16`, `1:1` or `4:5`.
- `language` is one of the narration languages below.
- Send an `Idempotency-Key` header to retry safely: for 24 hours the same key returns the same
  render instead of starting and charging a second one. The same key with different parameters is
  refused with `409` and code `IDEMPOTENCY_CONFLICT`.

## Narration languages

Thirteen languages, by code: English `en`, French `fr`, Spanish `es`, German `de`, Italian `it`,
Portuguese `pt`, Dutch `nl`, Arabic `ar` (captions right to left), Hindi `hi`, Korean `ko`,
Polish `pl`, Turkish `tr` and Swedish `sv`.

## Track it

```bash
curl https://pagetovid.com/api/v1/videos/$VIDEO_ID \
  -H "Authorization: Bearer $PAGETOVID_API_KEY"
```

Poll until the status is `done` (or `error`, with the reason). A finished video carries its MP4,
poster and subtitle links, plus `warnings` — read them before you publish.

## Endpoints

| Method | Path | Purpose |
|---|---|---|
| `POST` | `/api/v1/videos` | Create and render a video from a URL |
| `GET` | `/api/v1/videos/{id}` | Status, progress, files and warnings |
| `POST` | `/api/v1/videos/{id}/translate` | The same film in 1 to 6 other languages, one new video each; answers `202` |
| `PUT` `POST` | `/api/v1/uploads/{token}` | Send a file to the address `create_upload` returned (up to 30 MB) — see [Send your own files](guides/your-own-files) |
| `GET` `POST` | `/api/v1/sites` | The sites on your account; add one |
| `GET` | `/api/v1/sites/{domain}` | One site: its films, plan and formats |
| `GET` `POST` | `/api/v1/sites/{domain}/plan` | The site's video plan; generate it |
| `GET` `POST` | `/api/v1/sites/{domain}/plan/videos` | Films in the plan; render them |
| `POST` | `/api/v1/sites/{domain}/plan/code-shots` | Shots authored from a code repository |
| `GET` `PUT` | `/api/v1/sites/{domain}/brand-kit` | The site's brand kit; `PUT` changes only the keys you send (`null` clears one) |
| `GET` `POST` `DELETE` | `/api/v1/sites/{domain}/session` | A capture session for a page behind a login; registering one needs the Scale plan |
| `GET` | `/api/v1/sites/{domain}/formats` | Recurring-video formats for a site |
| `GET` `POST` | `/api/v1/sites/{domain}/shows` | Shows (recurring videos from a feed) |
| `PATCH` | `/api/v1/shows/{id}` | Change a show |
| `POST` | `/api/v1/shows/{id}/run` | Run a show now |
| `POST` | `/api/v1/shows/{id}/webhook` | Signed webhook that triggers an episode |
| `GET` `POST` | `/api/v1/characters` | Recurring characters for generated clips ([guide](guides/characters)) |
| `DELETE` | `/api/v1/characters/{name}` | Remove a character |
| `GET` `POST` | `/api/v1/captures` | Captured screens banked for a site |
| `POST` | `/api/v1/captures/images` | Upload captured images |
| `GET` | `/api/v1/commons` | Shared media others made available |
| `GET` `POST` | `/api/v1/connections` | MCP/HTTP connections a format can read from |
| `DELETE` | `/api/v1/connections/{alias}` | Remove a connection |

Everything the API does, the [MCP server](mcp/) does too — with an assistant writing the storyboard.
