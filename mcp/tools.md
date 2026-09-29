---
title: Tool reference
parent: MCP server
nav_order: 3
---

# Tool reference
{: .no_toc }

Every tool the PageToVid MCP server publishes — **74 tools** — generated from the server's own `tools/list`, so each parameter here is exactly what your client receives. Endpoint: `http://localhost:3000/mcp`.

| Tool | Cost | What it does |
|---|---|---|
| [`add_comment`](#add_comment) | Free | Adds a timestamped comment; open comments feed the editor's AI revision. |
| [`approve`](#approve) | Free | Approves the pending round, as one of its approvers. |
| [`cancel_video`](#cancel_video) | Free | Stops a running render and refunds every credit it spent (render and AI visuals). |
| [`copy_scene`](#copy_scene) | Free | Copies a scene into another of your videos with its footage and generated media, so nothing is filmed or generated again. |
| [`create_animation`](#create_animation) | 40 credits | Make a video from data: an animated explainer, data or chart video from content you hold — figures, a table, notes, an idea — with NO website or URL. |
| [`create_character`](#create_character) | Free or 40 credits | Names a character so generated clips that name it keep one identity. |
| [`create_format`](#create_format) | Free | A format is how an episode is made — aspect, language, voice, music, tone, goal, length, cards, brand, theme, the brief or the scene templates — and knows nothi |
| [`create_object`](#create_object) | Free | Names a product, bag, watch, logo, packaging, place, vehicle or UI screen from reference images so films keep it identical. |
| [`create_review_link`](#create_review_link) | Free | A link to watch the film and, if allowed, comment with no account. |
| [`create_show`](#create_show) | Free | A show makes a video from each new item in a feed — the same storyboard every episode, new data every episode: a weekly release video from a changelog, a daily  |
| [`create_upload`](#create_upload) | Free | A one-hour address to send a file you hold (picture, clip, music, font, PDF/PPTX deck, ≤ 30 MB): curl -sS -T <file> "<upload_url>". |
| [`create_video`](#create_video) | 40 credits | Turns a public web page into a narrated video: AI voiceover, motion graphics, optional subtitles. |
| [`delete_character`](#delete_character) | Free | Deletes a character by name. |
| [`delete_object`](#delete_object) | Free | Deletes an object by name. |
| [`detect_brand`](#detect_brand) | Free | Opens a public web page in a real browser and reads its design tokens from the live CSS: accent colours, heading typeface, light or dark ground and corner style |
| [`fork_format`](#fork_format) | Free | A new format whose version 1 is the original's latest version, unpinned from its parent. |
| [`generate_asset`](#generate_asset) | 40 or 311 credits | One AI still (40 credits each) or clip (house 311, a named model its list_models price) straight into your bank — no render. |
| [`generate_site_videos`](#generate_site_videos) | 40 credits | Per video started. |
| [`get_account`](#get_account) | Free | Reads this account. |
| [`get_audit_log`](#get_audit_log) | Free | Who did what here, newest first: members, spending, review links, approvals, comments. |
| [`get_brand_kit`](#get_brand_kit) | Free | A site's brand kit, what a film paints from it (and what it cannot, with why), the effective watermark, and the account defaults beneath it. |
| [`get_format`](#get_format) | Free | The format's current template, its version history and the shows that run it, with each show's pin. |
| [`get_frames`](#get_frames) | Free | JPEG stills (≤ 1280 px wide) cut from the finished MP4 at 1–6 moments in seconds, as URLs. |
| [`get_site_plan`](#get_site_plan) | Free | The videos a site should have, one per subject, best first: goal, pitch, the real page each films (checked to exist) and the video already made from it; detail  |
| [`get_storyboard`](#get_storyboard) | Free | Reads this account. |
| [`get_timeline`](#get_timeline) | Free | Each scene's start and end in the finished MP4 (seconds), what drew it (recording, page still, AI clip/still, footage, graphic, card, inset), its transition, it |
| [`get_video`](#get_video) | Free | Reads this account. |
| [`get_video_embed`](#get_video_embed) | Free | Returns ready-to-paste markup for a finished PageToVid video: an HTML video element, Open Graph and Twitter player meta tags so the page unfurls as a playable v |
| [`import_objects`](#import_objects) | Free | Creates or replaces up to 50 objects from a product feed. |
| [`inspect_page`](#inspect_page) | Free | Opens a public page in a real browser and ranks what a video could point its camera at — calls to action, product images, cards, pricing, testimonials, search b |
| [`invite_member`](#invite_member) | Free | Emails an invite to this workspace with a role, optional site limits and monthly credit cap. |
| [`list_assets`](#list_assets) | Free | Your PRIVATE bank: every image, clip and audio file this account generated, uploaded or captured, newest first, with its id, URL, brief and tags. |
| [`list_characters`](#list_characters) | Free | The reusable characters on this account, each with its reference images and description. |
| [`list_comments`](#list_comments) | Free | Timestamped comments from members and review-link guests, oldest first, and the approval round. |
| [`list_commons_assets`](#list_commons_assets) | Free | Media people shared from their banks for anyone to use in a film — logos, product shots, illustrations, recorded flows — with tags, a licence and the site to cr |
| [`list_connections`](#list_connections) | Free | Every registered connection with its alias, kind and URL. |
| [`list_formats`](#list_formats) | Free | The account's formats, newest change first, with versions and the shows running each. |
| [`list_members`](#list_members) | Free | Members with role, sites, cap and spend this month; seats; your workspaces (send one as the X-PageToVid-Workspace header to act in it). |
| [`list_models`](#list_models) | Free | Every model this account can generate clips and stills with — capabilities, limits and the exact credit price — before spending anything. |
| [`list_motions`](#list_motions) | Free | List animations, motions, visuals and chart types: what a scene can be drawn as (chart, big number, comparison, timeline, quote, table, title card and 15 more), |
| [`list_objects`](#list_objects) | Free | The reusable objects on this account, with reference images, kind and metadata (price, brand, sku). |
| [`list_options`](#list_options) | Free | Every enum and range a film accepts (voices, languages, beds, looks, captions, motions, transitions, visuals, aspects, faces, brand kit), the models with a cred |
| [`list_revisions`](#list_revisions) | Free | Every storyboard edit, newest first: what changed and a revision_id. |
| [`list_scenes`](#list_scenes) | Free | Saved scenes, newest first: name, id, visual, aspect, whether footage is kept, the {{placeholders}} each needs as params, and tags. |
| [`list_shows`](#list_shows) | Free | Reads this account. |
| [`list_themes`](#list_themes) | Free | Lists what the theme parameter accepts: the built-in presets, the modes, the type faces the renderer can actually load, and the contrast and palette rules that  |
| [`list_video_options`](#list_video_options) | Free | Lists what create_video accepts: goals, aspect ratios, languages, voices, background music beds (9, each with a family: calm, energetic, serious, playful) and t |
| [`list_videos`](#list_videos) | Free | Reads this account. |
| [`list_voices`](#list_voices) | Free | The narrator voices with measured pitch (band and median Hz) and a short sample in the chosen language where one exists (else sample_url is null). |
| [`preview_episode`](#preview_episode) | Free | Runs the format's resolvers against the item (real calls, cached as the format says) and compiles the storyboard: every beat's final text, the beats dropped and |
| [`quote_cost`](#quote_cost) | Free | What something will cost, spending nothing: one generation (kind clip or image, optional model, duration_s, resolution, role, count), or a video_id's next reren |
| [`register_mcp_connection`](#register_mcp_connection) | Free | Registers (or replaces) a connection by alias: the URL and, optionally, a credential kept encrypted on this account. |
| [`release_video`](#release_video) | Free | Publishes a video its quality_gate held (status "held") as it is: status becomes done. |
| [`remove_member`](#remove_member) | Free | Removes a member or cancels an invite, freeing the seat; your own member id leaves the workspace. |
| [`request_approval`](#request_approval) | Free | Opens an approval round for the named approvers; supersedes a pending one. |
| [`request_changes`](#request_changes) | Free | Closes the pending round as changes requested. |
| [`rerender_video`](#rerender_video) | 40 credits | A new film from the video's current storyboard, without re-planning. |
| [`restore_revision`](#restore_revision) | Free | Puts the storyboard back as it was before a revision, undoing that edit and every later one. |
| [`rotate_webhook_secret`](#rotate_webhook_secret) | Free | Replaces the secret completion events are signed with and returns the new one, once. |
| [`run_show`](#run_show) | 40 credits | Per episode started. |
| [`save_scene`](#save_scene) | Free | Saves a scene for reuse: narration, visual, data, style AND its footage and generated media (copied so deleting the film cannot break it). |
| [`set_account_defaults`](#set_account_defaults) | Free | Partial update of the options every film starts from (below a site's brand kit). |
| [`set_brand_kit`](#set_brand_kit) | Free | Partial update of a site's brand kit: logo, palette, face (named or an uploaded font), intro/outro templates, watermark and logo corner, default voice/music/cap |
| [`set_webhook`](#set_webhook) | Free | Sets (or with null clears) the account-wide URL that receives a signed JSON event whenever a render ends. |
| [`translate_video`](#translate_video) | 40 credits | per language: a NEW video from an existing one — same storyboard and pictures, narration translated (quotes verbatim, figures localised), re-voiced and re-capti |
| [`update_character`](#update_character) | Free | Changes a character's references, description or name; anything not given is kept. |
| [`update_format`](#update_format) | Free | Changes any of a format's template fields. |
| [`update_member`](#update_member) | Free | Changes only the fields sent. |
| [`update_object`](#update_object) | Free | Changes only the fields sent. |
| [`update_show`](#update_show) | Free | Changes a show's switch, cadence, caps or name, or moves it to another format or format version. |
| [`update_storyboard`](#update_storyboard) | Free | Edits a video's storyboard in 21 operations (each branch of operations says what it does and takes): words, captions, visuals, data, shots, scenes, transitions, |
| [`upload_asset`](#upload_asset) | Free | Puts a file in your bank from a public https url or small data_base64 (a bigger file you hold: create_upload). |
| [`validate_format`](#validate_format) | Free | Compiles the template against a sample item without touching the database or any feed: the catalogue checks (voice, music, language, theme…), the scene template |
| [`verify_episode`](#verify_episode) | Free | The proof behind a film: the format version that made it (template SHA-256), every resolver source and what it fetched, the integrity report, the claim ledger ( |

1. TOC
{:toc}

## add_comment

**Cost:** Free

Adds a timestamped comment; open comments feed the editor's AI revision.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `video_id` | string | yes | The video's id. |
| `scene_id` | string |  | From get_storyboard. |
| `at_s` | number |  | Moment in the film, seconds. Range 0–36000. |
| `text` | string | yes | The comment. |

## approve

**Cost:** Free

Approves the pending round, as one of its approvers.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `video_id` | string | yes | The video's id. |
| `comment` | string |  | Optional note. |

## cancel_video

**Cost:** Free · destructive

Stops a running render and refunds every credit it spent (render and AI visuals). Use it when get_storyboard shows a plan you do not want. A finished render cannot be cancelled. The video is marked cancelled at once; the worker stops at its next step.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `video_id` | string | yes | The running video to stop. |

## copy_scene

**Cost:** Free

Copies a scene into another of your videos with its footage and generated media, so nothing is filmed or generated again. A recording cannot change aspect, nor go into a film made from data. Does not re-render.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `from_video_id` | string | yes | The video the scene is in. |
| `scene_id` | string | yes | The scene to copy, from get_storyboard. |
| `to_video_id` | string | yes | The video to copy it into (may be the same one). |
| `after_scene_id` | string |  | Put it after this scene of the target. Omitted: at the end. |

## create_animation

**Cost:** 40 credits

Make a video from data: an animated explainer, data or chart video from content you hold — figures, a table, notes, an idea — with NO website or URL. You write the scenes; each is drawn as a motion graphic, voiced, captioned and rendered. list_motions has the 21 visuals, what each needs and the animations it accepts. Asynchronous: returns a start receipt with the video_id; call get_video for the full status. Every video tool works on the result as on a filmed video.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `scenes` | array | yes | The scenes, in order, 1-20, all validated before anything is charged. On top of the render, a still (data.generate) costs 40 and a clip (data.clip) 311, refunded if it fails. |
| `aspect_ratio` | `16:9` · `9:16` · `1:1` · `4:5` |  | 16:9 for web and YouTube, 9:16 for Reels/Shorts/TikTok, 1:1 and 4:5 (1080×1350) for feeds. Default `"16:9"`. |
| `language` | string |  | As create_video. Write the narration in it. Default `"en"`. |
| `voice` | string |  | As create_video. Default `"auto"`. |
| `music` | string |  | As create_video. Default `"auto"`. |
| `tone` | string |  | As create_video. Default `"energetic"`. |
| `subtitles` | boolean |  | As create_video. Default `true`. |
| `intro` | boolean |  | Include the branded opening title card. Default `true`. |
| `outro` | boolean |  | As create_video. Default `true`. |
| `target_seconds` | integer |  | A CHECK, not a setting: your words set the length. A script more than 15% off is refused before any credit moves, saying how many words to cut or add. Omitted: any length from 15 to 180 s. Range 15–180. |
| `title` | string |  | Name for the video. Defaults to the first scene's heading. |
| `brand_name` | string |  | Name shown on the intro and outro cards. |
| `cta_text` | string |  | Call to action on the closing card. |
| `source_url` | string |  | Attribution only; nothing is fetched or filmed. |
| `theme` | object |  | As create_video. Omitted: the house palette. |
| `look` | string |  | As create_video. Default `"auto"`. |
| `caption_style` | string |  | As create_video. |
| `caption_animation` | string |  | As create_video. |
| `caption_emphasis` | string |  | As create_video. |
| `grade` | string |  | As create_video. |
| `sfx_level` | string |  | As create_video. |
| `callout` | string |  | As create_video. |
| `cursor_style` | string |  | As create_video. |
| `press_effect` | string |  | As create_video. |
| `end_screen` | string |  | As create_video. |
| `edit_style` | string |  | As create_video. |
| `pronunciations` | array |  | As create_video. |
| `ai_budget` | object |  | A ceiling on this render's AI generation; the receipt's ai_plan says what was asked for and its cost. Omitted: uncapped. |
| `idempotency_key` | string |  | As create_video. |
| `outputs` | array |  | As create_video. |
| `draft` | boolean |  | As create_video. |
| `callback_url` | string |  | As create_video. |
| `dry_run` | boolean |  | Quote only; nothing made or charged. |
| `max_credits` | integer |  | Refuse (budget_exceeded + quote) above this. Range 0–1000000. |

## create_character

**Cost:** Free or 40 credits

Names a character so generated clips that name it keep one identity. refs (1 to 3 image URLs on this account) is free; a generate prompt DRAWS the reference (40 credits, refunded on failure). Then an image scene's data.clip=true and data.character="<name>". From one of your films take raw_frame_url, never thumbnail_url: its burnt-in text teaches the generator to draw text.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `name` | string | yes | The character's name, e.g. "Ada, the founder". A clip scene names it in data.character to stay consistent. |
| `refs` | array |  | 1 to 3 reference image URLs — media on this account (a generated still, a bank asset, a commons asset from list_commons_assets). These become Veo's ingredients so the same character recurs. Give these OR a generate prompt. |
| `generate` | string |  | Draw the reference portrait instead of supplying one — e.g. "a woman in her late twenties, platinum blonde, grey tee". Costs 40 credits (one still), refunded if it fails. Ignored when refs are given. |
| `description` | string |  | A short line describing the character, added to every clip's prompt so words and image agree. |
| `site_url` | string |  | Scope the character to one site. |

## create_format

**Cost:** Free

A format is how an episode is made — aspect, language, voice, music, tone, goal, length, cards, brand, theme, the brief or the scene templates — and knows nothing about any subject. It is versioned: update_format writes a new version, shows pin one or follow latest, and every episode records the version that made it. One format can drive several shows. Validated now against a sample item; nothing is rendered.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `site_url` | string | yes | Any public http(s) URL on the site the format belongs to; the site is identified by its domain. |
| `name` | string | yes | The format's name, e.g. "Le mot du chantier". Available as {{show}} in templates. |
| `kind` | `video` · `animation` |  | video: episodes film the item's page. animation: episodes are drawn from `scenes` with the item's data filled in. Default `"video"`. |
| `goal` | `explainer` · `ad` · `demo` · `tutorial` · `article` |  | What the video is for; shapes the script. Default `"explainer"`. |
| `aspect_ratio` | `16:9` · `9:16` · `1:1` · `4:5` |  | 16:9 for web and YouTube, 9:16 for Reels/Shorts/TikTok, 1:1 and 4:5 (1080×1350) for feeds. Default `"16:9"`. |
| `language` | `en` · `fr` · `es` · `de` · `it` · `pt` · `nl` · `ar` · `hi` · `ko` · `pl` · `tr` · `sv` |  | Language of the voiceover and captions. Write the narration in this language. Default `"en"`. |
| `target_seconds` | integer |  | A CHECK, not a setting: your words set the length. A script more than 15% off is refused before any credit moves, saying how many words to cut or add. Omitted: any length from 15 to 180 s. Range 15–180. |
| `tone` | string |  | Delivery of the narration, up to 80 characters — e.g. energetic, calm, authoritative, or a short direction like "dry and deadpan, like a friend telling a story". Default `"energetic"`. |
| `voice` | `auto` · `Kore` · `Zephyr` · `Puck` · `Charon` · `Aoede` · `Fenrir` · `Leda` · `Orus` · `Callirrhoe` · `Achird` · `Sulafat` · `Sadachbia` |  | Narrator (all multilingual). auto picks a voice that fits the goal and tone and differs from the site's previous films. Default `"auto"`. |
| `music` | string |  | Music bed, "none", or "asset:<id>" (upload_asset). auto fits the goal and differs from the site's previous films. Default `"auto"`. |
| `subtitles` | boolean |  | Burn captions into the picture and emit a .vtt sidecar. Default `true`. |
| `intro` | boolean |  | Include the branded opening title card. Default `true`. |
| `outro` | boolean |  | Include the closing call-to-action card. Default `true`. |
| `brand_name` | string |  | Name shown on the intro and outro cards. |
| `theme` | object |  | As create_video. |
| `focus_template` | string |  | video formats: the brief every episode's script writer gets, with {{title}} {{summary}} {{link}} {{date}} {{image}} {{show}} {{site}} filled from the item. |
| `title_template` | string |  | animation formats: the episode's title, same placeholders. Default "{{show}} — {{title}}". |
| `scenes` | array |  | animation formats: the scene templates, as create_animation's scenes (not from_library), with the placeholders in any string. |
| `programme` | object |  | animation formats: the programme instead of plain scenes. {beats: [...], resolvers: [...], computed: {...}, requires_beats: [...], reject_if: [...]}. A beat is a scene (visual, motion, mood, heading, caption, narration, data) plus beat (one of cold_open, title, identity, context, trend, breakdown, outlier, comparison, caveats, verdict, sources), when (an expression; dropped when not true) and for_each (an expression yielding a list; repeated per element). Any string may carry {{ expressions }} — dotted paths and filters such as money(EUR,M), percent(0), say, sort_by(year), take_last(6), map({label: year, value: total}) — and any field may be {"$bind": "expression"} to receive a real number, list or object (a chart's points). Resolvers fetch data before compiling: {id, call: {mcp: alias, tool, input} | {http: url, query, body}, select, required, on_missing: skip_episode | drop_beats(a,b) | use_default | fail_loud, cache: "30d"}; each reads what the ones before it bound. Every numeral in a narration or caption must come from an expression: a figure typed by hand fails validation by beat. validate_format checks the template; preview_episode runs the resolvers and compiles a real episode for free. |
| `routing` | object |  | How episodes are made: {planner?: flash|pro, footage?: prefer-recorded|record-fresh}. flash is the benched default (it beat every larger model under the real prompt); pro is a deliberate choice. prefer-recorded uses the site's banked flow recordings when they match a scene; record-fresh films every episode anew, for a subject that changes each time. |

## create_object

**Cost:** Free

Names a product, bag, watch, logo, packaging, place, vehicle or UI screen from reference images so films keep it identical. Generated pictures take it in data.objects (clips, stills, insets, generate_asset) next to a character; image, gallery, pricing and compare cards draw it from data.object with its name and price. The same name replaces the earlier object.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `name` | string | yes | The object's name, e.g. "Aurora watch". Scenes name it. |
| `kind` | `product` · `bag` · `watch` · `logo` · `packaging` · `place` · `vehicle` · `ui_screen` · `other` | yes | What it is. |
| `refs` | array | yes | 1-6 reference images, best first: asset ids (list_assets) or media URLs on this account. |
| `description` | string | null |  | One line added to every prompt that names it. |
| `site_url` | string |  | Scope it to one of your sites. |
| `source_url` | string |  | Where it comes from (a product page). Attribution only. |
| `metadata` | object |  | {price, currency (ISO 4217), brand, sku, url}. A price is drawn on pricing/compare/image cards. |

## create_review_link

**Cost:** Free

A link to watch the film and, if allowed, comment with no account. Shown once; only its hash is stored.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `video_id` | string | yes | The video's id. |
| `expires_in_hours` | integer |  | Lifetime. Default `168`. Range 1–720. |
| `can_comment` | boolean |  | Guests may comment. Default `true`. |

## create_show

**Cost:** Free

A show makes a video from each new item in a feed — the same storyboard every episode, new data every episode: a weekly release video from a changelog, a daily listing video from an RSS feed, a clip per new post. Episodes are ordinary videos (a render each) made by run_show or, once confirmed, by the scheduler at the show's cadence. A new show is HELD: nothing renders until its owner has called run_show once with confirm=true, and it never spends more than max_credits_per_day. Returns the show and what to do next.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `site_url` | string | yes | Any public http(s) URL on the site; the site is identified by its domain. |
| `name` | string | yes | The show's name, e.g. "Le mot du chantier". Available as {{show}} in templates. |
| `kind` | `video` · `animation` |  | video: each episode films the item's own page (like create_video) with focus_template as its brief. animation: each episode is drawn from `scenes` (like create_animation) with the item's data filled in. Default `"video"`. |
| `feed_kind` | `rss` · `json` · `manual` · `query` · `watchlist` · `webhook` |  | rss: RSS/Atom. json: a JSON Feed or any JSON API via feed_map. query: one call per run on a registered connection (`source`). watchlist: the fixed items in `watchlist`. webhook: another system POSTs items to the show's webhook URL, signed with the secret returned once (X-PageToVid-Signature: sha256=HMAC of the body); cadence manual. manual: items passed to run_show, never scheduled. Default `"rss"`. |
| `feed_url` | string |  | The feed's public URL for rss and json. It is read once now to make sure it parses. |
| `source` | object |  | feed_kind query: {call: {mcp: alias, tool, input} | {http: url, query}, select: an expression into the answer that yields the list, map: dotted paths from an element to the item ({id, title, summary, link, image, date})}. Strings in the input may carry {{ show }}, {{ site }} and {{ now }}. Called once now to make sure it answers. |
| `watchlist` | array |  | feed_kind watchlist: the items, as run_show takes them. Each is made once — or once per period with repeat_every. |
| `repeat_every` | `none` · `month` · `quarter` · `year` |  | query and watchlist shows: make every item again each period (the period is in the episode key and available to a programme as {{ item.period }}). none: each item once, ever. Default `"none"`. |
| `feed_map` | object |  | For feed_kind json when the document is not a JSON Feed: dotted paths, e.g. {"items":"data.results","id":"slug","title":"name","summary":"excerpt","link":"href","image":"cover.url","date":"published_at"}. `items` may be omitted when the document is an array. |
| `cadence` | `manual` · `hourly` · `daily` · `weekly` |  | How often the scheduler runs the show once it is confirmed. manual: only when run_show is called. Default daily; manual for manual and webhook feeds. |
| `max_episodes_per_run` | integer |  | Newest items first; at most this many episodes per run. Default `1`. Range 1–10. |
| `max_credits_per_day` | integer |  | The show never spends more than this in a UTC day, however many items the feed gains. An episode is 40 credits. Default `120`. Range 40–2000. |
| `format_id` | string |  | Run an existing format (create_format / list_formats) instead of the fields below; its kind must match. Without it, the fields below become the show's own format, version 1, editable later with update_format. |
| `format_version` | integer |  | With format_id: pin the show to this version. Omitted, the show follows the format's latest version. Range 1–100000. |
| `goal` | string |  | As create_format. Default `"explainer"`. |
| `aspect_ratio` | string |  | As create_format. Default `"16:9"`. |
| `language` | string |  | As create_format. Default `"en"`. |
| `target_seconds` | integer |  | As create_format. |
| `tone` | string |  | As create_format. Default `"energetic"`. |
| `voice` | string |  | As create_format. Default `"auto"`. |
| `music` | string |  | As create_format. Default `"auto"`. |
| `subtitles` | boolean |  | As create_format. Default `true`. |
| `intro` | boolean |  | As create_format. Default `true`. |
| `outro` | boolean |  | As create_format. Default `true`. |
| `brand_name` | string |  | As create_format. |
| `theme` | object |  | As create_video. |
| `focus_template` | string |  | As create_format. Omitted: a brief leading with the item's title and summary. |
| `title_template` | string |  | As create_format. |
| `scenes` | array |  | As create_format. An image scene whose {{image}} is empty for an item is dropped from that episode. |
| `routing` | object |  | As create_format. |

## create_upload

**Cost:** Free

A one-hour address to send a file you hold (picture, clip, music, font, PDF/PPTX deck, ≤ 30 MB): curl -sS -T <file> "<upload_url>". The reply is the asset or the deck's slides.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `kind` | `image` · `video` · `audio` · `font` · `deck` |  | Read from the bytes if omitted. |
| `name` | string |  | A label. |
| `site_url` | string |  | Attach to this site. |

## create_video

**Cost:** 40 credits

Turns a public web page into a narrated video: AI voiceover, motion graphics, optional subtitles. Asynchronous (several minutes, sometimes past fifteen): returns a start receipt with the video_id at once; call get_video for the full status. A page behind a login is filmed only with a capture session registered from the VS Code or browser extension.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `url` | string | yes | Public http(s) page to film; you must have the right to. |
| `goal` | `explainer` · `ad` · `demo` · `tutorial` · `article` |  | What the video is for; shapes the script. Default `"explainer"`. |
| `aspect_ratio` | `16:9` · `9:16` · `1:1` · `4:5` |  | 9:16 (Reels/Shorts) films the page's MOBILE layout in a phone viewport; 16:9, 1:1 and 4:5 film the 1280-wide desktop layout. Default `"16:9"`. |
| `language` | `en` · `fr` · `es` · `de` · `it` · `pt` · `nl` · `ar` · `hi` · `ko` · `pl` · `tr` · `sv` |  | Language of the script and voiceover. Default `"en"`. |
| `target_seconds` | integer |  | Target length; the finished film is measured against it. Default `45`. Range 15–180. |
| `subtitles` | boolean |  | Burn captions in and emit a .vtt sidecar. Default `true`. |
| `tone` | string |  | Narration delivery, e.g. calm, or a short direction. Default `"energetic"`. |
| `voice` | `auto` · `Kore` · `Zephyr` · `Puck` · `Charon` · `Aoede` · `Fenrir` · `Leda` · `Orus` · `Callirrhoe` · `Achird` · `Sulafat` · `Sadachbia` |  | Narrator (all multilingual). auto picks a voice that fits the goal and tone and differs from the site's previous films. Default `"auto"`. |
| `music` | string |  | Music bed, "none", or "asset:<id>" (upload_asset). auto fits the goal and differs from the site's previous films. Default `"auto"`. |
| `brand_name` | string |  | Name on the intro and outro cards; default the site's. |
| `focus` | string |  | Context the page cannot show (an offer, the audience, a code, what to avoid). Anything here may be voiced as FACT in the customer's voice; a line in quotation marks is placed verbatim, usually as the hook. |
| `idempotency_key` | string |  | Same key within 24 h returns the original video, uncharged. Use it if your client may retry. |
| `theme` | object |  | Palette, type and mode; list_themes has the presets and rules, detect_brand reads a site's. Omitted: a filmed video adopts the page's CSS. |
| `intro` | boolean |  | Opening title card (1.5 s). Omitted: true, except goal "ad" (opens on its hook). |
| `outro` | boolean |  | Closing call-to-action card. Default `true`. |
| `routing` | object |  | {planner?: flash|pro, footage?: prefer-recorded|record-fresh}. flash is the benched default (pro is a choice, not an upgrade); prefer-recorded reuses the site's banked flow recordings. |
| `look` | `clean` · `bold` · `editorial` · `playful` · `tech` · `auto` |  | The film's look: captions, cutting, sound cues, music family and motion together; auto varies with goal, shape and the site's films (list_video_options). Default `"auto"`. |
| `caption_style` | `karaoke` · `bold` · `boxed` · `minimal` · `outline` |  | Overrides the look's captions. |
| `caption_animation` | `none` · `pop` · `bounce` · `wave` · `glow` · `slide` |  | What a spoken word does; overrides the look's. |
| `caption_emphasis` | `manual` · `auto` · `none` |  | Brand-coloured words: **asterisked** (manual), plus figures (auto), or none. |
| `grade` | `none` · `warm` · `cool` · `vivid` · `mono` · `vintage` · `contrast` |  | Footage colour grade; overrides the look's. |
| `sfx_level` | `off` · `subtle` · `full` |  | Sound-design loudness; overrides the look's. |
| `callout` | `none` · `ring` · `arrow` · `underline` · `dim` |  | What points at a screencast's subject. |
| `cursor_style` | `arrow` · `hand` · `dot` · `none` |  | The pointer a recording draws. |
| `press_effect` | `punch` · `freeze` · `slowmo` · `none` |  | What the picture does on a click. |
| `end_screen` | `cta` · `qr` · `social` · `logo` · `none` |  | The closing card. |
| `edit_style` | `tiktok_punchy` · `documentary` · `corporate` · `cinematic` |  | Cutting rhythm (list_motions); a scene's own transition still wins. |
| `ai_mode` | `none` · `assist` · `rich` |  | AI visuals for beats the page cannot show (paid plans): none; assist = a few stills; rich = stills and clips within ai_budget. Omitted: assist where the plan generates, else none. Charged per visual, refunded on failure. |
| `ai_budget` | object |  | Ceiling on AI visuals, given to the planner; past it they are dropped (refuse = fallback here), queue lifts it. |
| `model` | string |  | Clip model (list_models) for ai_mode rich, or auto (routed per scene, see optimize); omit for the house clip. |
| `optimize` | `quality` · `balanced` · `speed` · `cost` |  | With model auto: quality, balanced (default), speed or cost. |
| `quality_gate` | object |  | auto_fix (default): dead air and colliding overlays fixed before rendering (auto_fixes). hold: also, a film scored under min_score ends "held" until release_video. deliver: as authored. |
| `outputs` | array |  | One storyboard in 1-4 shapes: the first is this video (replaces aspect_ratio), each other a sibling (get_video formats), a render each, started when the first ends. |
| `draft` | boolean |  | Free preview: 1/3 resolution, DRAFT mark, no AI visuals. 5/hour. rerender_video without draft then makes the paid film, no re-plan. |
| `callback_url` | string |  | https URL POSTed a JSON event when the render ends (done/held/error/cancelled), 3 tries. Verify: X-PageToVid-Signature = "sha256=" + hex HMAC-SHA256(secret, X-PageToVid-Timestamp + "." + raw body); refuse timestamps over 5 min old. Secret: webhook_secret, shown once, or rotate_webhook_secret. |
| `dry_run` | boolean |  | Quote only; nothing made or charged. |
| `max_credits` | integer |  | Refuse (budget_exceeded + quote) above this. Range 0–1000000. |
| `pronunciations` | array |  | Voice-only lexicon, e.g. [{"text":"Nginx","say":"engine x"}]; captions keep the text. |

## delete_character

**Cost:** Free · destructive

Deletes a character by name. Its reference images stay in your bank and clips made with it stay in their films.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `name` | string | yes | The character's current name. |

## delete_object

**Cost:** Free · destructive

Deletes an object by name. Its images stay in your bank and media made with it stays in its films.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `name` | string | yes | The object to delete. |

## detect_brand

**Cost:** Free · read-only

Opens a public web page in a real browser and reads its design tokens from the live CSS: accent colours, heading typeface, light or dark ground and corner style. Returns a theme object ready to pass to create_video, create_animation or rerender_video, plus any colour the site uses that the film cannot paint with and why. No video is made and no credit is spent.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `url` | string | yes | A public page to read the brand from. The home page is usually the richest. |

## fork_format

**Cost:** Free

A new format whose version 1 is the original's latest version, unpinned from its parent. Edit the copy without touching the original.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `format_id` | string | yes | The format_id from create_format or list_formats. |
| `name` | string |  | The copy's name. Default: the original's name with " (copy)". |
| `site_url` | string |  | The site the copy belongs to. Default: the original's site. |

## generate_asset

**Cost:** 40 or 311 credits

One AI still (40 credits each) or clip (house 311, a named model its list_models price) straight into your bank — no render. Clip controls are refused, with the allowed values, when the model is not sent them; model auto picks one and says why. best_of makes N and keeps the best graded (all N charged). Charged before, refunded on failure; dry_run quotes it free. Paid plans.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `kind` | `image` · `video` |  | image (a still) or video (a clip). Default image. |
| `prompt` | string | yes | What to draw or film. |
| `aspect_ratio` | `16:9` · `9:16` · `1:1` · `4:5` · `21:9` |  | Default 16:9. 21:9 and 4:5 only where list_models says the model takes them. |
| `model` | string |  | list_models id, house, house-image, or auto (clips; see optimize). |
| `count` | integer |  | Stills: how many, each charged. Range 1–4. |
| `optimize` | `quality` · `balanced` · `speed` · `cost` |  | For model auto. Default balanced. |
| `duration_s` | integer |  | Seconds (list_models range). Range 1–60. |
| `resolution` | `480p` · `720p` · `768p` · `1080p` · `2k` · `4k` |  | One the model offers. |
| `first_frame` | string |  | Bank image id/URL to start on. |
| `last_frame` | string |  | Bank image to end on. |
| `seed` | integer |  | Where the model takes one. Range 0–4294967295. |
| `negative_prompt` | string |  | Where the model takes one. |
| `camera` | object |  | Folded into the prompt. |
| `shot` | `wide` · `medium` · `close_up` |  | Folded into the prompt. |
| `best_of` | integer |  | N graded, best kept, all charged. Range 1–4. |
| `dry_run` | boolean |  | Quote only; nothing made or charged. |
| `max_credits` | integer |  | Refuse (budget_exceeded + quote) above this. Range 0–1000000. |
| `character` | string |  | A character from create_character, so the same face comes back. |
| `objects` | array |  | Object names (list_objects) kept consistent, after the character. |
| `tags` | string |  | Comma-separated tags, to find it again. |
| `site_url` | string |  | Attach it to one of your sites. |

## generate_site_videos

**Cost:** 40 credits

Per video started. One ordinary filmed video per idea of get_site_plan without one (or the idea_ids given), of the idea's verified page with its sourced brief as focus. Without confirm it lists what it would make and the cost, capped at the balance (the rest under needs_credits), creating nothing; confirm=true starts those. get_video reports each. A retry never starts an idea twice.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `site_url` | string | yes | Any public http(s) URL on the site; the site is identified by its domain. |
| `idea_ids` | array |  | Which ideas from get_site_plan to make, in order. Omitted: every idea that has no video yet. |
| `url` | string |  | The page to film for every video. Omitted, each idea films its own verified page (page_url in get_site_plan). |
| `aspect_ratio` | string |  | As create_video. Default `"16:9"`. |
| `language` | string |  | As create_video. Default `"en"`. |
| `voice` | string |  | As create_video. Default `"auto"`. |
| `music` | string |  | As create_video. Default `"auto"`. |
| `subtitles` | boolean |  | As create_video. Default `true`. |
| `intro` | boolean |  | Include the branded opening title card. Default `true`. |
| `outro` | boolean |  | As create_video. Default `true`. |
| `brand_name` | string |  | Name shown on the intro and outro cards. |
| `theme` | object |  | As create_video. |
| `look` | string |  | As create_video. Default `"auto"`. |
| `caption_style` | string |  | As create_video. |
| `confirm` | boolean |  | false (the default) previews the videos and spends nothing. true starts them and spends 40 credits each. Default `false`. |
| `max_videos` | integer |  | At most this many videos in one call. Call again for the rest. Default `5`. Range 1–10. |

## get_account

**Cost:** Free · read-only

Reads this account. CALL THIS FIRST: the plan, credits left, whether AI visuals are available and charged here, watermarking, renders running, length and rate limits. Then usually: inspect_page (in the aspect you will film), create_video or create_animation, get_storyboard (the only place the chosen shots show), update_storyboard, rerender_video.

_No parameters._

## get_audit_log

**Cost:** Free · read-only

Who did what here, newest first: members, spending, review links, approvals, comments.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `site_url` | string |  | Only entries about this site. |
| `since` | string |  | Only entries from this time on. |

## get_brand_kit

**Cost:** Free · read-only

A site's brand kit, what a film paints from it (and what it cannot, with why), the effective watermark, and the account defaults beneath it.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `site_url` | string | yes | Any URL of the site. |

## get_format

**Cost:** Free · read-only

The format's current template, its version history and the shows that run it, with each show's pin.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `format_id` | string | yes | The format_id from create_format or list_formats. |

## get_frames

**Cost:** Free · read-only

JPEG stills (≤ 1280 px wide) cut from the finished MP4 at 1–6 moments in seconds, as URLs. Cached per render.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `video_id` | string | yes | The video's id. |
| `times` | array | yes | 1–6 times in seconds (0.1 s steps). |

## get_site_plan

**Cost:** Free

The videos a site should have, one per subject, best first: goal, pitch, the real page each films (checked to exist) and the video already made from it; detail full adds the brief, every fact with its source page and sentence (unsourced ones removed), and the shots. Generated from the site's pages on first call (no credit), then stored. generate_site_videos works from it.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `site_url` | string | yes | Any public http(s) URL on the site; the site is identified by its domain. |
| `language` | `en` · `fr` · `es` · `de` · `it` · `pt` · `nl` · `ar` · `hi` · `ko` · `pl` · `tr` · `sv` |  | Language the ideas and shot list are written in. This is the planner's working language, not the videos' — generate_site_videos sets that. Default `"en"`. |
| `refresh` | boolean |  | true regenerates the plan even if one exists, overwriting it. A plan is generated automatically the first time. Default `false`. |
| `limit` | integer |  | How many ideas to return, best first (one per subject). Default `8`. Range 1–35. |
| `detail` | `short` · `full` |  | short: title, goal, pitch, page and whether it was made. full: also the brief (focus), its sources, audience, tone and shots. Default `"short"`. |

## get_storyboard

**Cost:** Free · read-only

Reads this account. Returns the scene-by-scene plan of a video: what each scene narrates, its on-screen caption, how long it holds, and whether it is real footage of the page or a motion graphic (and which motion).

| Parameter | Type | Required | Description |
|---|---|---|---|
| `video_id` | string | yes | The video_id to read. |

## get_timeline

**Cost:** Free · read-only

Each scene's start and end in the finished MP4 (seconds), what drew it (recording, page still, AI clip/still, footage, graphic, card, inset), its transition, its slice of the one voice track with word onsets, plus the music and caption style. timeline_source: stored by the render, or rebuilt from the scenes.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `video_id` | string | yes | The video's id. |

## get_video

**Cost:** Free · read-only

Reads this account. The full status of a render: phase and progress while it runs (with poll_after_seconds), then the files, length, credits, warnings and quality. `status` is one of, in pipeline order: draft, queued, analyzing, scripting, recording, voicing, rendering, held, done, error. In flight, so poll again after poll_after_seconds: queued, analyzing, scripting, recording, voicing, rendering. Terminal, so stop polling: held, done, error — a cancelled render ends as error with the reason in `error`, and a film can be done and still carry warnings. held: finished but unpublished by quality_gate. draft has not been queued.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `video_id` | string | yes | The video_id returned by create_video. |

## get_video_embed

**Cost:** Free · read-only

Returns ready-to-paste markup for a finished PageToVid video: an HTML video element, Open Graph and Twitter player meta tags so the page unfurls as a playable video, and a schema.org VideoObject JSON-LD block.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `video_id` | string | yes | The video_id of a finished render. |
| `page_url` | string |  | The page this markup will be pasted into. Used for og:url so a share resolves to your page rather than nothing. |
| `title` | string |  | Overrides the title in the share card. Defaults to the video's own title. |
| `description` | string |  | Overrides the share description. Defaults to a sentence written in the video's language. |

## import_objects

**Cost:** Free

Creates or replaces up to 50 objects from a product feed. Each image is downloaded (public addresses only) and banked as a reference. Failed rows are listed with the reason.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `items` | array | yes | 1-50 catalogue rows. image_url: one public image URL or a list (best first, up to 6); kind defaults to product. |
| `site_url` | string |  | Scope it to one of your sites. |

## inspect_page

**Cost:** Free · read-only

Opens a public page in a real browser and ranks what a video could point its camera at — calls to action, product images, cards, pricing, testimonials, search boxes, headings — each with a CSS selector, a size and a score (a rank, not a percentage). Says when the browser met a robot check, a sign-in or a missing page instead (blocked, block_kind, not_found), and which text fields will never be typed into. The planner reads the same ranking. Nothing is made or charged.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `url` | string | yes | A public page to look at. Nothing is filmed and no credit is spent. |
| `aspect_ratio` | `16:9` · `9:16` · `1:1` · `4:5` |  | The viewport to look through. 9:16 loads the page as a phone does, which is the layout a vertical video films — a responsive site offers different elements there (a sticky call bar, stacked cards) and they score differently. |
| `limit` | integer |  | How many candidates to return, best first. A dense page offers up to 40 and a film needs four or five; the rest are the largest single thing this surface puts in a context window. The `kinds` histogram still counts every one, so nothing is hidden — raise this only when the shortlist has nothing you want. Default `12`. Range 1–40. |
| `kinds` | string |  | Comma-separated kinds to keep, e.g. "cta,search,card". The vocabulary is in the `kinds` histogram of any reply: cta, media, image, card, pricing, testimonial, logos, heading, section, nav, search, chat, input. Omitted, every kind is offered. |

## invite_member

**Cost:** Free

Emails an invite to this workspace with a role, optional site limits and monthly credit cap. Members spend the owner's credits. Seats incl. owner: Free/Starter 1, Pro 3, Scale 5, Business 15, Agency unlimited.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `email` | string | yes | They join by signing in with it. |
| `role` | `admin` · `editor` · `reviewer` · `viewer` · `billing` | yes | editor makes and spends; reviewer comments and approves. |
| `site_urls` | array | null |  | Limit to these sites; null = all. |
| `credit_cap` | integer | null |  | Monthly credit cap; null = none. Range 0–…. |

## list_assets

**Cost:** Free · read-only

Your PRIVATE bank: every image, clip and audio file this account generated, uploaded or captured, newest first, with its id, URL, brief and tags. Reuse a picture by putting its id in an image scene as data.asset_id (a clip resolves to clipUrl by itself); an audio asset is a film's music as "asset:<id>". Reusing costs no credit.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `kind` | `image` · `video` · `audio` · `font` |  | Only images, clips, uploaded audio or fonts. |
| `q` | string |  | A word to find in the brief or the tags. |
| `character` | string |  | Only assets generated for this character. |
| `site_url` | string |  | Only assets attached to this site. |
| `limit` | integer |  | At most this many, newest first (default 40). Range 1–200. |

## list_characters

**Cost:** Free · read-only

The reusable characters on this account, each with its reference images and description. Credentials are never involved; these are just image references.

_No parameters._

## list_comments

**Cost:** Free · read-only

Timestamped comments from members and review-link guests, oldest first, and the approval round.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `video_id` | string | yes | The video's id. |

## list_commons_assets

**Cost:** Free · read-only

Media people shared from their banks for anyone to use in a film — logos, product shots, illustrations, recorded flows — with tags, a licence and the site to credit. An image scene of create_animation or update_storyboard takes an asset's id as data.asset_id (or its url as imageUrl); a gallery takes urls. Nothing here is private: only assets their owners switched to shared.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `kind` | `image` · `video` |  | Only images, or only clips. |
| `tag` | string |  | One tag, e.g. logo, dashboard, person. |
| `q` | string |  | A word to find in tags or the asset's brief. |
| `limit` | integer |  | At most this many, newest first (default 40). Range 1–200. |

## list_connections

**Cost:** Free · read-only

Every registered connection with its alias, kind and URL. Credentials are never returned.

_No parameters._

## list_formats

**Cost:** Free · read-only

The account's formats, newest change first, with versions and the shows running each.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `site_url` | string |  | Only this site's formats. Omitted, every format on the account. |

## list_members

**Cost:** Free · read-only

Members with role, sites, cap and spend this month; seats; your workspaces (send one as the X-PageToVid-Workspace header to act in it).

| Parameter | Type | Required | Description |
|---|---|---|---|
| `site_url` | string |  | Only members with this site. |

## list_models

**Cost:** Free · read-only

Every model this account can generate clips and stills with — capabilities, limits and the exact credit price — before spending anything. Omit model in a scene for the house clip; name one (data.model, or set_inset model) to choose it and pay its price. quote_cost prices a specific request.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `modality` | `video` · `image` |  | Only video or only image models. |
| `include_unavailable` | boolean |  | Also list models this account cannot use now, with the reason. |

## list_motions

**Cost:** Free · read-only

List animations, motions, visuals and chart types: what a scene can be drawn as (chart, big number, comparison, timeline, quote, table, title card and 15 more), the entrance animations each accepts, grouped by feel, and the transitions. Call it before create_animation or update_storyboard: a mismatched pair is refused, not swapped.

_No parameters._

## list_objects

**Cost:** Free · read-only

The reusable objects on this account, with reference images, kind and metadata (price, brand, sku).

| Parameter | Type | Required | Description |
|---|---|---|---|
| `kind` | `product` · `bag` · `watch` · `logo` · `packaging` · `place` · `vehicle` · `ui_screen` · `other` |  | Only this kind. |
| `q` | string |  | A word in the name or description. |
| `site_url` | string |  | Scope it to one of your sites. |

## list_options

**Cost:** Free · read-only

Every enum and range a film accepts (voices, languages, beds, looks, captions, motions, transitions, visuals, aspects, faces, brand kit), the models with a credit example, and the inheritance levels.

_No parameters._

## list_revisions

**Cost:** Free · read-only

Every storyboard edit, newest first: what changed and a revision_id. restore_revision puts the storyboard back as it was before one.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `video_id` | string | yes | The video whose storyboard history to use. |
| `limit` | integer |  | How many, newest first. Default `20`. Range 1–50. |

## list_scenes

**Cost:** Free · read-only

Saved scenes, newest first: name, id, visual, aspect, whether footage is kept, the {{placeholders}} each needs as params, and tags.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `q` | string |  | A word in the name, heading or narration. |
| `tags` | array |  | Only scenes carrying every one of these tags. |
| `site_url` | string |  | Scope it to one of your sites. |
| `limit` | integer |  | At most this many, newest first (default 40). Range 1–200. |

## list_shows

**Cost:** Free · read-only

Reads this account. Lists the shows on this account — or one site's — with their cadence, caps, whether each is confirmed or still held, what it spent today, and its five most recent episodes with the video each became.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `site_url` | string |  | Only this site's shows. Omitted: every show on the account. |

## list_themes

**Cost:** Free · read-only

Lists what the theme parameter accepts: the built-in presets, the modes, the type faces the renderer can actually load, and the contrast and palette rules that are enforced before a credit moves. Static reference data — no account access, no page fetched, free.

_No parameters._

## list_video_options

**Cost:** Free · read-only

Lists what create_video accepts: goals, aspect ratios, languages, voices, background music beds (9, each with a family: calm, energetic, serious, playful) and the allowed length range. Static reference data — no account access.

_No parameters._

## list_videos

**Cost:** Free · read-only

Reads this account. Lists videos newest first with their status and, when finished, their links. Filter by status or by a word in the page URL or title. Returns a cursor when more remain.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `status` | `any` · `queued` · `analyzing` · `scripting` · `recording` · `voicing` · `rendering` · `held` · `done` · `error` |  | Only videos in this state. Default `"any"`. |
| `query` | string |  | Matches part of the source URL or the title. |
| `created_after` | string |  | ISO 8601 timestamp; only videos created after it. |
| `cursor` | string |  | The next_cursor from a previous call. Opaque — pass it back unchanged. |
| `limit` | integer |  | How many to return. Default `10`. Range 1–50. |

## list_voices

**Cost:** Free · read-only

The narrator voices with measured pitch (band and median Hz) and a short sample in the chosen language where one exists (else sample_url is null). Every voice speaks every language.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `language` | `en` · `fr` · `es` · `de` · `it` · `pt` · `nl` · `ar` · `hi` · `ko` · `pl` · `tr` · `sv` |  | Language of the samples. Default `"en"`. |
| `pitch` | `low` · `mid` · `high` |  | Only this pitch band. |

## preview_episode

**Cost:** Free · read-only

Runs the format's resolvers against the item (real calls, cached as the format says) and compiles the storyboard: every beat's final text, the beats dropped and why, the integrity report, the upstream calls and where every bound value came from. Nothing is rendered. Read it before run_show confirm=true.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `format_id` | string | yes | The format_id from create_format or list_formats. |
| `format_version` | integer |  | Preview this version; omitted, the latest. Range 1–100000. |
| `item` | object |  | The item to make the episode of: {title, summary, link, image, date}. Omitted, a sample item. |

## quote_cost

**Cost:** Free · read-only

What something will cost, spending nothing: one generation (kind clip or image, optional model, duration_s, resolution, role, count), or a video_id's next rerender_video (render plus every AI visual not yet made). A length between two a model makes is rounded UP, with a warning; one it cannot make is refused with what it can. plan_note says when this plan has no AI generation.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `video_id` | string |  | Price the next rerender_video of this video. |
| `kind` | `clip` · `image` |  | Price one generation of this kind. |
| `model` | string |  | A model id from list_models. Omit for the house model. |
| `duration_s` | number |  | Clip length in seconds, within the model's range. Range 1–60. |
| `resolution` | `480p` · `720p` · `768p` · `1080p` · `2k` · `4k` |  | Clip resolution, one the model offers. |
| `role` | `scene` · `inset` |  | A full-frame scene or a presenter in a corner (a presenter uses the cheapest resolution). |
| `count` | integer |  | How many, 1-4. Range 1–4. |

## register_mcp_connection

**Cost:** Free

Registers (or replaces) a connection by alias: the URL and, optionally, a credential kept encrypted on this account. Formats refer to the alias only, so a format never carries a secret and is safe to publish or fork. Nothing is called now.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `alias` | string | yes | The name a format's resolvers use: {"mcp": "finance_ds", ...}. Letters, digits, underscore. |
| `url` | string | yes | The server's public http(s) address: an MCP endpoint (streamable HTTP) or an http API base. |
| `kind` | `mcp` · `http` |  | mcp: JSON-RPC tools/call. http: plain JSON endpoints under this base. Default `"mcp"`. |
| `secret` | string |  | A bearer token or API key sent as Authorization: Bearer. Stored encrypted, never returned, never in a format. |
| `note` | string |  | What this server is, for the list. |

## release_video

**Cost:** Free

Publishes a video its quality_gate held (status "held") as it is: status becomes done. Nothing is re-rendered.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `video_id` | string | yes | The held video. |

## remove_member

**Cost:** Free · destructive

Removes a member or cancels an invite, freeing the seat; your own member id leaves the workspace. Their work stays.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `member_id` | string | yes | From list_members. |

## request_approval

**Cost:** Free

Opens an approval round for the named approvers; supersedes a pending one.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `video_id` | string | yes | The video's id. |
| `approver_ids` | array | yes | Member ids, or the owner's user id. |

## request_changes

**Cost:** Free

Closes the pending round as changes requested.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `video_id` | string | yes | The video's id. |
| `comment` | string | yes | What to change. |

## rerender_video

**Cost:** 40 credits · destructive

A new film from the video's current storyboard, without re-planning. Free once per video when the film missed its length target (length_within_tolerance: false). captions_only re-times the subtitles on the existing voice, free once per render. The file is replaced when the new render finishes. Returns a start receipt; call get_video for the full status.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `video_id` | string | yes | The video to re-render. |
| `theme` | object |  | As create_video; replaces the video's theme and is kept for later re-renders. |
| `idempotency_key` | string |  | A caller-chosen id for this request. Sending the same key again within 24 hours returns the same re-render instead of starting and charging a second time — use it if your client may retry. |
| `captions_only` | boolean |  | true re-times the subtitles on the voice track the film already has and renders again — nothing is re-recorded, re-scripted or re-voiced, so only the caption timing changes. The first such resync after a paid render is free; the next one on the same render costs a render's credits. Use it when get_video's film has captions out of step with the voice. |
| `target_seconds` | integer |  | Re-baseline how long this film is MEANT to be. The target a video was created with is often a guess made before any content existed; when the film has legitimately grown or shrunk since, set it to what it should be now rather than cutting to satisfy the old number. It changes what length_within_tolerance is measured against and is kept for later re-renders. It does not change the film — the narration is still what sets the length. Range 15–180. |
| `quality_gate` | object |  | As create_video, for this render. |
| `outputs` | array |  | As create_video; must include this video's shape. Other shapes re-render their sibling or make one, a render each. |
| `draft` | boolean |  | As create_video; only before the first paid render. |
| `callback_url` | string |  | As create_video, for this render. |
| `dry_run` | boolean |  | Quote only; nothing made or charged. |
| `max_credits` | integer |  | Refuse (budget_exceeded + quote) above this. Range 0–1000000. |

## restore_revision

**Cost:** Free · destructive

Puts the storyboard back as it was before a revision, undoing that edit and every later one. Itself a revision, so it can be undone. Nothing is re-rendered until rerender_video.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `video_id` | string | yes | The video whose storyboard history to use. |
| `revision_id` | string | yes | From list_revisions. The storyboard returns to how it was BEFORE this edit. |

## rotate_webhook_secret

**Cost:** Free · destructive

Replaces the secret completion events are signed with and returns the new one, once. The old secret stops verifying at once, including for retries still in flight.

_No parameters._

## run_show

**Cost:** 40 credits

Per episode started. Reads the show's feed (or the items given), skips every item that already became an episode, and — within max_episodes_per_run and max_credits_per_day — starts one video per new item. Without confirm it returns the list it would make and spends nothing. On a held show, confirm=true is the owner's one-time approval: it makes the episodes and lets the scheduler run the show from then on.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `show_id` | string | yes | The show_id from create_show or list_shows. |
| `confirm` | boolean |  | false (the default): a free preview of the episodes this run would make. true: make them, and on a held show, confirm it — from then on the scheduler runs it at its cadence. Default `false`. |
| `items` | array |  | The items to make episodes from, for a manual show. A feed show ignores this and reads its feed. |

## save_scene

**Cost:** Free

Saves a scene for reuse: narration, visual, data, style AND its footage and generated media (copied so deleting the film cannot break it). Reusing it — update_storyboard add_scene_from_library, create_animation from_library — films and generates nothing, so no AI credit. Write {{placeholders}} in its narration or data first to fill them per use.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `video_id` | string | yes | The video the scene is in. |
| `scene_id` | string | yes | The scene, from get_storyboard. |
| `name` | string | yes | A name to reuse it by. The same name replaces the earlier entry. |
| `tags` | array |  | Tags to find it by. |

## set_account_defaults

**Cost:** Free

Partial update of the options every film starts from (below a site's brand kit). null clears a field.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `voice` | `Kore` · `Zephyr` · `Puck` · `Charon` · `Aoede` · `Fenrir` · `Leda` · `Orus` · `Callirrhoe` · `Achird` · `Sulafat` · `Sadachbia` |  | Default narrator. |
| `music` | string |  | Default bed, or "asset:<id>". |
| `look` | `clean` · `bold` · `editorial` · `playful` · `tech` |  | Default look. |
| `caption_style` | `karaoke` · `bold` · `boxed` · `minimal` · `outline` |  | Default caption style. |
| `transition` | `cut` · `crossfade` · `whip_left` · `whip_right` · `zoom_punch` · `flash` · `swipe_up` · `glitch` · `slide_left` · `slide_right` · `spin` · `blur_dissolve` · `light_leak` · `film_burn` · `zoom_blur` |  | Default arrival for scenes naming none. |
| `end_screen` | `cta` · `qr` · `social` · `logo` · `none` |  | Outro card template. |
| `intro` | `card` · `none` |  | Intro card template. |
| `font_family` | string |  | A list_options face. |
| `model` | string |  | Clip model for ai_mode rich (list_models). |

## set_brand_kit

**Cost:** Free

Partial update of a site's brand kit: logo, palette, face (named or an uploaded font), intro/outro templates, watermark and logo corner, default voice/music/captions/look/transition. null clears a field. Films of the site inherit it unless the call overrides.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `site_url` | string | yes | Any URL of the site. |
| `from_detect` | boolean |  | Fill palette, face and logo from detect_brand first; your fields win. |
| `colors` | object | null |  | Hex per slot; partial merges. |
| `logo_asset_id` | string |  | Image asset id (upload_asset). |
| `font_asset_id` | string |  | Font asset id (upload_asset kind "font"); outranks font_family. |
| `logo_corner` | `tl` · `tr` · `bl` · `br` · `none` |  | Logo corner on the picture, or none. |
| `logo_safe_zone` | number |  | Logo clear space, % of the short side. Range 2–12. |
| `watermark` | boolean |  | Paid plans: badge on or off. Free keeps it. |
| `voice` | `Kore` · `Zephyr` · `Puck` · `Charon` · `Aoede` · `Fenrir` · `Leda` · `Orus` · `Callirrhoe` · `Achird` · `Sulafat` · `Sadachbia` |  | Default narrator. |
| `music` | string |  | Default bed, or "asset:<id>". |
| `look` | `clean` · `bold` · `editorial` · `playful` · `tech` |  | Default look. |
| `caption_style` | `karaoke` · `bold` · `boxed` · `minimal` · `outline` |  | Default caption style. |
| `transition` | `cut` · `crossfade` · `whip_left` · `whip_right` · `zoom_punch` · `flash` · `swipe_up` · `glitch` · `slide_left` · `slide_right` · `spin` · `blur_dissolve` · `light_leak` · `film_burn` · `zoom_blur` |  | Default arrival for scenes naming none. |
| `end_screen` | `cta` · `qr` · `social` · `logo` · `none` |  | Outro card template. |
| `intro` | `card` · `none` |  | Intro card template. |
| `font_family` | string |  | A list_options face. |
| `model` | string |  | Clip model for ai_mode rich (list_models). |

## set_webhook

**Cost:** Free

Sets (or with null clears) the account-wide URL that receives a signed JSON event whenever a render ends. The first time a secret is needed it is created and returned here, once.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `url` | string | null | yes | Public https URL for the completion event of every render that has no callback_url of its own; null removes it. Signed as callback_url describes on create_video. |

## translate_video

**Cost:** 40 credits

per language: a NEW video from an existing one — same storyboard and pictures, narration translated (quotes verbatim, figures localised), re-voiced and re-captioned, card text translated. Filmed scenes are re-recorded on the site's page in that language when it has one (hreflang), else the footage is reused and `scenes` says so. Charged and refunded like any render; AI visuals already made are reused free.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `video_id` | string | yes | A finished video. |
| `languages` | array | yes | One new video each. |
| `idempotency_key` | string |  | Same key within 24 h returns the videos already started, uncharged. |

## update_character

**Cost:** Free

Changes a character's references, description or name; anything not given is kept. Clips already made keep the look they were made with.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `name` | string | yes | The character's current name. |
| `new_name` | string |  | Rename it. Scenes that name the old name must be updated. |
| `refs` | array |  | 1-3 reference image URLs from your bank, replacing the current ones. |
| `description` | string | null |  | What the character looks like; null clears it. |

## update_format

**Cost:** Free

Changes any of a format's template fields. The result is a NEW version — the previous ones stay exactly as they were, and every episode already made keeps the version that made it. Shows following latest use the new version from their next run; pinned shows do not move until update_show moves them. Validated whole before anything is written.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `format_id` | string | yes | The format_id from create_format or list_formats. |
| `name` | string |  | A new name. |
| `note` | string |  | What this version changes, for the version history. |
| `goal` | string |  | As create_format. |
| `aspect_ratio` | string |  | As create_format. |
| `language` | string |  | As create_format. |
| `target_seconds` | integer |  | As create_format. |
| `tone` | string |  | As create_format. |
| `voice` | string |  | As create_format. |
| `music` | string |  | As create_format. |
| `subtitles` | boolean |  | As create_format. |
| `intro` | boolean |  | As create_format. |
| `outro` | boolean |  | As create_format. |
| `brand_name` | string |  | As create_format. |
| `theme` | object |  | As create_video. |
| `focus_template` | string |  | As create_format. |
| `title_template` | string |  | As create_format. |
| `scenes` | array |  | animation formats: the scene templates, as create_animation's scenes (not from_library), with the placeholders in any string. |
| `programme` | object |  | As create_format. |
| `routing` | object |  | As create_format. |

## update_member

**Cost:** Free

Changes only the fields sent. Only the owner grants or changes admin and billing.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `member_id` | string | yes | From list_members. |
| `role` | `admin` · `editor` · `reviewer` · `viewer` · `billing` |  | New role. |
| `site_urls` | array | null |  | Limit to these sites; null = all. |
| `credit_cap` | integer | null |  | Monthly credit cap; null = none. Range 0–…. |

## update_object

**Cost:** Free

Changes only the fields sent. Media already generated with it is kept until a scene's description changes.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `name` | string | yes | The object to change. |
| `new_name` | string |  | Rename it. |
| `kind` | `product` · `bag` · `watch` · `logo` · `packaging` · `place` · `vehicle` · `ui_screen` · `other` |  | What it is. |
| `refs` | array |  | Replace the references. |
| `description` | string | null |  | One line added to every prompt that names it. |
| `site_url` | string |  | Scope it to one of your sites. |
| `source_url` | string |  | Where it comes from (a product page). Attribution only. |
| `metadata` | object |  | Merged into the metadata; a null value clears that key. |

## update_show

**Cost:** Free

Changes a show's switch, cadence, caps or name, or moves it to another format or format version. The template itself is edited with update_format, which writes a new version and leaves every episode already made where it is. Nothing is rendered.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `show_id` | string | yes | The show_id from create_show or list_shows. |
| `active` | boolean |  | false pauses the show (the scheduler skips it, run_show refuses); true resumes it. |
| `cadence` | `manual` · `hourly` · `daily` · `weekly` |  | A new cadence. |
| `max_episodes_per_run` | integer |  | A new per-run cap. Range 1–10. |
| `max_credits_per_day` | integer |  | A new daily credit cap (an episode is 40 credits). Range 40–2000. |
| `name` | string |  | A new name. |
| `format_id` | string |  | Move the show to another format of the same kind. |
| `format_version` | integer |  | Pin the show to this version of its format. Range 1–100000. |
| `format_version_latest` | boolean |  | true unpins the show so it follows its format's latest version. |
| `source` | object |  | query shows: a new source (same shape as create_show). |
| `watchlist` | array |  | watchlist shows: the new list; it replaces the old one. Items already made stay made. |
| `repeat_every` | `none` · `month` · `quarter` · `year` |  | query and watchlist shows: a new period, or none to stop repeating. |
| `rotate_webhook_secret` | boolean |  | webhook shows: mint a new signing secret (returned once in this call's webhook_secret); the old one stops working at once. |

## update_storyboard

**Cost:** Free · destructive

Edits a video's storyboard in 21 operations (each branch of operations says what it does and takes): words, captions, visuals, data, shots, scenes, transitions, presenter, voice, music, look. Does not re-render — rerender_video makes the new film. Every call is snapshotted, so an edit can be undone (list_revisions).

| Parameter | Type | Required | Description |
|---|---|---|---|
| `video_id` | string | yes | The video to edit. Its scene ids come from get_storyboard. |
| `operations` | array | yes | The changes to apply, in order, up to 20. All are validated before any is written, so a bad batch changes nothing; a wrong figure is set_data plus one rerender_video, not a new video. |

## upload_asset

**Cost:** Free

Puts a file in your bank from a public https url or small data_base64 (a bigger file you hold: create_upload). Picture or clip → data.asset_id in an image scene; audio → music "asset:<id>"; deck (PDF/PPTX) → every slide's text and pictures, to write the storyboard from. Identical bytes return the existing asset.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `url` | string |  | Public https URL. |
| `data_base64` | string |  | The file, base64, ≤ 2 MB. |
| `filename` | string |  | Its file name. |
| `kind` | `image` · `video` · `audio` · `font` · `deck` |  | Required with url. image ≤ 20 MB, video ≤ 200 MB/60 s, audio ≤ 50 MB, font ≤ 2 MB, deck (PDF/PPTX) ≤ 30 MB. |
| `name` | string |  | A label to find it again. |
| `site_url` | string |  | Attach an image or clip to one of your sites. |

## validate_format

**Cost:** Free · read-only

Compiles the template against a sample item without touching the database or any feed: the catalogue checks (voice, music, language, theme…), the scene templates filled and checked as an animation, and what the first episode's title, brief and scene count would be. Returns problems by field; nothing is created, rendered or charged.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `name` | string |  | The format's name, for {{show}}. Default `"Preview"`. |
| `kind` | `video` · `animation` |  | video or animation. Default `"video"`. |
| `goal` | string |  | As create_format. Default `"explainer"`. |
| `aspect_ratio` | string |  | As create_format. Default `"16:9"`. |
| `language` | string |  | As create_format. Default `"en"`. |
| `target_seconds` | integer |  | As create_format. |
| `tone` | string |  | As create_format. Default `"energetic"`. |
| `voice` | string |  | As create_format. Default `"auto"`. |
| `music` | string |  | As create_format. Default `"auto"`. |
| `subtitles` | boolean |  | As create_format. Default `true`. |
| `intro` | boolean |  | As create_format. Default `true`. |
| `outro` | boolean |  | As create_format. Default `true`. |
| `brand_name` | string |  | As create_format. |
| `theme` | object |  | As create_video. |
| `focus_template` | string |  | As create_format. |
| `title_template` | string |  | As create_format. |
| `scenes` | array |  | animation formats: the scene templates, as create_animation's scenes (not from_library), with the placeholders in any string. |
| `programme` | object |  | As create_format. |
| `routing` | object |  | As create_format. |

## verify_episode

**Cost:** Free · read-only

The proof behind a film: the format version that made it (template SHA-256), every resolver source and what it fetched, the integrity report, the claim ledger (which figures trace to the page, the brief or nothing), the Content Credentials (C2PA), and a reproducibility check recompiling the stored data against the narration word for word.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `episode_id` | string |  | The episode to verify, from run_show or a show's recent_episodes. |
| `video_id` | string |  | Or a video id: the episode is found through it when there is one; a plain video is verified on its claim ledger and credentials. |

