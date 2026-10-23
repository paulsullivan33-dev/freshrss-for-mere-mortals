# Glossary

The terms this guide uses, collected in
one place. Each is explained in the
chapter that leans on it; these are the
short versions.

**Actualizer** — the script
(`app/actualize_script.php`) that polls
every feed for every user and files new
articles. Run by cron or its per-user
sibling; the part whose silence looks
like "no news".

**API password** — a per-user secret,
separate from the web password, used
only by client apps and the API. Set at
creation (`--api-password`) or in the
profile.

**Atom** — the other feed format:
RSS's standardised sibling. FreshRSS
reads both without being asked.

**Category** — the folder a
subscription lives in (News,
Gardening…). One per feed; OPML imports
arrive categorised.

**Challenge** — the value FreshRSS's
login actually sends: the password's
stored hash, hashed again with a
one-time nonce. The password itself
never crosses the network.

**ClientLogin** — the Google Reader
API's login call: user name + API
password in, an `Auth` token out.

**Default user** — the first reader,
named at install; the account that also
administers the install.

**Feed** — the machine-readable file a
site updates when it publishes: titles,
links, summaries, dates. RSS or Atom.

**Fever API** — an older reader API
FreshRSS also emulates, for clients
that speak it.

**Filter action** — a standing rule:
articles matching a search, as they
arrive, get marked read, starred, or
labelled automatically.

**Google Reader API** — the dialect
most sync reader apps share, kept in
common use after Google's 2013 shutdown
of the original service. FreshRSS
speaks it at `api/greader.php`.

**Internal host allowlist** — the
fetcher's permission slip for private
or reserved addresses: `host:port`
pairs or CIDR ranges, without which
FreshRSS refuses to fetch them
(SSRF protection).

**Mute** — silencing one feed without
unsubscribing: it is not fetched and
does not count until unmuted.

**Nonce** — a one-time random value
issued for a single login attempt and
consumed by it, so a captured login
exchange cannot be replayed.

**OPML** — the XML suitcase format for
subscription lists: every reader
exports and imports it, categories
included.

**Retention** — the per-feed (or
global) rule for letting old, unstarred
articles go: keep at most N, or at most
so many days.

**River** — the main stream: every
unread article from every subscription,
newest first. This guide's informal
name for the front page.

**SQLite** — the file-based database:
here, one `db.sqlite` per reader under
`data/users/`. The household default.

**SSRF** — server-side request forgery:
tricking a server into fetching
addresses it should not. FreshRSS's
resolve-and-allowlist fetcher exists to
refuse exactly that.

**Star / favourite** — the keep-this
flag on an article: never expires,
survives retention, has its own view.

**TTL** — a feed's refresh interval:
the actualizer will not re-fetch before
it, however often it runs.

**WebSub** — the push protocol by
which a hub notifies your server the
moment a feed changes; needs a publicly
reachable FreshRSS.
