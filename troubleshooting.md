# Troubleshooting

**Scope:** symptom → cause → fix, for
the failures a home installer actually
meets — led by the lab's own twenty
minutes of confusion, which turned out
to contain the two most instructive
guards in the whole application.

Start every feed mystery in the same
place: the reader's log,
`data/users/<name>/log.txt`. FreshRSS
writes fetch failures there with the
real error text, and the entries below
quote it verbatim.

## A feed on your own network will not fetch

**Symptom:** adding or refreshing a
feed whose address is a machine at
home fails; the log shows one of:

```text
cURL error 56: Recv failure: Connection reset by peer
[http://localhost:8099/allotment-journal.xml]
```

or

```text
Fetching this URL is not allowed, because the host's IP
is not in the allowlist [http://127.0.0.1:8099/]
```

…while curl from the same machine
fetches the feed perfectly. (The lab's
whole episode is transcript `t04`.)

**Cause 1 — FreshRSS resolves names
itself.** As an anti-SSRF measure the
fetcher resolves a feed's hostname with
a real DNS query and pins the answer —
it does not read `/etc/hosts`. On a
network whose DNS intercepts or
answers creatively (the lab's bench
answered `localhost` with `198.18.8.20`,
an address where nothing listens), the
pin lands somewhere dead, and the
connection is reset. **Fix:** put the
literal IP address in the feed URL for
local feeds.

**Cause 2 — private addresses are
refused on purpose.** IPs in private or
reserved ranges are rejected unless
allowlisted — the same guard's second
door. **Fix:** allowlist exactly what
you mean to fetch, as `host:port` pairs
or CIDR ranges, in the system setting
`internal_host_allowlist` or the
`INTERNAL_HOST_ALLOWLIST` environment
variable — and set it for *every*
process that fetches: the web server
and the cron job are different
processes with different environments.
The lab's working value was a single
pair:

```bash
INTERNAL_HOST_ALLOWLIST='127.0.0.1:8099'
```

A bare IP with no port does not match;
`*` disables the guard entirely and is
not the answer at home either.

## Nothing is new since Tuesday

The actualizer stopped (chapter 7):
cron edited, timer disabled, container
rescheduled, PHP path changed under it.
Run `app/actualize_script.php` by hand
and read its report — feeds actualize,
or the log names the one that cannot.

## One feed errors; others are fine

That **feed** broke, not FreshRSS: it
moved (fix the URL in the feed's
settings; history stays), it started
requiring a login (per-feed
credentials), or it died (mute it while
you decide; chapter 6). The feed's
card shows its error state and last
successful fetch.

## The login page will not submit

The button stays dead and the form
says JavaScript must be enabled:
FreshRSS's login *is* JavaScript —
chapter 4's nonce-and-hash ceremony
runs in the browser (transcript `t02`
does it by hand). Allow the script, or
sign in from a browser that runs it.

## A client app gets 401

In order of likelihood: the app was
given the **web** password instead of
the **API password**; the API was not
enabled for the install or no API
password is set on the user; the app
wants the `…/api/greader.php` address
and got the bare site address. Prove
the server side with chapter 8's
ClientLogin from curl before debugging
the app — the API answers plainly.

## Counts disagree between app and web

They read the same database, so a
lasting disagreement is a stale
client: force a full sync in the app.
A *brief* disagreement is chapter 7 —
one surface refreshed, the other's
cache has not.

Check: for any feed problem, you can
now say which of the three witnesses
you have consulted — the user's log,
the feed's own error state, and a hand
actualize — and in which order. That
order is the troubleshooting method;
the entries above are just its
greatest hits.
