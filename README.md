# The Chronicle

A weekly card game played against your own life. Four areas — friendships, dating, reading & learning, housework. You build a deck on Sunday, get dealt a hand, and every card you play asks you one question. At the end of the week a chronicler turns your answers into a chapter.

The dials do everything: how many cards each area puts into the week, and — by whichever you push highest — which area the week leans towards. Level dials mean an even week with no lean and no multiplier.

---

## Deploying

Drop all six files into a repo, turn on GitHub Pages, done.

```
index.html      the app
cards.json      the deck — edit this, not the app
manifest.json   PWA
sw.js           offline shell
icon-192.png
icon-512.png
```

Then open it on your phone and add to home screen.

## Editing the deck

Open `cards.json` in GitHub's web editor — the pencil icon — from any device. Each card:

| field | what it is |
|---|---|
| `d` | `friendships`, `dating`, `reading`, `housework` |
| `s` | suit — free text, shown in small caps on the card |
| `t` | title, four words or fewer |
| `b` | what you are asking yourself to do |
| `q` | **the question you get asked after you play it** |
| `xp` | 5–60 |

`q` is the important one. It is the only thing the chronicler ever sees, so ask for something physical and specific. *What could you not remember?* works. *How did it go?* does not.

Cards written inside the app live in your record, not in this file. Move the good ones here when you want them on every device.

Malformed cards are skipped rather than breaking the deck — a card needs at least a valid `d`, a `t` and a `b`. If any are skipped you get a quiet note on load. `index.html` also carries a complete copy of the deck, so the app never runs short if `cards.json` cannot be read.

## Memory

Same arrangement as Das Wortreich, and the same token works for both.

Tap ☁ → paste a GitHub token with **gist scope only** → Connect and sync. The app searches your gists for one containing `chronicle_record.json`, uses it if it finds one, and creates a private gist if it does not. There is no id to copy across. Paste the same token on your phone and it lands on the same record.

After that: it pulls when you open it, saves four seconds after any change, and saves again when you close the tab. Newest copy wins — so if you play on two devices in the same week, open the second one before touching anything so it pulls first.

The token is stored under its own key, separate from the record. It is not in the gist and not in your exports. Disconnecting removes it and leaves everything on the device.

## The chronicler

**Close the week → Copy the week.** That puts the whole thing on your clipboard: the rules, this week's form, your last three chapters so it does not repeat itself, and every line you wrote with the question that prompted it. Paste it into a Claude conversation. Push back until the chapter is right — the prompt ends by telling it to rewrite rather than defend. Then paste the final version into the box and save.

No API key, no billing, no proxy, nothing to keep running. And you can argue with it, which an automatic version never could.

Set up a Sunday task in the Claude app if you would rather be asked for it than remember.

## Sunday reminders

The banner appears when you open the app on a Sunday. A real notification needs the page still in memory — browsers cannot wake a static site on a schedule. If you want a proper Sunday alarm, use a phone reminder pointing at the URL. This is a limitation of the platform, not something worth engineering around.

## What a keepsake stores

The card title, the question it asked, your answer, the week, and the date. It is a snapshot — rewriting or deleting a card in `cards.json` never changes anything you have already kept.

## Backups and reading

Two exports, for two purposes.

**Export a copy** writes the whole record as JSON — weeks, keepsakes, chapters, your own cards. This is the backup. Do it after any week worth keeping. Import replaces everything on the device, so read the count in the confirmation before agreeing. The state carries a version number and migrates on load, so old exports keep working.

**Export the chapters** writes it as Markdown: every chapter in order, your margin notes as blockquotes, and the keepsakes each one was built from listed underneath with the question that drew them out. This is the version you read, print, or paste into a document. It is not a backup and cannot be imported.

## Maintenance

Once a season, twenty minutes: read the chapters, delete cards you never play, write three new ones.

**Bump `CACHE` in `sw.js` whenever you change `index.html`** or the service worker keeps serving the old one and you will think you have broken something. It is at `chronicle-v6` now.

---

Class of Coffee — with AI assistance
