# Story Reader for Telegram

A one-page reader for stories told in chapters. Readers can change text size, font and background; each chapter plays its own background music; readers can comment on a passage; bookmarks follow them across devices. Each story is completely separate: its own link, its own chapters and music, its own comments group. Readers of one story never see another.

## What's in the folder

```
index.html                          the reader (shared by all stories; never needs editing)
stories/
  lantern-road/                     one folder per story — the folder name is the story's address
    chapters.json                   title, author, links, and the list of chapters
    chapters/ch1.md                 chapter text, one Markdown file per chapter
    chapters/ch2.md
    music/ch1.mp3                   chapter music
    music/ch2.mp3
  second-story/                     another story, same layout
    chapters.json
    chapters/ch1.md
    music/ch1.mp3
```

Each story is opened with its folder name: `https://YOUR-USERNAME.github.io/my-story/?story=lantern-road`. The two sample stories and music loops are placeholders; rename or replace them.

Folder names: lowercase letters, numbers and hyphens only (`winter-tale`, `book2`). No spaces or Persian characters — those go in the title inside `chapters.json`, which can be anything.

## 1. Put it online (GitHub Pages, free)

1. Create a GitHub account and a new repository, for example `my-story`.
2. Upload everything in this folder, keeping the `stories/` folder structure.
3. In the repository go to **Settings → Pages**, choose **Deploy from a branch**, branch `main`, folder `/ (root)`, and save.
4. After a minute the reader is live. Test a story in a phone browser: `https://YOUR-USERNAME.github.io/my-story/?story=lantern-road`

Any other static host works too (Netlify, Vercel, Cloudflare Pages). It must be HTTPS.

## 2. One Telegram Mini App per story

You need one bot (once) and then one Mini App for each story. All apps live under the same bot but each has its own link, title and cover image, so readers only ever see the story they were sent.

Once: open **@BotFather**, send `/newbot`, give it a name and a username ending in `bot`.

For every story: send `/newapp`, pick the bot, then answer: a title (the story's name), a short description, a 640×360 cover image, `/empty` to skip the GIF, the story's address (for example `https://YOUR-USERNAME.github.io/my-story/?story=lantern-road`), and a short name for the link (for example `lantern`). BotFather replies with the story's link:

```
https://t.me/YOUR_BOT/lantern
```

Post that link in the channel. `https://t.me/YOUR_BOT/lantern?startapp=ch2` opens straight to chapter 2.

## 3. Fill in chapters.json

Each story's `chapters.json` starts with:

```json
"title": "The Lantern Road",
"author": "Your name",
"description": "One or two lines shown above the chapter list.",
"appLink": "https://t.me/YOUR_BOT/lantern",
"commentsGroup": "lanternroad_chat",
```

- `appLink` — the Mini App link from step 2. Comments end with a link back to the chapter.
- `commentsGroup` — public username (without `@`) of the group where comments should go, usually the channel's discussion group. To give a group a username: open the group → Edit → Group Type → Public → choose a username. Each story can point at a different group. Leave it empty and the comment button becomes "Share to Telegram" (the reader picks the chat).

## 4. Reader comments

In a chapter, readers can select a passage (a "Comment" button pops up) or tap "Comment on this chapter", write a comment, and send. That opens the comments group with the message already typed; the reader taps send and it appears under their own name. No server involved. Readers who haven't joined the group are asked to join first.

The message looks like:

```
The Lantern Road — Chapter 2: The Road

“…the selected passage…”

The reader's comment

https://t.me/YOUR_BOT/lantern?startapp=ch2
```

## 5. Bookmarks that follow the reader

Position, last chapter and finished chapters are saved per story on the device and, inside Telegram, also to the reader's Telegram account (CloudStorage). Phone and desktop stay in sync. Nothing to configure.

## 6. Adding a chapter

1. Write the chapter and save it as `stories/<story>/chapters/ch3.md`.
2. Put its music in `stories/<story>/music/ch3.mp3` (or reuse an existing file in that story's folder).
3. Add one entry to that story's `chapters.json`:

```json
{
  "id": "ch3",
  "title": "Chapter title",
  "subtitle": "optional one-line teaser",
  "text": "chapters/ch3.md",
  "music": "music/ch3.mp3",
  "musicTitle": "optional track name shown in the player"
}
```

4. Upload. The page updates within a minute.
5. Post `https://t.me/YOUR_BOT/lantern?startapp=ch3` in the channel.

Rules: `id` must be unique within the story and use only letters, numbers, `_` or `-` (no double underscore). Chapters appear in the order listed. Leave `music` out if a chapter has none. You can upload chapter files early and only add them to `chapters.json` on release day.

## 7. Adding a new story

1. Create `stories/<new-name>/` with its own `chapters.json`, `chapters/` and `music/` (copy `second-story` as a starting point).
2. Create a Mini App for it in BotFather (`/newapp`, address `...?story=<new-name>`, its own short name and cover).
3. Put the new link into that story's `appLink`, and its comments group into `commentsGroup`.
4. Post the link wherever that story's readers are.

Nothing in one story refers to another. Deleting a story is deleting its folder.

## Writing chapters

Chapters are Markdown. Persian and other right-to-left text works automatically. Supported formatting:

```
Blank line between paragraphs.

*italic*   **bold**

## A heading inside the chapter

> A quote, indented with a line on the side.

* * *          ← a scene break (three stars or dashes on their own line)
```

## Music tips

- MP3, 64–128 kbps, mono is fine. A 2–3 minute loop is about 1–3 MB.
- The track loops on its own. If the end matches the start, the loop is seamless.
- Music can't start by itself on phones. It starts when the reader taps a chapter or the play button, and their choice (on/off, volume) is remembered.

## Optional: one Mini App for all stories

If you'd rather have a single link, set the Mini App address to the page without `?story=` and post links of the form `https://t.me/YOUR_BOT/read?startapp=lantern-road__ch2` (story folder, two underscores, chapter). Per-story links are recommended though: they let each story have its own title, cover and comments group.
