---
title: Characters
parent: Guides
nav_order: 3
description: "Keep the same person in every generated clip of a film: create a character from reference images or draw one, then name it in clips and presenters."
---

# Characters
{: .no_toc }

A character is a name, one to three reference images and a short description. Name it in a generated
clip and those images go to the model with the prompt, so the same face comes back in every shot — on
Veo, Seedance or MiniMax alike — instead of drifting from scene to scene.
{: .fs-5 .fw-300 }

![Sam's reference portrait, drawn with create_character](../assets/films/character-sam.jpg){: width="256" }

1. TOC
{:toc}

## Create a character

With the MCP tool `create_character`, in one of two ways.

### From images you already have — free

Pass one to three image URLs that are **media on your account**: a generated still, an asset from your
bank, or a shared asset from `list_commons_assets`.

```json
{ "name": "create_character",
  "arguments": {
    "name": "Ada, the founder",
    "refs": ["https://storage.googleapis.com/…/ada-front.png",
             "https://storage.googleapis.com/…/ada-three-quarter.png"],
    "description": "A woman in her late twenties, platinum blonde bob, grey tee, calm and direct."
  } }
```

### Draw the reference — the price of one still

No images yet? Pass `generate` and PageToVid draws a clean reference portrait (neutral background,
even light, the whole subject in frame) for **40 credits**, refunded if the drawing fails.

```json
{ "name": "create_character",
  "arguments": {
    "name": "Sam, the PageToVid host",
    "generate": "A friendly man in his early thirties, short dark hair, light stubble, navy crew-neck sweater, at a desk in a bright home office, looking into the camera",
    "description": "Sam, a friendly man in his early thirties, talking to camera like a YouTuber."
  } }
```

The drawn portrait lands in your media bank too. If the character is then refused (say, a name longer
than 60 characters), the error gives the portrait's URL: retry with it as `refs` and you are not
charged again.

| Field | Rule |
|---|---|
| `name` | Required, at most 60 characters. Creating a character with an existing name **replaces** it. |
| `refs` | 1 to 3 image URLs on your account. Three is the model's own ceiling for reference images. |
| `generate` | Draws the reference instead; ignored when `refs` is given. |
| `description` | At most 300 characters, added to every clip's prompt so the words and the picture agree. |
| `site_url` | Optional: attach the character to one of your sites. |

`list_characters` shows your characters; the REST API has the same:
`GET` / `POST /api/v1/characters` and `DELETE /api/v1/characters/{name}` — see [REST API](../api).

## Use it in a clip

Add `data.character` to a clip scene, in `create_animation` or `update_storyboard`:

```json
{ "visual": "image",
  "heading": "Ada at work",
  "narration": "Ada used to spend her Mondays on reports.",
  "data": { "generate": "Ada at a standing desk, sighing at a spreadsheet, slow push-in, cool office light.",
            "clip": true,
            "character": "Ada, the founder" } }
```

It works with any model: add `"model": "seedance-2.0-mini"` and Seedance receives the same reference
images. `generate_asset` takes `character` too, to make a single clip or still of the character into
your bank. See [AI clips](ai-clips) for everything else about clip scenes.

## Use it as a presenter

A character can also talk in the corner of the frame while the real site is filmed full-screen — the
classic screen-tutorial layout:

```json
{ "op": "set_inset", "scene_id": "YOUR_SCENE_ID",
  "character": "Sam, the PageToVid host",
  "generate": "Sam at his desk, talking to camera. He says: \"Step one: paste a link.\"" }
```

The full recipe, with a film made that way, is in [A presenter in the corner](presenter).

## Best practices

- **A clear, front-facing reference.** Face the camera, eyes visible, even light, a plain background.
  Add a three-quarter view and a full-body shot as the second and third references if you have them.
- **Simple, distinctive wardrobe.** A navy sweater survives eight shots; a patterned shirt with a
  necklace does not. Put the wardrobe in the `description` too.
- **No text in a reference.** A reference with words in it teaches the model to draw words. To build a
  character from a film you already made, use a scene's `raw_frame_url` from `get_storyboard` — never
  its `thumbnail_url`, which is cut from the finished film with the headline and caption burnt in.
- **One character per clip.** A scene names one `character`; two people in one generated shot is
  where identity drifts first.
- **Short spoken lines, in quotation marks.** `He says: "Two minutes, that's all."` — one sentence per
  clip. A scene with empty narration is held until the character's last word.
- **Describe the action, not the face.** The references carry the face; the prompt should spend its
  words on what the character does, where, and how the camera moves.

## Limits

- Characters are used in **generated clips and stills**, which are a paid-plan feature.
- There is **no character editor in the web app yet**: characters are created over MCP
  (`create_character`) or the REST API (`POST /api/v1/characters`). Once created, a clip made in the
  web editor does not name one — use `update_storyboard` to put a character in a scene.
- At most **three** reference images per character.
