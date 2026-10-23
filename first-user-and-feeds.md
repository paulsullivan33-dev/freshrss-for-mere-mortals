# First User and First Feeds

**Scope:** the first reader's account,
the login ceremony that never sends the
password, and the three roads by which
feeds arrive — typing one address,
importing an OPML file, and inheriting
someone else's — with the lab's import
as the worked example.

## The default user

The install names a **default user**:
the first reader, and the one whose
settings include running the place —
creating other users, system settings.
Chapter 3's `create-user.php` made her.
More readers are made the same way, or
from her settings screens once she is
signed in; chapter 11's recipes assume
a household of them.

Keep two passwords per reader in mind
from the start, because chapter 8 will
spend the second:

- the **web password**, for the login
  form;
- the **API password**, a separate
  secret used only by apps and the API.
  It can be set at creation
  (`--api-password`) or later in the
  reader's profile. It is *not* the web
  password, and a leaked one can be
  changed without touching the other.

## The login that never sends a password

FreshRSS's login form never transmits
the password at all. What the browser's
JavaScript does instead (transcript
`t02` walks the same steps with curl):

1. Ask the server for a one-time
   **nonce** and the reader's **salt**.
2. Hash the password with that salt —
   which reproduces the stored hash —
   then hash *that* with the nonce,
   under a fresh salt.
3. Send the result as the `challenge`.
   The server checks it against its own
   copy; the nonce is consumed, so the
   exchange cannot be replayed.

Two consequences worth knowing. With
JavaScript disabled the form plainly
says so and will not submit — scripting
is part of this login by design. And a
script that wants to log in must do the
same bcrypt dance; there is no
plain-password POST to imitate.

## Adding feeds, three ways

**By hand.** Subscription management →
add: paste a site address or a feed
address; FreshRSS finds the feed,
fetches a title, files it. Best for one
at a time.

**By OPML.** An **OPML** file is the
universal suitcase for subscriptions:
every reader exports one, FreshRSS
imports one, from the web page or the
command line —

```bash
php cli/import-for-user.php \
  --user marta \
  --filename sample-subscriptions.opml
php cli/actualize-user.php --user marta
```

The lab's file (`examples/
sample-subscriptions.opml`) carried two
feeds in two categories, and the import
plus one actualize run delivered the
state this guide keeps quoting
(transcripts `t03`–`t04`):

| Feed | Source | Articles | Unread |
|---|---|---|---|
| BBC News - World | the public web | 39 | 39 |
| The Allotment Journal | this machine | 5 | 5 |

**By inheritance.** When the admin
allows it, a new reader can start from
the default subscriptions file; between
that and OPML, nobody in a household
types thirty addresses twice.

## A feed is checked when it is added

Adding a feed is also its first fetch:
FreshRSS retrieves it to learn its
title and site, so a bad address fails
*at add time*, not at midnight. The
failure in transcript `t04` happened
exactly there — the fixture feed's
address could not be fetched by
FreshRSS even though curl reached it
fine — and chapter 14 tells that story
in full, because the two guards behind
it (self-resolution and the internal-
host allowlist) are things a home
installer genuinely meets the first
time they subscribe to anything on
their own network.

Check: sign in, import the sample OPML,
actualize, and count — the reading page
title shows your unread total in
brackets, and each feed lists its own.
If a feed is missing, its add-time
error is in the reader's log
(`data/users/<name>/log.txt`), which is
where chapter 14 always starts.
