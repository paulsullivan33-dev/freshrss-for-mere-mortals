# Keeping Feeds Fresh

**Scope:** the actualizer — who runs
it, how often, what a single run does
to a feed — plus **WebSub**, the push
mechanism that makes polling moot for
feeds that support it.

## Polling is the design

Feeds do not push (with one exception,
below). Freshness means asking, on a
schedule: that is the **actualizer**,
`app/actualize_script.php`, which
refreshes every user in turn, and its
per-user sibling
`cli/actualize-user.php --user <name>`,
which the lab ran for its transcripts.
Nothing inside FreshRSS *starts* them;
something outside must:

- **cron** on a Linux server — the
  standing arrangement, typically every
  15–30 minutes, run as the web user:

```cron
*/20 * * * * php /path/to/FreshRSS/app/actualize_script.php > /dev/null 2>&1
```

- a systemd timer, same shape;
- the Docker image's own scheduling,
  which is this same script on a loop
  (documented with the image);
- your own finger: the web UI's refresh
  button actualizes *your* feeds, now.

A useful experiment, once: stop the
scheduler for a day. FreshRSS works
flawlessly on old news, and chapter
14's first question explains itself.

## What one run does to one feed

For each subscription whose turn has
come: fetch the feed file (politely —
conditional requests let an unchanged
feed answer "nothing new" cheaply),
file articles not already known,
apply filter actions (chapter 6), and
apply retention. Feeds answer at their
own pace, so each carries its own
**TTL**: FreshRSS will not re-fetch a
feed before its interval, however often
the actualizer runs. Busy news feeds
suit 15–30 minutes; most blogs are
honestly served by hours. The lab's
single-feed runs show the bookkeeping
in the open: `actualized 1 feeds …
(5 new articles)` — and, just as
instructively, `actualized 0 feeds`
when a feed was not yet due (transcript
`t04`'s first re-run).

## WebSub: the doorbell

Some feeds — many large platforms among
them — advertise a **WebSub** hub.
FreshRSS subscribes your server to the
hub; when the feed changes, the hub
*pushes* the new article to your
server within seconds, no polling.
Requirements are real: your FreshRSS
must be reachable from the internet at
its configured base URL, because the
hub has to call *it*. On a
LAN-only install WebSub simply never
engages and polling carries everything
— the lab's case, so WebSub here is
**documented, not demonstrated**: the
bench had no public endpoint for a hub
to call, and nothing in these chapters
claims a push was received.

Check: run the actualizer by hand,
read its one-line report, then run it
again immediately and watch a feed be
skipped as not-due. Set one feed's
interval long and one short, and you
have the whole freshness machine in
view.
