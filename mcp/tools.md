---
title: Tool reference
parent: MCP server
nav_order: 3
---

# Tool reference
{: .no_toc }

Every tool the PageToVid MCP server publishes — **36 tools** — generated from the server's own `tools/list`, so each parameter here is exactly what your client receives. Endpoint: `https://pagetovid.com/mcp`.

| Tool | Cost | What it does |
|---|---|---|
| [`cancel_video`](#cancel_video) | Free | Stops a render that is still running and returns every credit it spent — the render credit and any AI stills or clips it had already generated. |
| [`create_animation`](#create_animation) | 1 credit | Make a video from data. |
| [`create_character`](#create_character) | Free or 1 credit | Names a character so a generated clip that names it keeps the same identity across scenes (Veo 3.1 ingredients-to-video). |
| [`create_format`](#create_format) | Free | A format is how an episode is made — aspect, language, voice, music, tone, goal, length, cards, brand, theme, the brief or the scene templates — and knows nothi |
| [`create_show`](#create_show) | Free | A show makes a video from each new item in a feed — the same storyboard every episode, new data every episode: a weekly release video from a changelog, a daily  |
| [`create_video`](#create_video) | 1 credit | Starts a PageToVid render that turns a public web page URL into a narrated video with an AI voiceover, motion graphics and optional subtitles. |
| [`detect_brand`](#detect_brand) | Free | Opens a public web page in a real browser and reads its design tokens from the live CSS: accent colours, heading typeface, light or dark ground and corner style |
| [`fork_format`](#fork_format) | Free | A new format whose version 1 is the original's latest version, unpinned from its parent. |
| [`generate_asset`](#generate_asset) | 1 or 4 credits | Generates a single AI still (1 credit) or clip (4 credits) straight into your media bank and returns its id and URL — no project, no render, no minimum length. |
| [`generate_site_videos`](#generate_site_videos) | 1 credit | Per video started. |
| [`get_account`](#get_account) | Account | CALL THIS FIRST. |
| [`get_format`](#get_format) | Free | The format's current template, its version history and the shows that run it, with each show's pin. |
| [`get_site_plan`](#get_site_plan) | Free | Returns the plan for a site: the videos it should have, each with a goal, a pitch, an audience, a ready creative brief and the shots it needs — and, for each, t |
| [`get_storyboard`](#get_storyboard) | Account | Returns the scene-by-scene plan of a video: what each scene narrates, its on-screen caption, how long it holds, and whether it is real footage of the page or a  |
| [`get_video`](#get_video) | Account | Reports how far a PageToVid render has got and, once it is finished, returns the video, poster and subtitle links. |
| [`get_video_embed`](#get_video_embed) | Free | Returns ready-to-paste markup for a finished PageToVid video: an HTML video element, Open Graph and Twitter player meta tags so the page unfurls as a playable v |
| [`inspect_page`](#inspect_page) | Free | Opens a public web page in a real browser and lists what a video could point its camera at, ranked: calls to action, product images, cards, pricing blocks, test |
| [`list_assets`](#list_assets) | Free | Your PRIVATE bank: every image and clip this account generated, uploaded or captured, newest first, with its id, URL, brief and tags. |
| [`list_characters`](#list_characters) | Free | The reusable characters on this account, each with its reference images and description. |
| [`list_commons_assets`](#list_commons_assets) | Free | Media people shared from their banks for anyone to use in a film — logos, product shots, illustrations, recorded flows — with tags, a licence and the site to cr |
| [`list_connections`](#list_connections) | Free | Every registered connection with its alias, kind and URL. |
| [`list_formats`](#list_formats) | Free | The account's formats, newest change first, with versions and the shows running each. |
| [`list_motions`](#list_motions) | Free | List animations, motions, visuals and chart types. |
| [`list_shows`](#list_shows) | Account | Lists the shows on this account — or one site's — with their cadence, caps, whether each is confirmed or still held, what it spent today, and its five most rece |
| [`list_themes`](#list_themes) | Free | Lists what the theme parameter accepts: the built-in presets, the modes, the type faces the renderer can actually load, and the contrast and palette rules that  |
| [`list_video_options`](#list_video_options) | Free | Lists what create_video accepts: goals, aspect ratios, languages, voices, background music beds (eight, each with a family: calm, energetic, serious, playful) a |
| [`list_videos`](#list_videos) | Account | Lists videos newest first with their status and, when finished, their links. |
| [`preview_episode`](#preview_episode) | Free | Runs the format's resolvers against the item (real upstream calls, cached where the format says so), compiles the storyboard and returns every beat's final text |
| [`register_mcp_connection`](#register_mcp_connection) | Free | Registers (or replaces) a connection by alias: the URL and, optionally, a credential kept encrypted on this account. |
| [`rerender_video`](#rerender_video) | 1 credit | Produces a new film from the video's current storyboard, skipping the page analysis and scripting that create_video does. |
| [`run_show`](#run_show) | 1 credit | Per episode started. |
| [`update_format`](#update_format) | Free | Changes any of a format's template fields. |
| [`update_show`](#update_show) | Free | Changes a show's switch, cadence, caps or name, or moves it to another format or format version. |
| [`update_storyboard`](#update_storyboard) | Free | Changes a video's storyboard: rewrite what a scene says, change its caption or heading, redraw it as a different visual, correct its data, tint it, point its ca |
| [`validate_format`](#validate_format) | Free | Compiles the template against a sample item without touching the database or any feed: the catalogue checks (voice, music, language, theme…), the scene template |
| [`verify_episode`](#verify_episode) | Free | The proof behind a film. |

1. TOC
{:toc}

## cancel_video

**Cost:** Free · destructive

Stops a render that is still running and returns every credit it spent — the render credit and any AI stills or clips it had already generated. Use it the moment get_storyboard shows a plan you do not want: a film takes several minutes, and without this the only option was to watch it finish. A render that has already finished cannot be cancelled, and is reported as such rather than refunded. The worker is not killed mid-frame; it stops at its next step, and the video is marked as cancelled straight away.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `video_id` | string | yes | The running video to stop. |

## create_animation

**Cost:** 1 credit

Make a video from data. Create, make, generate or render an animated video, explainer, data video or chart video from content you already have — figures, a table, notes, an idea — with NO website and NO URL required. This is the tool for turning numbers or text you are holding into a finished MP4 with narration and captions. You supply the scenes; PageToVid draws each as a motion graphic (charts, big numbers, comparisons, timelines, quotes, title cards), records an AI voiceover, burns captions and renders it. Call list_motions first for the 19 visuals, what each one needs, and the animations it accepts. Rendering is asynchronous: this returns a video_id immediately and get_video reports progress. get_video, get_storyboard, update_storyboard, rerender_video and get_video_embed all work on the result exactly as they do for a filmed video.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `scenes` | array | yes | The scenes to draw, in order, 1-20. Every one is validated before anything is created or charged. The render costs 1 credit; on top of that each scene that generates an AI visual is metered — a still (data.generate) 1, a clip (data.clip) 4 — charged per visual, refunded if one fails, and skipped if you run out. get_account returns credit_costs. |
| `aspect_ratio` | `16:9` · `9:16` · `1:1` |  | 16:9 for web and YouTube, 9:16 for Reels/Shorts/TikTok, 1:1 for feeds. Default `"16:9"`. |
| `language` | `en` · `fr` · `es` · `de` · `it` · `pt` · `nl` |  | Language of the voiceover and captions. Write the narration in this language. Default `"en"`. |
| `voice` | `auto` · `Kore` · `Zephyr` · `Puck` · `Charon` · `Aoede` · `Fenrir` · `Leda` · `Orus` · `Callirrhoe` · `Achird` · `Sulafat` · `Sadachbia` |  | Voice character (every voice is multilingual). auto picks a voice that fits the goal and tone and differs from the site's previous films; name one to fix it. Default `"auto"`. |
| `music` | `auto` · `none` · `uplift` · `corporate` · `chill` · `cinematic` · `ambient` · `pulse` · `playful` · `warm` |  | Background music bed, or "none". auto fits the goal and differs from the site's previous films; name one to fix it. Only the listed ids — these are tracks, not a style prompt. Default `"auto"`. |
| `tone` | string |  | Delivery of the narration, up to 80 characters — e.g. energetic, calm, authoritative, or a short direction like "dry and deadpan, like a friend telling a story". Default `"energetic"`. |
| `subtitles` | boolean |  | Burn captions into the picture and emit a .vtt sidecar. Default `true`. |
| `intro` | boolean |  | Include the branded opening title card. Default `true`. |
| `outro` | boolean |  | Include the closing call-to-action card. Default `true`. |
| `target_seconds` | integer |  | How long the film should be. Here it is a CHECK, not a setting: you wrote the narration and a narrated scene lasts exactly as long as its words, so nothing can stretch or shrink it. If the script misses this by more than 15%, the call is refused before any credit moves, and the refusal says how many words 45 seconds actually carries and how many to cut or add. Omit it and any length between 15 and 180 s is accepted. Range 15–180. |
| `title` | string |  | Name for the video. Defaults to the first scene's heading. |
| `brand_name` | string |  | Name shown on the intro and outro cards. |
| `cta_text` | string |  | Call to action on the closing card. |
| `source_url` | string |  | Attribution only — where the material came from. Nothing is fetched from it and no page is filmed. |
| `theme` | object |  | The film's visual identity: palette, type and mode. Call list_themes for the presets and the rules, or detect_brand to read a site's own. Omitted, an animation uses the house palette and a filmed video adopts whatever the page's CSS says. |
| `look` | `clean` · `bold` · `editorial` · `playful` · `tech` · `auto` |  | The film's LOOK: captions, cutting, sound cues, music family and motion register chosen together. auto picks one from the goal, the shape and the site's film count, so two films of a site differ; list_video_options describes each. Default `"auto"`. |
| `caption_style` | `karaoke` · `bold` · `boxed` · `minimal` · `outline` |  | Caption style overriding the look's own; omit it to keep the look's. |
| `caption_animation` | `none` · `pop` · `bounce` · `wave` · `glow` · `slide` |  | What a caption's word does when it is spoken, overriding the look's own. |
| `caption_emphasis` | `manual` · `auto` · `none` |  | Which caption words are drawn in the brand colour: the ones the script wraps in **asterisks** (manual), those plus figures and shouted words (auto), or none. |
| `grade` | `none` · `warm` · `cool` · `vivid` · `mono` · `vintage` · `contrast` |  | Colour grade for the footage, overriding the look's own. Never touches the captions or a card's type. |
| `sfx_level` | `off` · `subtle` · `full` |  | How loud the sound-design layer is, overriding the look's own. |
| `callout` | `none` · `ring` · `arrow` · `underline` · `dim` |  | What is drawn over a screencast to point at the subject: a ring, an arrow, an underline, a dimmed surround, or none. |
| `cursor_style` | `arrow` · `hand` · `dot` · `none` |  | The pointer the recording draws: the system arrow, a pointing hand, a presenter's dot, or none. |
| `press_effect` | `punch` · `freeze` · `slowmo` · `none` |  | What the picture does when the cursor presses something: punch in, freeze for a beat, half speed, or nothing. |
| `end_screen` | `cta` · `qr` · `social` · `logo` · `none` |  | The closing card: the call to action, the same with a scannable code to the film's page, the brand's handles, the mark alone, or no card. |
| `ai_budget` | object |  | A ceiling on AI generation for this render, so a plan full of clips cannot surprise you with the bill. Generation is metered (1 credit a still, 4 a clip, on top of 1 for the render), and the response always returns ai_plan with what was asked for and the estimated cost. Omitted, nothing is capped. |
| `idempotency_key` | string |  | A caller-chosen id for this request. Sending the same key again within 24 hours returns the original video instead of rendering and charging a second time — use it if your client may retry. |

## create_character

**Cost:** Free or 1 credit

Names a character so a generated clip that names it keeps the same identity across scenes (Veo 3.1 ingredients-to-video). Give refs — 1 to 3 reference image URLs on this account — or a generate prompt to DRAW the reference here (1 image credit, refunded if it fails; naming a character from refs you already have is free). Then set an animation image scene's data.clip=true and data.character="<name>" to make a moving beat with that character. Building one from a film you already made: take a scene's raw_frame_url from get_storyboard, never its thumbnail_url — the thumbnail is cut from the finished video and carries the headline and caption burnt into the picture, and a reference image with text in it teaches the generator to draw text.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `name` | string | yes | The character's name, e.g. "Ada, the founder". A clip scene names it in data.character to stay consistent. |
| `refs` | array |  | 1 to 3 reference image URLs — media on this account (a generated still, a bank asset, a commons asset from list_commons_assets). These become Veo's ingredients so the same character recurs. Give these OR a generate prompt. |
| `generate` | string |  | Draw the reference portrait instead of supplying one — e.g. "a woman in her late twenties, platinum blonde, grey tee". Costs 1 image credit, refunded if it fails. Ignored when refs are given. |
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
| `goal` | `explainer` · `ad` · `demo` · `tutorial` · `article` |  | What the video is for. Shapes the script's structure and pacing. Default `"explainer"`. |
| `aspect_ratio` | `16:9` · `9:16` · `1:1` |  | 16:9 for web and YouTube, 9:16 for Reels/Shorts/TikTok, 1:1 for feeds. Default `"16:9"`. |
| `language` | `en` · `fr` · `es` · `de` · `it` · `pt` · `nl` |  | Language of the voiceover and captions. Write the narration in this language. Default `"en"`. |
| `target_seconds` | integer |  | How long the film should be. Here it is a CHECK, not a setting: you wrote the narration and a narrated scene lasts exactly as long as its words, so nothing can stretch or shrink it. If the script misses this by more than 15%, the call is refused before any credit moves, and the refusal says how many words 45 seconds actually carries and how many to cut or add. Omit it and any length between 15 and 180 s is accepted. Range 15–180. |
| `tone` | string |  | Delivery of the narration, up to 80 characters — e.g. energetic, calm, authoritative, or a short direction like "dry and deadpan, like a friend telling a story". Default `"energetic"`. |
| `voice` | `auto` · `Kore` · `Zephyr` · `Puck` · `Charon` · `Aoede` · `Fenrir` · `Leda` · `Orus` · `Callirrhoe` · `Achird` · `Sulafat` · `Sadachbia` |  | Voice character (every voice is multilingual). auto picks a voice that fits the goal and tone and differs from the site's previous films; name one to fix it. Default `"auto"`. |
| `music` | `auto` · `none` · `uplift` · `corporate` · `chill` · `cinematic` · `ambient` · `pulse` · `playful` · `warm` |  | Background music bed, or "none". auto fits the goal and differs from the site's previous films; name one to fix it. Only the listed ids — these are tracks, not a style prompt. Default `"auto"`. |
| `subtitles` | boolean |  | Burn captions into the picture and emit a .vtt sidecar. Default `true`. |
| `intro` | boolean |  | Include the branded opening title card. Default `true`. |
| `outro` | boolean |  | Include the closing call-to-action card. Default `true`. |
| `brand_name` | string |  | Name shown on the intro and outro cards. |
| `theme` | object |  | The film's visual identity: palette, type and mode. Call list_themes for the presets and the rules, or detect_brand to read a site's own. Omitted, an animation uses the house palette and a filmed video adopts whatever the page's CSS says. |
| `focus_template` | string |  | video formats: the brief every episode's script writer gets, with {{title}} {{summary}} {{link}} {{date}} {{image}} {{show}} {{site}} filled from the item. |
| `title_template` | string |  | animation formats: the episode's title, same placeholders. Default "{{show}} — {{title}}". |
| `scenes` | array |  | animation formats: the scene templates, as create_animation takes scenes, with the placeholders in any string. |
| `programme` | object |  | animation formats: the programme instead of plain scenes. {beats: [...], resolvers: [...], computed: {...}, requires_beats: [...], reject_if: [...]}. A beat is a scene (visual, motion, mood, heading, caption, narration, data) plus beat (one of cold_open, title, identity, context, trend, breakdown, outlier, comparison, caveats, verdict, sources), when (an expression; dropped when not true) and for_each (an expression yielding a list; repeated per element). Any string may carry {{ expressions }} — dotted paths and filters such as money(EUR,M), percent(0), say, sort_by(year), take_last(6), map({label: year, value: total}) — and any field may be {"$bind": "expression"} to receive a real number, list or object (a chart's points). Resolvers fetch data before compiling: {id, call: {mcp: alias, tool, input} | {http: url, query, body}, select, required, on_missing: skip_episode | drop_beats(a,b) | use_default | fail_loud, cache: "30d"}; each reads what the ones before it bound. Every numeral in a narration or caption must come from an expression: a figure typed by hand fails validation by beat. validate_format checks the template; preview_episode runs the resolvers and compiles a real episode for free. |
| `routing` | object |  | How episodes are made: {planner?: flash|pro, footage?: prefer-recorded|record-fresh}. flash is the benched default (it beat every larger model under the real prompt); pro is a deliberate choice. prefer-recorded uses the site's banked flow recordings when they match a scene; record-fresh films every episode anew, for a subject that changes each time. |

## create_show

**Cost:** Free

A show makes a video from each new item in a feed — the same storyboard every episode, new data every episode: a weekly release video from a changelog, a daily listing video from an RSS feed, a clip per new post. Episodes are ordinary videos (1 credit each) made by run_show or, once confirmed, by the scheduler at the show's cadence. A new show is HELD: nothing renders until its owner has called run_show once with confirm=true, and it never spends more than max_credits_per_day. Returns the show and what to do next.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `site_url` | string | yes | Any public http(s) URL on the site; the site is identified by its domain. |
| `name` | string | yes | The show's name, e.g. "Le mot du chantier". Available as {{show}} in templates. |
| `kind` | `video` · `animation` |  | video: each episode films the item's own page (like create_video) with focus_template as its brief. animation: each episode is drawn from `scenes` (like create_animation) with the item's data filled in. Default `"video"`. |
| `feed_kind` | `rss` · `json` · `manual` · `query` · `watchlist` · `webhook` |  | rss: an RSS or Atom feed. json: a JSON Feed, or any JSON API read through feed_map. query: the items come from `source` — one call on a registered connection (register_mcp_connection), run at every run. watchlist: a fixed list of items in `watchlist`. webhook: items are POSTed to the show's webhook URL by another system (a CMS on publish, CI on release), signed with the secret create_show returns once (X-PageToVid-Signature: sha256=HMAC of the body); cadence manual; a confirmed show makes the episodes within its caps. manual: no feed — items are passed to run_show each time, and the show cannot be scheduled. Default `"rss"`. |
| `feed_url` | string |  | The feed's public URL for rss and json. It is read once now to make sure it parses. |
| `source` | object |  | feed_kind query: {call: {mcp: alias, tool, input} | {http: url, query}, select: an expression into the answer that yields the list, map: dotted paths from an element to the item ({id, title, summary, link, image, date})}. Strings in the input may carry {{ show }}, {{ site }} and {{ now }}. Called once now to make sure it answers. |
| `watchlist` | array |  | feed_kind watchlist: the items, as run_show takes them. Each is made once — or once per period with repeat_every. |
| `repeat_every` | `none` · `month` · `quarter` · `year` |  | query and watchlist shows: make every item again each period (the period is in the episode key and available to a programme as {{ item.period }}). none: each item once, ever. Default `"none"`. |
| `feed_map` | object |  | For feed_kind json when the document is not a JSON Feed: dotted paths, e.g. {"items":"data.results","id":"slug","title":"name","summary":"excerpt","link":"href","image":"cover.url","date":"published_at"}. `items` may be omitted when the document is an array. |
| `cadence` | `manual` · `hourly` · `daily` · `weekly` |  | How often the scheduler runs the show once it is confirmed. manual: only when run_show is called. Default `"daily"`. |
| `max_episodes_per_run` | integer |  | Newest items first; at most this many episodes per run. Default `1`. Range 1–10. |
| `max_credits_per_day` | integer |  | The show never spends more than this in a UTC day, however many items the feed gains. Default `3`. Range 1–50. |
| `format_id` | string |  | Run an existing format (create_format / list_formats) instead of the fields below; its kind must match. Without it, the fields below become the show's own format, version 1, editable later with update_format. |
| `format_version` | integer |  | With format_id: pin the show to this version. Omitted, the show follows the format's latest version. Range 1–100000. |
| `goal` | `explainer` · `ad` · `demo` · `tutorial` · `article` |  | What the video is for. Shapes the script's structure and pacing. Default `"explainer"`. |
| `aspect_ratio` | `16:9` · `9:16` · `1:1` |  | 16:9 for web and YouTube, 9:16 for Reels/Shorts/TikTok, 1:1 for feeds. Default `"16:9"`. |
| `language` | `en` · `fr` · `es` · `de` · `it` · `pt` · `nl` |  | Language of the voiceover and captions. Write the narration in this language. Default `"en"`. |
| `target_seconds` | integer |  | How long the film should be. Here it is a CHECK, not a setting: you wrote the narration and a narrated scene lasts exactly as long as its words, so nothing can stretch or shrink it. If the script misses this by more than 15%, the call is refused before any credit moves, and the refusal says how many words 45 seconds actually carries and how many to cut or add. Omit it and any length between 15 and 180 s is accepted. Range 15–180. |
| `tone` | string |  | Delivery of the narration, up to 80 characters — e.g. energetic, calm, authoritative, or a short direction like "dry and deadpan, like a friend telling a story". Default `"energetic"`. |
| `voice` | `auto` · `Kore` · `Zephyr` · `Puck` · `Charon` · `Aoede` · `Fenrir` · `Leda` · `Orus` · `Callirrhoe` · `Achird` · `Sulafat` · `Sadachbia` |  | Voice character (every voice is multilingual). auto picks a voice that fits the goal and tone and differs from the site's previous films; name one to fix it. Default `"auto"`. |
| `music` | `auto` · `none` · `uplift` · `corporate` · `chill` · `cinematic` · `ambient` · `pulse` · `playful` · `warm` |  | Background music bed, or "none". auto fits the goal and differs from the site's previous films; name one to fix it. Only the listed ids — these are tracks, not a style prompt. Default `"auto"`. |
| `subtitles` | boolean |  | Burn captions into the picture and emit a .vtt sidecar. Default `true`. |
| `intro` | boolean |  | Include the branded opening title card. Default `true`. |
| `outro` | boolean |  | Include the closing call-to-action card. Default `true`. |
| `brand_name` | string |  | Name shown on the intro and outro cards. |
| `theme` | object |  | The film's visual identity: palette, type and mode. Call list_themes for the presets and the rules, or detect_brand to read a site's own. Omitted, an animation uses the house palette and a filmed video adopts whatever the page's CSS says. |
| `focus_template` | string |  | video shows: the brief every episode's script writer gets, with {{title}} {{summary}} {{link}} {{date}} {{image}} {{show}} {{site}} filled from the item. Anything written here may be voiced as fact. Omitted, a default brief leads with the item's title and summary. |
| `title_template` | string |  | animation shows: the episode's title, same placeholders. Default "{{show}} — {{title}}". |
| `scenes` | array |  | animation shows: the scene templates, exactly as create_animation takes scenes, with the placeholders in any string. An image or gallery scene whose {{image}} is empty for an item is dropped from that episode. Validated now against a sample item, so a broken template is refused here rather than on its first scheduled run. |
| `routing` | object |  | How episodes are made: {planner?: flash|pro, footage?: prefer-recorded|record-fresh}. flash is the benched default (it beat every larger model under the real prompt); pro is a deliberate choice. prefer-recorded uses the site's banked flow recordings when they match a scene; record-fresh films every episode anew, for a subject that changes each time. |

## create_video

**Cost:** 1 credit

Starts a PageToVid render that turns a public web page URL into a narrated video with an AI voiceover, motion graphics and optional subtitles. Rendering is asynchronous and usually takes several minutes but can run past fifteen for a heavy page or a busy queue; this returns a video_id immediately, and get_video reports the phase, the progress and an estimate recalculated from how long this particular render has already taken. The page must be publicly reachable — a page behind a login is filmed only when a capture session was registered for the site from the VS Code or browser extension.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `url` | string | yes | Public http(s) URL of the page to film. You must have the right to make a video from this page. |
| `goal` | `explainer` · `ad` · `demo` · `tutorial` · `article` |  | What the video is for. Shapes the script's structure and pacing. Default `"explainer"`. |
| `aspect_ratio` | `16:9` · `9:16` · `1:1` |  | 16:9 for web and YouTube, 9:16 for Reels/Shorts/TikTok, 1:1 for feeds. The shape chooses the device: 9:16 films the page's own MOBILE layout in a 414×736 phone viewport at 3× with an iPhone user agent (breakpoints, touch targets, stacked sections); 16:9 and 1:1 film the 1280-wide desktop layout. Nothing is squeezed from one into the other. Default `"16:9"`. |
| `language` | `en` · `fr` · `es` · `de` · `it` · `pt` · `nl` |  | Language of the script and voiceover. These are the languages PageToVid verifies end to end. Default `"en"`. |
| `target_seconds` | integer |  | Target length in seconds. The finished film is measured against this, not estimated. Default `45`. Range 15–180. |
| `subtitles` | boolean |  | Burn captions into the picture and emit a .vtt sidecar. Default `true`. |
| `tone` | string |  | Delivery of the narration, up to 80 characters — e.g. energetic, calm, authoritative, or a short direction like "dry and deadpan, like a friend telling a story". Default `"energetic"`. |
| `voice` | `auto` · `Kore` · `Zephyr` · `Puck` · `Charon` · `Aoede` · `Fenrir` · `Leda` · `Orus` · `Callirrhoe` · `Achird` · `Sulafat` · `Sadachbia` |  | Voice character (every voice is multilingual). auto picks a voice that fits the goal and tone and differs from the site's previous films; name one to fix it. Default `"auto"`. |
| `music` | `auto` · `none` · `uplift` · `corporate` · `chill` · `cinematic` · `ambient` · `pulse` · `playful` · `warm` |  | Background music bed, or "none". auto fits the goal and differs from the site's previous films; name one to fix it. Only the listed ids — these are tracks, not a style prompt. Default `"auto"`. |
| `brand_name` | string |  | Name shown on the intro and outro cards. Defaults to the site's own name. |
| `focus` | string |  | Context the page cannot show, treated as authoritative by the script writer: a launch or offer to lead with, the audience, a referral code, something to avoid. Anything written here may be voiced as FACT in the finished film — an angle and a claim are not distinguished — so put only what you are prepared to have said in the customer’s voice. A line in quotation marks is placed verbatim, usually as the hook. |
| `idempotency_key` | string |  | A caller-chosen id for this request. Sending the same key again within 24 hours returns the original video instead of rendering and charging a second time — use it if your client may retry. |
| `theme` | object |  | The film's visual identity: palette, type and mode. Call list_themes for the presets and the rules, or detect_brand to read a site's own. Omitted, an animation uses the house palette and a filmed video adopts whatever the page's CSS says. |
| `intro` | boolean |  | Include the branded opening title card. Defaults to true, EXCEPT for goal "ad", where it defaults to false: the card is 1.5s, a view is counted at 3s, and about 47% of a campaign's measured value lands in that window — an ad should open on the hook, not a logo. Pass it explicitly to override either way. Default `true`. |
| `outro` | boolean |  | Include the closing call-to-action card. Default `true`. |
| `routing` | object |  | How the film is MADE, as opposed to what it says: {planner?: flash|pro, footage?: prefer-recorded|record-fresh}. flash is the benched default and beat every larger model under this prompt, so pro is a deliberate choice rather than an upgrade. prefer-recorded reuses the site's banked flow recordings when one matches a scene — footage of the product as it really behaved; record-fresh films everything anew, for a page whose content changes between renders. |
| `look` | `clean` · `bold` · `editorial` · `playful` · `tech` · `auto` |  | The film's LOOK: captions, cutting, sound cues, music family and motion register chosen together. auto picks one from the goal, the shape and the site's film count, so two films of a site differ; list_video_options describes each. Default `"auto"`. |
| `caption_style` | `karaoke` · `bold` · `boxed` · `minimal` · `outline` |  | Caption style overriding the look's own; omit it to keep the look's. |
| `caption_animation` | `none` · `pop` · `bounce` · `wave` · `glow` · `slide` |  | What a caption's word does when it is spoken, overriding the look's own. |
| `caption_emphasis` | `manual` · `auto` · `none` |  | Which caption words are drawn in the brand colour: the ones the script wraps in **asterisks** (manual), those plus figures and shouted words (auto), or none. |
| `grade` | `none` · `warm` · `cool` · `vivid` · `mono` · `vintage` · `contrast` |  | Colour grade for the footage, overriding the look's own. Never touches the captions or a card's type. |
| `sfx_level` | `off` · `subtle` · `full` |  | How loud the sound-design layer is, overriding the look's own. |
| `callout` | `none` · `ring` · `arrow` · `underline` · `dim` |  | What is drawn over a screencast to point at the subject: a ring, an arrow, an underline, a dimmed surround, or none. |
| `cursor_style` | `arrow` · `hand` · `dot` · `none` |  | The pointer the recording draws: the system arrow, a pointing hand, a presenter's dot, or none. |
| `press_effect` | `punch` · `freeze` · `slowmo` · `none` |  | What the picture does when the cursor presses something: punch in, freeze for a beat, half speed, or nothing. |
| `end_screen` | `cta` · `qr` · `social` · `logo` · `none` |  | The closing card: the call to action, the same with a scannable code to the film's page, the brand's handles, the mark alone, or no card. |

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

**Cost:** 1 or 4 credits

Generates a single AI still (1 credit) or clip (4 credits) straight into your media bank and returns its id and URL — no project, no render, no minimum length. Use it for character reference portraits, or for any visual you want to see before it goes into a film. The charge is taken before the call and refunded automatically if the generation fails; identical output is de-duplicated, so a repeat does not cost a second file. Generation is a paid-plan feature.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `kind` | `image` · `video` |  | image (a still) or video (a clip). Default image. |
| `prompt` | string | yes | What to draw or film. |
| `aspect_ratio` | `16:9` · `9:16` · `1:1` |  | Shape of the asset. Default 16:9. |
| `character` | string |  | A character from create_character, so the same face comes back. |
| `tags` | string |  | Comma-separated tags, to find it again. |
| `site_url` | string |  | Attach it to one of your sites. |

## generate_site_videos

**Cost:** 1 credit

Per video started. Starts a video for each idea in the site's plan (see get_site_plan) that has none yet, or for the idea_ids given. Each is an ordinary filmed video — the idea's brief becomes its focus — and each costs one credit when it starts. Called without confirm it only lists what it would make and what that costs; nothing is created. Rendering is asynchronous: get_video reports each one. A retried call does not start the same idea twice.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `site_url` | string | yes | Any public http(s) URL on the site; the site is identified by its domain. |
| `idea_ids` | array |  | Which ideas from get_site_plan to make, in order. Omitted: every idea that has no video yet. |
| `url` | string |  | The page to film. Defaults to the site's home page; the planner follows the site's own links from there. |
| `aspect_ratio` | `16:9` · `9:16` · `1:1` |  | 16:9 for web and YouTube, 9:16 for Reels/Shorts/TikTok, 1:1 for feeds. Default `"16:9"`. |
| `language` | `en` · `fr` · `es` · `de` · `it` · `pt` · `nl` |  | Language of the voiceover and captions. Write the narration in this language. Default `"en"`. |
| `voice` | `auto` · `Kore` · `Zephyr` · `Puck` · `Charon` · `Aoede` · `Fenrir` · `Leda` · `Orus` · `Callirrhoe` · `Achird` · `Sulafat` · `Sadachbia` |  | Voice character (every voice is multilingual). auto picks a voice that fits the goal and tone and differs from the site's previous films; name one to fix it. Default `"auto"`. |
| `music` | `auto` · `none` · `uplift` · `corporate` · `chill` · `cinematic` · `ambient` · `pulse` · `playful` · `warm` |  | Background music bed, or "none". auto fits the goal and differs from the site's previous films; name one to fix it. Only the listed ids — these are tracks, not a style prompt. Default `"auto"`. |
| `subtitles` | boolean |  | Burn captions into the picture and emit a .vtt sidecar. Default `true`. |
| `intro` | boolean |  | Include the branded opening title card. Default `true`. |
| `outro` | boolean |  | Include the closing call-to-action card. Default `true`. |
| `brand_name` | string |  | Name shown on the intro and outro cards. |
| `theme` | object |  | The film's visual identity: palette, type and mode. Call list_themes for the presets and the rules, or detect_brand to read a site's own. Omitted, an animation uses the house palette and a filmed video adopts whatever the page's CSS says. |
| `look` | `clean` · `bold` · `editorial` · `playful` · `tech` · `auto` |  | The film's LOOK: captions, cutting, sound cues, music family and motion register chosen together. auto picks one from the goal, the shape and the site's film count, so two films of a site differ; list_video_options describes each. Default `"auto"`. |
| `caption_style` | `karaoke` · `bold` · `boxed` · `minimal` · `outline` |  | Caption style overriding the look's own; omit it to keep the look's. |
| `confirm` | boolean |  | false (the default) previews the videos and spends nothing. true starts them and spends one credit each. Default `false`. |
| `max_videos` | integer |  | At most this many videos in one call. Call again for the rest. Default `5`. Range 1–10. |

## get_account

**Cost:** Account · read-only

CALL THIS FIRST. What this account may do and what it will be charged: the plan, the credits left, whether AI stills and clips are available and whether they cost anything here, whether finished videos carry a watermark, how many renders are running, and the length and rate limits. The usual order after this is inspect_page on each page you might film (in the aspect ratio you will film it in), then create_video or create_animation, then get_storyboard — which is free and is the only place the shots the planner actually chose are visible — then update_storyboard and rerender_video.

_No parameters._

## get_format

**Cost:** Free · read-only

The format's current template, its version history and the shows that run it, with each show's pin.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `format_id` | string | yes | The format_id from create_format or list_formats. |

## get_site_plan

**Cost:** Free

Returns the plan for a site: the videos it should have, each with a goal, a pitch, an audience, a ready creative brief and the shots it needs — and, for each, the video already made from it on this account, if any. Generated on first call from the site's own pages (text-only, no credit), stored, and returned as is afterwards. This is the list generate_site_videos works from.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `site_url` | string | yes | Any public http(s) URL on the site; the site is identified by its domain. |
| `language` | `en` · `fr` · `es` · `de` · `it` · `pt` · `nl` |  | Language the ideas and shot list are written in. This is the planner's working language, not the videos' — generate_site_videos sets that. Default `"en"`. |
| `refresh` | boolean |  | true regenerates the plan even if one exists, overwriting it. A plan is generated automatically the first time. Default `false`. |

## get_storyboard

**Cost:** Account · read-only

Returns the scene-by-scene plan of a video: what each scene narrates, its on-screen caption, how long it holds, and whether it is real footage of the page or a motion graphic (and which motion).

| Parameter | Type | Required | Description |
|---|---|---|---|
| `video_id` | string | yes | The video_id to read. |

## get_video

**Cost:** Account · read-only

Reports how far a PageToVid render has got and, once it is finished, returns the video, poster and subtitle links. While a render is in progress the result includes a suggested number of seconds to wait before checking again. `status` is one of, in pipeline order: draft, queued, analyzing, scripting, recording, voicing, rendering, done, error. In flight, so poll again after poll_after_seconds: queued, analyzing, scripting, recording, voicing, rendering. Terminal, so stop polling: done, error — a cancelled render ends as error with the reason in `error`, and a film can be done and still carry warnings. draft has not been queued.

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

## inspect_page

**Cost:** Free · read-only

Opens a public web page in a real browser and lists what a video could point its camera at, ranked: calls to action, product images, cards, pricing blocks, testimonials, search and chat boxes, headings and sections — each with a CSS selector, a size and a score for how much a viewer wants to look at it. It also says when the browser was shown a robot check, a sign-in or an error page instead of the real one (blocked, block_kind), so a film is never shot on the wall in front of a site. Also lists the text fields that will never be typed into, and why. This is the same ranking the script planner reads when it decides the shots, so it is what to look at before asking for a particular one. No video is made and no credit is spent.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `url` | string | yes | A public page to look at. Nothing is filmed and no credit is spent. |
| `aspect_ratio` | `16:9` · `9:16` · `1:1` |  | The viewport to look through. 9:16 loads the page as a phone does, which is the layout a vertical video films — a responsive site offers different elements there (a sticky call bar, stacked cards) and they score differently. |
| `limit` | integer |  | How many candidates to return, best first. A dense page offers up to 40 and a film needs four or five; the rest are the largest single thing this surface puts in a context window. The `kinds` histogram still counts every one, so nothing is hidden — raise this only when the shortlist has nothing you want. Default `12`. Range 1–40. |
| `kinds` | string |  | Comma-separated kinds to keep, e.g. "cta,search,card". The vocabulary is in the `kinds` histogram of any reply: cta, media, image, card, pricing, testimonial, logos, heading, section, nav, search, chat, input. Omitted, every kind is offered. |

## list_assets

**Cost:** Free · read-only

Your PRIVATE bank: every image and clip this account generated, uploaded or captured, newest first, with its id, URL, brief and tags. list_commons_assets only shows what other people shared, so anything you generated yourself was invisible. Reuse one by putting its id in an image scene as data.asset_id — a clip resolves to clipUrl by itself, and a URL still works. Reusing costs no credit and generates nothing.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `kind` | `image` · `video` |  | Only images, or only clips. |
| `q` | string |  | A word to find in the brief or the tags. |
| `character` | string |  | Only assets generated for this character. |
| `site_url` | string |  | Only assets attached to this site. |
| `limit` | integer |  | At most this many, newest first (default 40). Range 1–200. |

## list_characters

**Cost:** Free · read-only

The reusable characters on this account, each with its reference images and description. Credentials are never involved; these are just image references.

_No parameters._

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

## list_motions

**Cost:** Free · read-only

List animations, motions, visuals and chart types. The catalogue of what a scene can be drawn as — chart, big number, comparison, timeline, checklist, quote, table, title card and twelve more — and the named entrance animations each accepts, grouped by feel (calm, elegant, bold, playful, dramatic, techy). Free, no account access, no credit. Call this before create_animation or update_storyboard so a scene is given a visual and an animation that exist and go together; a mismatched pair is refused, not silently swapped.

_No parameters._

## list_shows

**Cost:** Account · read-only

Lists the shows on this account — or one site's — with their cadence, caps, whether each is confirmed or still held, what it spent today, and its five most recent episodes with the video each became.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `site_url` | string |  | Only this site's shows. Omitted: every show on the account. |

## list_themes

**Cost:** Free · read-only

Lists what the theme parameter accepts: the built-in presets, the modes, the type faces the renderer can actually load, and the contrast and palette rules that are enforced before a credit moves. Static reference data — no account access, no page fetched, free.

_No parameters._

## list_video_options

**Cost:** Free · read-only

Lists what create_video accepts: goals, aspect ratios, languages, voices, background music beds (eight, each with a family: calm, energetic, serious, playful) and the allowed length range. Static reference data — no account access.

_No parameters._

## list_videos

**Cost:** Account · read-only

Lists videos newest first with their status and, when finished, their links. Filter by status or by a word in the page URL or title. Returns a cursor when more remain.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `status` | `any` · `queued` · `analyzing` · `scripting` · `recording` · `voicing` · `rendering` · `done` · `error` |  | Only videos in this state. Default `"any"`. |
| `query` | string |  | Matches part of the source URL or the title. |
| `created_after` | string |  | ISO 8601 timestamp; only videos created after it. |
| `cursor` | string |  | The next_cursor from a previous call. Opaque — pass it back unchanged. |
| `limit` | integer |  | How many to return. Default `10`. Range 1–50. |

## preview_episode

**Cost:** Free · read-only

Runs the format's resolvers against the item (real upstream calls, cached where the format says so), compiles the storyboard and returns every beat's final text, the beats dropped and why, the integrity report (hand-written numbers, missing required beats, rejections, length against the brief), the upstream calls made with their timing, and where every bound value came from. Nothing is rendered and no credit moves. This is what to read before run_show confirm=true.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `format_id` | string | yes | The format_id from create_format or list_formats. |
| `format_version` | integer |  | Preview this version; omitted, the latest. Range 1–100000. |
| `item` | object |  | The item to make the episode of: {title, summary, link, image, date}. Omitted, a sample item. |

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

## rerender_video

**Cost:** 1 credit · destructive

Produces a new film from the video's current storyboard, skipping the page analysis and scripting that create_video does. Consumes one PageToVid credit — except once per video when the finished film missed its own length target (get_video reports length_within_tolerance: false): that correction is ours, and free. With captions_only true it only re-times the subtitles on the film's existing voice track (no re-recording, no new take), free once per render. The previous video file is replaced once the new render finishes.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `video_id` | string | yes | The video to re-render. |
| `theme` | object |  | The film's visual identity: palette, type and mode. Call list_themes for the presets and the rules, or detect_brand to read a site's own. Omitted, an animation uses the house palette and a filmed video adopts whatever the page's CSS says. Set here it replaces the video's current theme and is kept for later re-renders. |
| `idempotency_key` | string |  | A caller-chosen id for this request. Sending the same key again within 24 hours returns the same re-render instead of starting and charging a second time — use it if your client may retry. |
| `captions_only` | boolean |  | true re-times the subtitles on the voice track the film already has and renders again — nothing is re-recorded, re-scripted or re-voiced, so only the caption timing changes. The first such resync after a paid render is free; the next one on the same render costs 1 credit. Use it when get_video's film has captions out of step with the voice. |
| `target_seconds` | integer |  | Re-baseline how long this film is MEANT to be. The target a video was created with is often a guess made before any content existed; when the film has legitimately grown or shrunk since, set it to what it should be now rather than cutting to satisfy the old number. It changes what length_within_tolerance is measured against and is kept for later re-renders. It does not change the film — the narration is still what sets the length. Range 15–180. |

## run_show

**Cost:** 1 credit

Per episode started. Reads the show's feed (or the items given), skips every item that already became an episode, and — within max_episodes_per_run and max_credits_per_day — starts one video per new item. Without confirm it returns the list it would make and spends nothing. On a held show, confirm=true is the owner's one-time approval: it makes the episodes and lets the scheduler run the show from then on.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `show_id` | string | yes | The show_id from create_show or list_shows. |
| `confirm` | boolean |  | false (the default): a free preview of the episodes this run would make. true: make them, and on a held show, confirm it — from then on the scheduler runs it at its cadence. Default `false`. |
| `items` | array |  | The items to make episodes from, for a manual show. A feed show ignores this and reads its feed. |

## update_format

**Cost:** Free

Changes any of a format's template fields. The result is a NEW version — the previous ones stay exactly as they were, and every episode already made keeps the version that made it. Shows following latest use the new version from their next run; pinned shows do not move until update_show moves them. Validated whole before anything is written.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `format_id` | string | yes | The format_id from create_format or list_formats. |
| `name` | string |  | A new name. |
| `note` | string |  | What this version changes, for the version history. |
| `goal` | `explainer` · `ad` · `demo` · `tutorial` · `article` |  | What the video is for. Shapes the script's structure and pacing. |
| `aspect_ratio` | `16:9` · `9:16` · `1:1` |  | 16:9 for web and YouTube, 9:16 for Reels/Shorts/TikTok, 1:1 for feeds. |
| `language` | `en` · `fr` · `es` · `de` · `it` · `pt` · `nl` |  | Language of the voiceover and captions. Write the narration in this language. |
| `target_seconds` | integer |  | How long the film should be. Here it is a CHECK, not a setting: you wrote the narration and a narrated scene lasts exactly as long as its words, so nothing can stretch or shrink it. If the script misses this by more than 15%, the call is refused before any credit moves, and the refusal says how many words 45 seconds actually carries and how many to cut or add. Omit it and any length between 15 and 180 s is accepted. Range 15–180. |
| `tone` | string |  | Delivery of the narration, up to 80 characters — e.g. energetic, calm, authoritative, or a short direction like "dry and deadpan, like a friend telling a story". |
| `voice` | `auto` · `Kore` · `Zephyr` · `Puck` · `Charon` · `Aoede` · `Fenrir` · `Leda` · `Orus` · `Callirrhoe` · `Achird` · `Sulafat` · `Sadachbia` |  | Voice character (every voice is multilingual). auto picks a voice that fits the goal and tone and differs from the site's previous films; name one to fix it. |
| `music` | `auto` · `none` · `uplift` · `corporate` · `chill` · `cinematic` · `ambient` · `pulse` · `playful` · `warm` |  | Background music bed, or "none". auto fits the goal and differs from the site's previous films; name one to fix it. Only the listed ids — these are tracks, not a style prompt. |
| `subtitles` | boolean |  | Burn captions into the picture and emit a .vtt sidecar. |
| `intro` | boolean |  | Include the branded opening title card. |
| `outro` | boolean |  | Include the closing call-to-action card. |
| `brand_name` | string |  | Name shown on the intro and outro cards. |
| `theme` | object |  | The film's visual identity: palette, type and mode. Call list_themes for the presets and the rules, or detect_brand to read a site's own. Omitted, an animation uses the house palette and a filmed video adopts whatever the page's CSS says. |
| `focus_template` | string |  | video formats: the brief every episode's script writer gets, with {{title}} {{summary}} {{link}} {{date}} {{image}} {{show}} {{site}} filled from the item. |
| `title_template` | string |  | animation formats: the episode's title, same placeholders. Default "{{show}} — {{title}}". |
| `scenes` | array |  | animation formats: the scene templates, as create_animation takes scenes, with the placeholders in any string. |
| `programme` | object |  | animation formats: the programme instead of plain scenes. {beats: [...], resolvers: [...], computed: {...}, requires_beats: [...], reject_if: [...]}. A beat is a scene (visual, motion, mood, heading, caption, narration, data) plus beat (one of cold_open, title, identity, context, trend, breakdown, outlier, comparison, caveats, verdict, sources), when (an expression; dropped when not true) and for_each (an expression yielding a list; repeated per element). Any string may carry {{ expressions }} — dotted paths and filters such as money(EUR,M), percent(0), say, sort_by(year), take_last(6), map({label: year, value: total}) — and any field may be {"$bind": "expression"} to receive a real number, list or object (a chart's points). Resolvers fetch data before compiling: {id, call: {mcp: alias, tool, input} | {http: url, query, body}, select, required, on_missing: skip_episode | drop_beats(a,b) | use_default | fail_loud, cache: "30d"}; each reads what the ones before it bound. Every numeral in a narration or caption must come from an expression: a figure typed by hand fails validation by beat. validate_format checks the template; preview_episode runs the resolvers and compiles a real episode for free. |
| `routing` | object |  | How episodes are made: {planner?: flash|pro, footage?: prefer-recorded|record-fresh}. flash is the benched default (it beat every larger model under the real prompt); pro is a deliberate choice. prefer-recorded uses the site's banked flow recordings when they match a scene; record-fresh films every episode anew, for a subject that changes each time. |

## update_show

**Cost:** Free

Changes a show's switch, cadence, caps or name, or moves it to another format or format version. The template itself is edited with update_format, which writes a new version and leaves every episode already made where it is. Nothing is rendered.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `show_id` | string | yes | The show_id from create_show or list_shows. |
| `active` | boolean |  | false pauses the show (the scheduler skips it, run_show refuses); true resumes it. |
| `cadence` | `manual` · `hourly` · `daily` · `weekly` |  | A new cadence. |
| `max_episodes_per_run` | integer |  | A new per-run cap. Range 1–10. |
| `max_credits_per_day` | integer |  | A new daily credit cap. Range 1–50. |
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

Changes a video's storyboard: rewrite what a scene says, change its caption or heading, redraw it as a different visual, correct its data, tint it, point its camera at a specific element of the page (set_shot: a selector from inspect_page with a click, typing, a hover or a spotlight — checked on the live page before the edit is accepted), add a scene, copy one, trim, remove or reorder them, or change the voice or background music. 18 operations, listed on the operations parameter. Costs no credit and does not re-render — call rerender_video to produce a new film from the edited storyboard. Every call is snapshotted, so an edit can be undone in the web editor.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `video_id` | string | yes | The video to edit. Its scene ids come from get_storyboard. |
| `operations` | array | yes | The changes to apply, in order. All are validated before any is written, so a bad batch changes nothing and nothing is charged; correcting a wrong figure is set_data plus one rerender_video, not a new video. Up to 20 per call. A name followed by (arguments) — a trailing ? marks an optional one. rewrite_narration(scene_id, narration) — Replace what a scene says. The film is as long as its voiceover, so this changes the length. set_caption(scene_id, caption) — Set or clear the on-screen caption of a scene. set_heading(scene_id, heading) — Rename a scene. The heading is the editor's label for it, not on-screen text. trim_scene(scene_id, duration_seconds) — Set how long a scene holds. Only a SILENT scene obeys this — a narrated one is as long as its narration. set_mood(scene_id, mood) — Tint a scene: a problem scene gets a red vignette and a little camera shake, a win scene a warm glow. set_shot(scene_id, selector, action?, text?, page_url?) — Only for a video made from a URL — there is nothing to film in one made from data. Point the camera: make a scene a screen recording of a specific element — a click on it, typing into it, a hover, a spotlight — or of the section around it, optionally on another page of the same site. THE BEST SHOT ON MOST PAGES IS ONE THAT DOES SOMETHING: click the call to action and let the page answer, or type a real query into the search box. A frame the camera merely drifts across is a screenshot that took longer. The selector is checked on the live page before the edit is accepted, which proves it matches SOMETHING, not that it matches what you meant: a selector hitting several elements films the first one in the page, and the result says so. remove_scene(scene_id) — Delete a scene. A storyboard must keep at least one. add_scene(heading, narration, caption?, selector?, shot_action?, shot_text?, page_url?, visual?, motion?, data?, mood?, duration_seconds?, after_scene_id?, before_scene_id?) — Insert a new scene. Without a visual the scene is a screen recording of the video's page, so it needs a video that filmed one, and it is framed by default, which on a dense page means a wide shot of unreadable text; point it somewhere with set_shot once get_storyboard has given you its scene_id. With a visual, it needs that visual's own fields in `data` (list_motions says which): a bignum with no number, or a grid with no cells, degrades to a plain card carrying whatever text it could find. duplicate_scene(scene_id) — Copy a scene, words, visual, data and all, straight after the original. Its heading gains a "copy" suffix, and it carries no recorded footage — the copy is filmed or drawn afresh on the next render. reorder_scenes(scene_ids) — Put the scenes in a new order. Must list every scene exactly once. set_visual(scene_id, visual, data?) — Change how a scene is drawn. Its content is carried over unless you send new data. set_transition(scene_id, transition, duration_ms?) — How a scene ARRIVES — the cut itself, as opposed to set_motion, which is how its contents animate once it is there. Only for a DRAWN scene: a screen recording has no card to hang an arrival on and the edit is refused, so call set_visual first if you want one there. list_motions publishes all eight with what each is for. The effect plays inside the scene's own window, so choosing one never changes the film's length or pushes the voice off the pictures. set_motion(scene_id, motion) — Change a scene's entrance animation. A motion from the wrong family is refused, not swapped. set_inset(scene_id, generate, character?, model?, corner?, shape?, size?, mute?) — A PRESENTER IN THE CORNER: a generated clip of a person drawn OVER this scene — the recording or the card keeps the frame, as in any screen tutorial. Works on a filmed scene and a drawn one. Costs one clip, refunded if it fails; the scene then plays without the presenter. generate: null removes it. set_data(scene_id, data) — Correct a scene's content without touching its visual or animation. One wrong figure costs no new video. Send the WHOLE content: it replaces what you wrote rather than merging into it — get_storyboard's `data` is exactly what to send back with your correction applied. What the composer added (`derived`) is kept either way. set_voice(voice) — Change the narrator for the whole video. set_music(music) — Change the background music for the whole video. set_look(look, caption_style?) — Change the whole film's LOOK — captions, cutting rhythm, sound cues and motion register together. list_video_options publishes the five with a note each. Applied on the next render; it never moves the timeline. |

## validate_format

**Cost:** Free · read-only

Compiles the template against a sample item without touching the database or any feed: the catalogue checks (voice, music, language, theme…), the scene templates filled and checked as an animation, and what the first episode's title, brief and scene count would be. Returns problems by field; nothing is created, rendered or charged.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `name` | string |  | The format's name, for {{show}}. Default `"Preview"`. |
| `kind` | `video` · `animation` |  | video or animation. Default `"video"`. |
| `goal` | `explainer` · `ad` · `demo` · `tutorial` · `article` |  | What the video is for. Shapes the script's structure and pacing. Default `"explainer"`. |
| `aspect_ratio` | `16:9` · `9:16` · `1:1` |  | 16:9 for web and YouTube, 9:16 for Reels/Shorts/TikTok, 1:1 for feeds. Default `"16:9"`. |
| `language` | `en` · `fr` · `es` · `de` · `it` · `pt` · `nl` |  | Language of the voiceover and captions. Write the narration in this language. Default `"en"`. |
| `target_seconds` | integer |  | How long the film should be. Here it is a CHECK, not a setting: you wrote the narration and a narrated scene lasts exactly as long as its words, so nothing can stretch or shrink it. If the script misses this by more than 15%, the call is refused before any credit moves, and the refusal says how many words 45 seconds actually carries and how many to cut or add. Omit it and any length between 15 and 180 s is accepted. Range 15–180. |
| `tone` | string |  | Delivery of the narration, up to 80 characters — e.g. energetic, calm, authoritative, or a short direction like "dry and deadpan, like a friend telling a story". Default `"energetic"`. |
| `voice` | `auto` · `Kore` · `Zephyr` · `Puck` · `Charon` · `Aoede` · `Fenrir` · `Leda` · `Orus` · `Callirrhoe` · `Achird` · `Sulafat` · `Sadachbia` |  | Voice character (every voice is multilingual). auto picks a voice that fits the goal and tone and differs from the site's previous films; name one to fix it. Default `"auto"`. |
| `music` | `auto` · `none` · `uplift` · `corporate` · `chill` · `cinematic` · `ambient` · `pulse` · `playful` · `warm` |  | Background music bed, or "none". auto fits the goal and differs from the site's previous films; name one to fix it. Only the listed ids — these are tracks, not a style prompt. Default `"auto"`. |
| `subtitles` | boolean |  | Burn captions into the picture and emit a .vtt sidecar. Default `true`. |
| `intro` | boolean |  | Include the branded opening title card. Default `true`. |
| `outro` | boolean |  | Include the closing call-to-action card. Default `true`. |
| `brand_name` | string |  | Name shown on the intro and outro cards. |
| `theme` | object |  | The film's visual identity: palette, type and mode. Call list_themes for the presets and the rules, or detect_brand to read a site's own. Omitted, an animation uses the house palette and a filmed video adopts whatever the page's CSS says. |
| `focus_template` | string |  | video formats: the brief every episode's script writer gets, with {{title}} {{summary}} {{link}} {{date}} {{image}} {{show}} {{site}} filled from the item. |
| `title_template` | string |  | animation formats: the episode's title, same placeholders. Default "{{show}} — {{title}}". |
| `scenes` | array |  | animation formats: the scene templates, as create_animation takes scenes, with the placeholders in any string. |
| `programme` | object |  | animation formats: the programme instead of plain scenes. {beats: [...], resolvers: [...], computed: {...}, requires_beats: [...], reject_if: [...]}. A beat is a scene (visual, motion, mood, heading, caption, narration, data) plus beat (one of cold_open, title, identity, context, trend, breakdown, outlier, comparison, caveats, verdict, sources), when (an expression; dropped when not true) and for_each (an expression yielding a list; repeated per element). Any string may carry {{ expressions }} — dotted paths and filters such as money(EUR,M), percent(0), say, sort_by(year), take_last(6), map({label: year, value: total}) — and any field may be {"$bind": "expression"} to receive a real number, list or object (a chart's points). Resolvers fetch data before compiling: {id, call: {mcp: alias, tool, input} | {http: url, query, body}, select, required, on_missing: skip_episode | drop_beats(a,b) | use_default | fail_loud, cache: "30d"}; each reads what the ones before it bound. Every numeral in a narration or caption must come from an expression: a figure typed by hand fails validation by beat. validate_format checks the template; preview_episode runs the resolvers and compiles a real episode for free. |
| `routing` | object |  | How episodes are made: {planner?: flash|pro, footage?: prefer-recorded|record-fresh}. flash is the benched default (it beat every larger model under the real prompt); pro is a deliberate choice. prefer-recorded uses the site's banked flow recordings when they match a scene; record-fresh films every episode anew, for a subject that changes each time. |

## verify_episode

**Cost:** Free · read-only

The proof behind a film. Returns the format version that made it (with the template's SHA-256), every resolver source with what it fetched and when, the integrity report and the beats dropped, the storyboard's claim ledger (which figures trace to the page, the brief, or nothing), the Content Credentials written on the render (manifest URL; whether the file is C2PA-signed and by whom), and a reproducibility check: the stored data is recompiled with the same format version and compared to the rendered narration word for word. Nothing is rendered and nothing is charged.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `episode_id` | string |  | The episode to verify, from run_show or a show's recent_episodes. |
| `video_id` | string |  | Or a video id: the episode is found through it when there is one; a plain video is verified on its claim ledger and credentials. |

