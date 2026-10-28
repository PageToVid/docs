---
title: Tips & tricks
nav_order: 4.5
description: "Short, practical tips for better PageToVid films: length, shape, free previews, briefs, logins, fixes and prompts that work in Claude and ChatGPT."
---

# Tips & tricks
{: .no_toc }

The shortest path to a good film. Each tip links to the guide that explains it in full.
{: .fs-5 .fw-300 }

1. TOC
{:toc}

---

## Before you film

- **Pick the shape you will post.** 9:16 films the site's own *mobile* layout (Reels, Shorts, TikTok);
  16:9, 1:1 and 4:5 film the desktop layout. Run `inspect_page` with the same `aspect_ratio` first.
- **Write one sentence of brief.** Who it is for and what they should do next. *"For dentists who lose
  patients to no-shows; end on the free trial"* beats a paragraph of adjectives.
- **Choose the goal.** `explainer`, `ad`, `demo`, `tutorial` or `article` — it sets the pace, the shots
  and the ending.
- **Check the page is public.** A robot check or a sign-in page cannot be filmed past;
  [`inspect_page`](mcp/tools#inspect_page) says so before you spend anything.

## Length and pace

- **The words are the length.** A scene lasts as long as its narration — about 149 words a minute at
  the default tone. For a 30-second ad, write about 70 words. [Why](guides/best-practices#1-the-narration-is-the-length).
- **One idea per scene.** Four or five short scenes keep a film moving; one long scene feels slow.
- **Silence is allowed.** A scene with no words holds for the time you give it — good for a logo or a
  final call to action.

## Spend nothing until it is right

- **Draft first.** `create_video` with `draft: true` is free: a low-resolution preview with no AI visuals.
- **Edit the storyboard, not the prompt.** `update_storyboard` is free and every edit can be undone with
  `restore_revision`. Then `rerender_video` once, without `draft`.
- **Price before you spend.** `dry_run: true` or `quote_cost` returns the price; `max_credits` refuses
  anything above your figure. See [Credits & pricing](pricing).

## Look and sound

- **Five looks** — `clean`, `bold`, `editorial`, `playful`, `tech` — set the captions, cuts and music
  together. `bold` for a feed that scrolls, `editorial` for a calm long read.
- **Voices are multilingual.** Pick a voice for its character; the language is set separately
  (13 languages).
- **Generate only what the page cannot show.** A real screencast is more convincing than a generated
  clip; add [AI clips](guides/ai-clips) for the beats the site has no picture for.

## Pages behind a login

- **From Chrome:** sign in to your app, open the [extension](extensions#chrome)'s side panel and send
  the session. It is scoped to one site and expires within 24 hours.
- **Without an extension:** tick *This site needs a login* when you create a film and give a **test
  account's** sign-in page; the password is never stored. SSO and two-factor logins need the extension.
- Filming behind a login is on the Scale plan and up.

## From your AI assistant

Add `https://pagetovid.com/mcp` as a connector in Claude or ChatGPT, then just ask:

> Make a 30-second vertical ad of example.com in French, with a bold look. Draft it first.

> Here is our launch post. Turn it into a 45-second animated explainer, no website.

> Look at the last film you made: shorten scene 3 and end on "Start free".

In Claude Code, the [plugin](https://github.com/PageToVid/claude-plugins) adds `/pagetovid:video`,
`/pagetovid:animate` and `/pagetovid:edit`.

## When something is off

- **Read the warnings.** A film can finish with a lost visual or a short scene and still say `done`:
  check `get_video`'s `warnings` before you share it.
- **Fix, don't remake.** Change the words or the shot of one scene and re-render; the plan and the
  visuals you kept are reused. [How](guides/best-practices#11-fix-dont-remake).
- **A failed render is refunded** automatically, including any AI visual that never reached the film.
- Still stuck? [Open an issue](https://github.com/PageToVid/docs/issues/new/choose) with the video id.
