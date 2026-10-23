# Writing Criteria

Every guide in this repo is written to the same
standard. If you're adding or editing a guide —
human or AI — hold it to these.

1. **Plain words, real ideas.** Simple language,
   never dumbed-down concepts. Explain jargon on
   first use; collect terms in the glossary.
2. **No hype.** No marketing adjectives, no
   "revolutionary," no promises about what
   something will do for the reader.
3. **Honest about limits.** Say what the thing
   *can't* do. State uncertainty instead of
   smoothing it over. Validation notes include
   what remains unverified.
4. **No invented numbers.** Benchmarks, defaults,
   and specs are either measured or qualified with
   "depends on your setup." If it wasn't tested,
   say so.
5. **Checkable.** Commands are meant to be run,
   with "Check:" blocks showing what success looks
   like. Sources are linked, not asserted.
6. **Respect the reader's setup.** Call out
   Windows/Mac/Linux differences. Don't assume a
   GPU, a budget, or prior experience.
7. **Safety isn't skipped.** Real risks get
   stated plainly, not buried.
8. **Scoped.** Each guide says what it covers and
   points elsewhere for the rest. No guide
   pretends to be the whole subject.
9. **Structure over prose.** Tables, before/after
   examples, symptom → fix. Scannable beats essay.

## Verification notes for this guide

Built and verified 2026-10-22 against
**FreshRSS 1.30.4** (project release published
2026-10-21, the current release on build day;
the release ships no binary assets, so the
official source archive was used, sha256
`4c750c79…`, version confirmed from the
archive's own `constants.php`).

**Primary sources read, not remembered:**
the release's own tree — `cli/` usage output
for every command the chapters name, the
login and fetcher behaviour read in
`app/Controllers/authController.php`,
`app/Models/FormAuth.php`, and
`app/Utils/httpUtil.php` (the allowlist
semantics in chapter 14 are quoted from
that code), and the shipped
`config.default.php`.

**Ran for real** (transcripts in
`freshrss-lab/transcripts/`): FreshRSS
1.30.4 on PHP 8.3.6 with SQLite, served by
PHP's built-in server (a declared lab
deviation — chapter 3), and:

- t00 — versions and archive hash, as above.
- t01 — `cli/do-install.php` (SQLite,
  form auth, API enabled), then
  `cli/create-user.php` for two invented
  readers with separate web and API
  passwords and `--no-default-feeds`.
- t02 — web login over HTTP with cookies,
  performed the way the browser does it:
  login page (CSRF), the
  `?c=javascript&a=nonce` exchange, the
  bcrypt challenge computed and POSTed;
  the signed-in page names the user and
  offers logout. The password itself was
  never sent.
- t03 — OPML import for Marta and one
  actualize: the real public feed (BBC
  News - World) delivered **39 articles**.
- t04 — the invented fixture feed's two
  failures and fix (self-resolution meets
  intercepted DNS; then the internal-host
  allowlist, opened with
  `INTERNAL_HOST_ALLOWLIST='127.0.0.1:8099'`):
  **5 articles**, counts verified in her
  own `db.sqlite` (BBC 39/39 unread,
  Allotment 5/5).
- t05 — reading on the web: all five
  fixture titles present in the stream
  page; the page's own read toggle
  marked one read — page title (44) →
  (43), database flag and per-feed count
  agree.
- t06 — Google Reader API `ClientLogin`
  with the API password → `Auth` token;
  the `reader/api/0/token` edit token.
- t07 — API unread-count (max 43; feed
  and category counts match the web) and
  the unread stream (43 items with ids,
  titles, origins, categories).
- t08 — `edit-tag` marked one item read
  → reply `OK`, unread 43 → 42.
- t09 — OPML round trip: Marta's export
  imported for Kenji; his actualize
  delivered the same 44 articles
  (39 + 5).
- t10 — independence, in both users'
  database files: the two articles Marta
  read are `is_read=1` for her and
  `is_read=0` for Kenji; totals 44
  entries each, 42 vs 44 unread.

**Environment note, stated once:** the
bench machine was rebuilt mid-lab; an
earlier, discarded run used MariaDB
(the first bench had PHP + MariaDB but
no `pdo_sqlite`). Every transcript here
is from the final SQLite run, and no
claim rests on the discarded one.

**Documented only, and labelled as such
in the chapters:** the Docker image
route (no container runtime on the
bench); Apache/nginx serving (the lab
used PHP's built-in server); WebSub
(no publicly reachable endpoint for a
hub to call); the Fever API (present,
unexercised); third-party client apps
(none installed — the API they speak
is the one t06–t08 exercised);
extensions and themes (none installed
or changed); sharing/public pages
(described, not enabled); full
folder-restore (backup contents were
inspected and the OPML path exercised;
no restore onto a fresh install was
rehearsed).

**Fixtures:** the readers (Marta
Ellison, marta@example.com; Kenji Mori,
kenji@example.com), the fixture feed
*The Allotment Journal* and its five
articles (invented, written for this
guide, served from the bench), and the
sample OPML are all invented and live in
`examples/`. The one real feed is the
BBC's public world-news RSS, named
wherever it is used. Passwords and
tokens are redacted in every transcript.
