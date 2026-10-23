# Installing

**Scope:** getting FreshRSS onto a
machine the plain way — the official
archive, a PHP runtime, a SQLite
database — with the scripted install
this guide's lab actually ran, and the
Docker route described and labelled,
because the lab's bench had no
container runtime.

You need three things: **PHP 8.1 or
newer** with a handful of extensions,
a place for one folder of data, and a
web server willing to serve PHP. For a
household, **SQLite** is the right
database: no database server to run,
one file per reader, backups by copying
(chapter 10). FreshRSS also speaks
MySQL/MariaDB and PostgreSQL; they earn
their keep on big multi-user installs,
not kitchen ones.

## The shape of the install

```text
1. Fetch the release archive and unpack it
2. Point a web server at its p/ folder
3. Run the installer (web wizard, or the CLI)
4. Create the first reader
5. Schedule the actualizer (chapter 7)
```

The piece people trip over is step 2:
the web server's document root is the
**`p/` subfolder**, not the unpack
folder. Everything outside `p/` — above
all `data/`, which will hold the
database and settings — stays off the
web. Serve the wrong folder and you
have published your own database.

## The scripted install (what the lab ran)

The project ships the whole install as
one command-line script, which is what
the lab used, followed by the user
script. Transcripts `t00`–`t01` in
`freshrss-lab/transcripts/` are the run
itself:

```bash
# Unpack (the archive is the project's
# own, from its GitHub releases page)
tar -xzf FreshRSS-1.30.4.tar.gz

php cli/do-install.php \
  --default-user=marta \
  --environment=production \
  --base-url=http://localhost:8080/ \
  --language=en --title=FreshRSS \
  --auth-type=form --api-enabled \
  --db-type=sqlite

php cli/create-user.php \
  --user marta --password <hers> \
  --api-password <a different one> \
  --email marta@example.com \
  --language en --no-default-feeds
```

Four flags deserve a word:

- `--db-type=sqlite` chooses the
  file-per-reader database. For MySQL
  you would add `--db-host`, `--db-user`,
  `--db-password`, `--db-base`.
- `--auth-type=form` selects FreshRSS's
  own login form (the alternative is
  delegating to the web server's HTTP
  authentication).
- `--api-enabled` turns on the API at
  install time; chapter 8 spends it.
- `--no-default-feeds` tells
  `create-user.php` *not* to seed the
  new reader with the project's starter
  subscriptions. The lab wanted exactly
  the feeds it imported and no others;
  on your first real account, leaving
  the flag off is a friendlier start.

The web wizard (visit the site, click
through the same questions) produces
the same result; the CLI is shown
because its transcript *is* the proof,
and because re-running it is how you
reconfigure a headless box
(`cli/reconfigure.php` exists too).

## Serving it

On a real machine, put Apache or nginx
in front, document root at `p/`, PHP
wired in, and HTTPS through your usual
route. The project documents both
servers; the shape is a standard PHP
site.

**The lab's declared deviation:** the
bench served FreshRSS with PHP's
built-in server —

```bash
php -S localhost:8080 -t p
```

— which is a development tool: one
request at a time, no hardening, no
HTTPS. It was honestly sufficient for
two invented readers on one machine,
and every behaviour this guide claims
was observed through it; do not copy
that one line into a standing install.

## The Docker route (documented, not run)

The project's official image packages
the same application with its own web
server and a built-in actualizer loop;
the documented shape is one container
and one mounted volume for `data/` (and
one for `extensions/`). The bench had
no container runtime, so no chapter in
this guide claims a Docker result —
the commands above are the route the
lab can vouch for, and the image is the
project's own packaging of exactly
this software.

## Checking the install

```bash
php cli/health.php            # the project's own once-over
php cli/list-users.php
curl -s http://localhost:8080/ | head
```

Check: the site answers, the login page
shows, and your user is listed. If PHP
complains about a missing extension,
the names it wants are the usual set —
curl, dom, intl, mbstring, SimpleXML,
zip, and a PDO driver (`pdo_sqlite`
here). Chapter 14 has the failure
table; chapter 4 makes the feeds.
