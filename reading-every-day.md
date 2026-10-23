# Reading Every Day

**Scope:** the daily reading surface —
the river of new articles, the views,
marking read (one at a time, in
bunches, and automatically), stars and
search — as the lab exercised it, with
the counts to prove the buttons mean
what they say.

## The river

The main page is one list, newest first,
across all subscriptions: the **main
stream**. The page title carries your
unread count — the lab's said `(44)`
after the first actualize, a small
number that becomes the chapter's
ruler. Down the side: your categories
and feeds, each with its own unread
count, each clickable to narrow the
river to one source.

Three views present the same articles:

- **Normal** — titles with a summary,
  expanding in place. The reading view.
- **Global** — every feed at once as a
  grid of sources with counts; the
  "what needs attention" view.
- **Reader** — full articles one after
  another, for long-form sitting-down
  reading.

Which is home is a per-reader setting;
the state underneath — read, starred —
is one and shared by all three.

## Marking read

Reading is mostly one gesture repeated:
an article opened, clicked, or scrolled
past is marked **read**, and its feed's
count falls. The lab did it the
deliberate way, through the page's own
read toggle on *Sowing Broad Beans
Before the First Frost* (transcript
`t05`): the entry's flag flipped in the
database, the Allotment Journal's
unread count fell 5 → 4, and the page
title's ruler fell `(44)` → `(43)`.

Around that gesture sit the bulk tools:
mark a whole feed read, mark
"everything older than…" read, and the
per-feed setting that marks articles
read as you scroll past them. Keyboard
shortcuts cover the whole loop (next,
previous, open, star, mark) and are
listed in the help overlay — daily
readers end up living on them.

## Stars and search

A **star** (FreshRSS calls them
favourites) is the keep-this flag: it
never expires, survives retention
cleanup, and has its own view. Search
covers titles and article bodies across
everything, with a small query language
worth learning once — `intitle:`,
`author:`, `inurl:`, `#tag`, date
ranges (`date:2026-10-01/2026-10-22`),
and negation. Between stars and search,
"I'm sure I read that here somewhere"
is a solvable problem.

## What the article page keeps

What you see for an article is what the
feed delivered — which for many feeds
is the whole article, and for others a
summary with a link out. FreshRSS can
fetch the full page for feeds that
truncate (a per-feed setting, chapter
6); it is a fetch from the site, not
magic, and chapter 13 is honest about
sites that object.

Check: mark one article read and watch
two numbers agree — the page title's
total and the feed's own count. Then
star one, open the favourites view, and
find a word you remember with search.
Those four gestures are ninety percent
of daily FreshRSS.
