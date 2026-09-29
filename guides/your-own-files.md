---
title: Send your own files
parent: Guides
nav_order: 7
description: "Film with your own logo, photos, footage, music, fonts and slide decks: create_upload, upload_asset and the Media bank."
---

# Send your own files
{: .no_toc }

A logo, a product photo, a few seconds of footage, a music track, a brand font or a slide deck is
yours to film with. Send it once and it goes into your media bank, where any scene can use it.
{: .fs-5 .fw-300 }

1. TOC
{:toc}

## What you can send

| Kind | Limit | Where it goes |
|---|---|---|
| Picture | 20 MB | an image scene, as `data.asset_id` |
| Clip | 60 seconds | an image scene, as `data.asset_id` |
| Music | 30 MB per send | the film's music, as `music: "asset:<id>"` |
| Font (WOFF2, WOFF, TTF, OTF) | 2 MB | the brand kit, as `font_asset_id` |
| Slide deck (PDF or PowerPoint) | first 40 slides | slides, each with its text and pictures |

One send takes up to **30 MB**. The kind is read from the file's bytes. Sending the same file twice
returns the asset you already have. Uploading is free.

## From an assistant: `create_upload`

Ask your assistant to use a file you gave it. It calls `create_upload`, which returns an address
that works for one hour, and sends the file there with one command:

```bash
curl -sS -T logo.png "<upload_url>"
```

The answer is the new asset, with its id and a line saying how to use it. The address is itself the
credential: it names your account, so treat it like a key until it expires.

A small file (up to 2 MB) can go inline instead, with `upload_asset` and `data_base64`.
`upload_asset` also takes a public `https` URL, which is the way for a video over 30 MB.

## Slide decks

Send a PDF or a PowerPoint file (`kind: "deck"`, or let the bytes decide) and every slide comes back
with its title, its text and its pictures, which are added to your bank.

- **PDF:** each slide becomes one image, exactly as designed, plus its text.
- **PowerPoint:** the pictures placed on each slide, its text and its speaker notes. The slides
  themselves are not drawn; export the deck as PDF if you want an image of each slide.

That is enough to write the storyboard: one slide, one scene, with the slide's picture as the
scene's `data.asset_id`. Only the first 40 slides are read.

## In the web app

The **Media bank** page has an **Add a file** box. Drop a picture, a clip, music, a font or a deck on
it, up to 30 MB. It uses the same upload address as an assistant, so a deck comes back as slides.

Then press **Copy for your AI assistant**. It copies the new ids in a sentence you can paste into any
chat. That is the way in for an assistant that cannot send a file itself.
