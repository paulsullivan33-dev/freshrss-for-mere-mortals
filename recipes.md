# Recipes

**Scope:** four standing arrangements
that combine the earlier chapters — the
kitchen server, the two-reader
household, the phone in your pocket,
and the local shelf — each with the
decisions already made.

## The standing home install

*One small machine, SQLite, Apache or
nginx at `p/`, cron every 20 minutes.*

- Install by chapter 3; choose SQLite
  and do not think about databases
  again.
- `actualize_script.php` under cron as
  the web user (chapter 7); check it
  weekly by looking at the newest
  article's age, not by reading logs.
- One OPML export after every big
  subscription tidy; a `data/` copy in
  the house backup rotation
  (chapter 10).

Serves a household for years on
hardware that was retired from sterner
duties.

## The two-reader household

*One server, an account each, OPML as
the family inheritance.*

- Create each reader with
  `create-user.php`, each with their
  own API password from day one.
- Whoever builds the subscription list
  exports OPML; the other imports it
  (chapter 4). From that moment the
  lists are *theirs* — the lab proved
  the point it makes (transcript
  `t10`): same 44 articles, different
  read state, 42 unread against 44.
- Shared interests get a category with
  the same name in both accounts;
  nobody shares an account "to keep it
  simple" — read state is personal, and
  sharing an account is how two people
  mark each other's articles read.

## The phone reader

*FreshRSS on the server, an app on the
phone, the API between them.*

- Confirm `--api-enabled` and set the
  API password (chapters 3–4).
- Verify with curl before touching the
  phone (chapter 8's four calls): if
  curl cannot log in, the app will fail
  more politely and less informatively.
- In the app: server address
  `https://your-server/api/greader.php`
  — or the Fever endpoint, per the
  app — user name, **API** password.
  The classic failure is the web
  password in that field.

Documented, not demonstrated — the lab
had no phone; the protocol it would
speak is the one chapter 8 ran.

## The local shelf

*Feeds from your own network, on
purpose and allowlisted.*

Some of the best feeds are local: a
blog on the NAS, a status page on the
router rack, a generator on a Pi.
FreshRSS will fetch them only after
you open its SSRF guard deliberately
(chapter 14's full story):

- Prefer the literal IP address in the
  feed URL over a name your DNS might
  answer creatively.
- Allowlist exactly the `host:port`
  pairs involved — system setting
  `internal_host_allowlist`, or the
  `INTERNAL_HOST_ALLOWLIST` environment
  variable for the web server *and* the
  cron job — never `*` at home either.

Check: each recipe names its own
moment of truth — the first cron-run
article, the second reader's differing
count, the first phone sync, the first
local article. Watch for that moment;
the recipe is working when it happens
without you in the room.
