# FreshRSS for Mere Mortals

Somewhere in your bookmarks there is a
list of sites you used to visit every
morning, and the list is quietly dying —
not because the sites vanished, but
because checking twenty places by hand
is a chore nobody keeps up. **FreshRSS**
is the open-source answer: a feed reader
you run yourself. It fetches the **RSS**
and Atom feeds your favourite sites
already publish, keeps one reading list
on a server in your house, and shows you
only what is new — in a browser, or in a
phone app that talks to it. This guide
explains how it works, installs it the
plain way, and proves each claim against
a real running copy.

The lab behind this guide ran the real
thing: **FreshRSS 1.30.4**, the project's
current release on build day, installed
from the official release archive onto
PHP 8.3 with a SQLite database, and
served by PHP's own built-in web server —
a lab convenience chapter 3 is honest
about. Two invented readers were created
(Marta and Kenji; no real person's
reading habits were involved anywhere),
subscribed to one real public feed — the
BBC's world news feed, which delivered
**39 articles** — and one feed invented
for the lab, *The Allotment Journal*,
served from the same machine, which
delivered its **5 articles** once the
lab had worked out why FreshRSS would
not fetch it at first (that story is
chapter 14's centrepiece, because it
teaches FreshRSS's anti-SSRF guard
better than any diagram). Articles were
marked read on the web page and through
the **Google Reader API**, an OPML file
made the round trip from one reader to
the other, and the second reader's
unread counts stayed stubbornly his own.
`criteria.md` keeps the ledger of what
was run and what was only read.

## What this guide covers

- [**What FreshRSS is**](what-freshrss-is.md) —
  the mental model: feeds come to you,
  one inbox for everything, read state
  that follows you; what it is not (a
  social network, an archive of the web)
- [**The moving parts**](the-moving-parts.md) —
  the web app, the database, the
  actualizer, and the feeds themselves:
  what each holds, and what stops when
  each stops
- [**Installing**](installing.md) —
  the official archive, PHP and SQLite,
  the scripted install, serving it, and
  the Docker route, labelled as read-not-run
- [**First user and first feeds**](first-user-and-feeds.md) —
  making readers from the command line,
  the login that never sends a password,
  and subscriptions by OPML import
- [**Reading every day**](reading-every-day.md) —
  the river of news, views, marking read,
  stars, and finding an article again
- [**Organising feeds**](organising-feeds.md) —
  categories, tags, filters that file or
  mark things for you, and per-feed settings
- [**Keeping feeds fresh**](keeping-feeds-fresh.md) —
  the actualizer, cron, refresh intervals,
  and WebSub, the push doorbell
- [**The API and clients**](the-api-and-clients.md) —
  the Google Reader API proven with curl:
  login, the unread stream, marking read;
  the Fever API and client apps, labelled
- [**Sharing and extensions**](sharing-and-extensions.md) —
  sharing links, per-user public views,
  extensions and themes — what they are,
  and the line between run and read
- [**Backing up**](backing-up.md) — one
  folder, honestly: the database file,
  the settings, the OPML safety net, and
  upgrading without drama
- [**Recipes**](recipes.md) — the standing
  home install, the two-reader household,
  the phone reader, the local-feed shelf
- [**The neighbours**](the-neighbours.md) —
  Feedly, Inoreader, Miniflux, Tiny Tiny
  RSS, NewsBlur: what each one trades
- [**Limits**](limits.md) — one small
  server, feeds that rot, and the parts
  of the web that no longer publish feeds
- [**Troubleshooting**](troubleshooting.md) —
  the feed that will not fetch, the feed
  that stopped, the login that loops,
  the API that says 401
- [**Glossary**](glossary.md) — the terms,
  collected in one place

## What it doesn't cover

Running FreshRSS for a crowd — it is a
household tool here, though it happily
serves a street's worth of readers — and
exposing any server to the internet
safely, which is a subject of its own
(a reverse proxy and TLS get a warning,
not a tutorial). Writing your own
extensions, scraping sites that publish
no feed (chapter 7 names the door,
chapter 13 is honest about it), and
feed *publishing* — this guide reads
feeds; your blog software makes them.

## How to use this guide

Read chapter 1 for the model and chapter
2 before installing anything — knowing
which part fetches and which part stores
turns later confusion into a named
problem. Chapter 3 gets a server running;
chapter 4 with a browser open is the
natural next sitting. If you already
read feeds somewhere else, chapter 4's
OPML import is your whole migration —
export there, import here, done. The
lab's transcripts live in
`freshrss-lab/transcripts/`; its notes
are `examples/lab-notes.txt`.

---

## Part of the series

This guide is one of the [For Mere Mortals](https://paulsullivan33-dev.github.io/mere-mortals/) guides: plain-language guides to the tools programmers and makers use.

Related guides:

- [SearXNG for Mere Mortals](https://paulsullivan33-dev.github.io/searxng-for-mere-mortals/)
- [Docker Compose for Mere Mortals](https://paulsullivan33-dev.github.io/docker-compose-for-mere-mortals/)
- [Caddy for Mere Mortals](https://paulsullivan33-dev.github.io/caddy-for-mere-mortals/)

## License

The writing in this guide is licensed under [CC BY 4.0](https://github.com/paulsullivan33-dev/freshrss-for-mere-mortals/blob/main/LICENSE). Code examples and lab scripts are licensed under the [MIT License](https://github.com/paulsullivan33-dev/freshrss-for-mere-mortals/blob/main/LICENSE-CODE).
