# Organising Feeds

**Scope:** the order you impose on the
river — categories, tags, per-feed
settings, filters that act on articles
as they arrive, and the mute and
retention switches that keep a big
list kind.

## Categories

A subscription lives in one
**category** (News, Gardening, Comics…)
shown in the sidebar; OPML imports
arrive already categorised, as the
lab's did — the API even reports unread
counts per category label (transcript
`t07`: Gardening 4, News 39). Categories
are folders, nothing more mystical: a
feed has one home, and the sidebar is
the map of them.

## Tags

**Tags** are labels *you* apply to
articles, many per article, from the
article's own menu or in bunches from
search results. Where categories file
the *source*, tags file the *piece*:
"to try", "receipts", "for the club
newsletter". Saved searches and tags
together are how a big reading list
stays browsable by future-you.

## Per-feed settings

Each feed carries its own card of
settings, and three earn their keep:

- **Refresh interval** — how often the
  actualizer may fetch it (chapter 7
  explains who obeys whom).
- **Retention** — how many articles to
  keep, or how long, before the oldest
  unstarred ones are let go.
- **Mute** — silence a feed without
  unsubscribing: seasonal blogs, a
  podcast between series, a news feed
  during a holiday. Muted feeds are
  not fetched and do not count.

Add to those the fetch-full-content
switch (chapter 5), and per-feed
credentials for the rare feed behind a
login, and most "this one feed behaves
oddly" wishes are already granted.

## Filters: rules that read for you

**Filter actions** are standing rules
evaluated as articles arrive: if an
article from *this* feed (or anywhere)
matches a search — a word in the title,
an author, a phrase — then mark it
read, star it, label it, or some of
each. Honest uses: mark the daily
horoscope read on arrival; star
anything from the council feed that
mentions your street; label all posts
by one prolific author for Sunday.
Filters are how a reader scales past
the point where "read everything"
stops being the plan.

A caution the UI also gives: a filter
that marks things read is a small
power tool. Start with labels, promote
to marking once the label has been
right for a month.

## When a feed changes its address

Sites move feeds. FreshRSS follows
redirects and quietly adopts a
permanent new address; a feed that has
moved *without* a redirect shows up in
the feed's health as errors (chapter
14), and the fix is editing the feed's
URL — articles, read state, and
history stay attached to the
subscription, not the address.

Check: build one category, tag three
articles, and write one labelling
filter. Then open the global view: the
sidebar counts, the tag, and the first
filtered arrivals are the shape of a
list you can live with at two hundred
feeds, not just twenty.
