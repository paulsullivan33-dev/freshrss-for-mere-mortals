# Limits

**Scope:** what FreshRSS will not do,
will not survive, or was never for —
stated plainly, so the tool you adopt
is the one that actually exists.

## One machine, one point of failure

A household FreshRSS is one folder on
one machine. If that machine dies, the
reading stops until the folder is
restored elsewhere (chapter 10 makes
that a small job, not a non-event).
There is no cluster mode, no replica,
no failover — multi-server scaling is
outside what this software is for. The
honest mitigation is the boring one:
backups, and hardware you can replace
without grief.

## It reads what feeds deliver

- A site that publishes a **summary**
  gives you a summary. Full-text
  fetching (chapter 5) helps where the
  site permits it; some sites truncate
  on purpose, and that is their call.
- A site that publishes **no feed**
  gives you nothing to subscribe to.
  Generators (chapter 12) bridge some
  of these; the modern platform web is
  steadily less feed-shaped, and no
  reader fixes that from its end.
- A feed is a **window, not an
  archive**: most feeds carry their
  newest few dozen items. Arrive after
  a long absence and the middle of the
  story may simply not be in the file
  any more. Retention settings keep
  what *you* fetched; they cannot fetch
  the past.

## Polling has a floor

Freshness is bounded by fetch
intervals and feed TTLs (chapter 7):
outside WebSub, "just published" means
"seen within the hour" on a typical
setup, and a feed's owner can ask for
slower. FreshRSS is a morning-paper
tool, not a wire service — by design,
and usually by preference: the asking
is throttled to stay a polite guest on
other people's servers.

## Small print that matters

- **Search** is over what you hold:
  titles and fetched bodies, not the
  web, and not articles let go by
  retention.
- **Security is a boundary, not a
  moat**: the login is properly built
  (chapter 4) and the fetcher is
  SSRF-guarded (chapter 14), but a
  FreshRSS exposed to the internet is
  a public login page; HTTPS and
  current versions are on you.
- **Extensions run as the app**
  (chapter 9): their power is the
  point and the risk, in one package.
- **PHP is the rent**: the stack is
  unfashionable and entirely adequate;
  upgrades of PHP itself are a real
  (if rare) chore the Docker route
  hides and the native route shows.

Check: none of these are surprises if
you have read this far — that is the
test of a limits chapter. The tool is
a well-kept desk for a quiet protocol;
adopt it for that, and it will not
disappoint you by being it.
