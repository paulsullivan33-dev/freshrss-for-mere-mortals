# What FreshRSS Is

**Scope:** the mental model — a feed
reader you run yourself, which fetches
what your favourite sites publish and
keeps one reading list that follows you
— plus what it is not, and the lab this
guide's claims rest on.

## The one-paragraph version

**FreshRSS** is open-source software
that reads **feeds** — the machine-
readable lists of new articles most
blogs, news sites, and podcasts already
publish in RSS or Atom format. Instead
of you visiting twenty sites to see
what changed, FreshRSS visits them for
you, collects what is new into a single
list, and remembers what you have read.
You read that list in a web browser, or
in a phone or tablet app that talks to
your server. It began as a one-person
project in 2012 and is now maintained
by a community; it is written in PHP,
runs on modest hardware — a Raspberry
Pi is plenty — and asks for no account
with any company, ever.

That is the whole idea. The rest of this
guide is the fine print: the parts that
fetch and store, the two passwords each
reader ends up with, and why a feed
sitting on your own network can be the
hardest one to fetch.

## The shape of the thing

Three pieces of the experience are
worth naming before any machinery:

- **The feed comes to you.** A feed is a
  small file a site updates whenever it
  publishes: titles, links, summaries,
  dates. FreshRSS polls your feeds on a
  schedule and files new articles under
  the right subscription. Your part of
  the bargain is just reading.
- **One inbox, every source.** News,
  blogs, comics, podcasts, release
  notes for software you run — if it
  publishes a feed, it lands in the
  same list, in time order, next to
  everything else. The list is the
  product; the sources are plumbing.
- **Read state follows you.** Mark an
  article read on the sofa and it is
  read on the phone. That small fact is
  the entire reason a *server* is
  involved: one copy of "what have I
  seen", kept in one place, instead of
  every device keeping its own.

## What it is not

Four confusions worth clearing away
early:

- It is **not a social network**. There
  is no following, no timeline of other
  people's opinions, no algorithm
  promoting anything. The order is the
  order things were published.
- It is **not a read-it-later service by
  itself**. It holds what feeds deliver,
  and old articles age out by rules you
  set. (It has friends that do the
  archiving — the neighbours chapter
  names them.)
- It is **not an e-mail newsletter in
  disguise**. Some services turn feeds
  into a daily e-mail; FreshRSS keeps
  reading *in the reader*, where read
  state, search, and stars live.
- It is **not finished software in the
  old sense**. Releases arrive steadily
  and occasionally rearrange things.
  Chapter 10's upgrade habit — read the
  notes, back up the folder, then move —
  is written in from the start.

## Versions and the lab

This guide was built against **FreshRSS
1.30.4**, the current release on the day
of the build, taken from the project's
official release archive and checked
against its own version constant before
anything ran. The lab installed it with
the project's command-line installer,
made two invented readers, and fed them
one real public feed (the BBC's world
news) and one feed invented on the spot
and served from the same machine. Every
claim in these chapters that sounds like
a demonstration was one: the transcripts
in `freshrss-lab/transcripts/` are the
lab's own output, with passwords and
tokens redacted.

One sandbox confession, stated once: the
lab served FreshRSS with PHP's built-in
web server — fine for two readers on one
machine, not the way chapter 3 tells
*you* to serve it — and the bench
machine's DNS is intercepted, which
turned the local fixture feed into a
small detective story. Both are declared
where they belong, in chapters 3 and 14,
and in `criteria.md`, which keeps the
full ledger of what was run and what was
only read.

Check: you should now be able to say
what a feed is, what the server adds
that a browser bookmark cannot, and why
"it fetches" and "it remembers" are two
different jobs. If that is clear,
chapter 2 opens the box.
