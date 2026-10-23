# Backing Up

**Scope:** what a FreshRSS backup
actually consists of — refreshingly,
almost everything in one folder — the
three layers it separates into, the
OPML safety net, and the upgrade habit
that makes backups feel routine.

## The good news first

FreshRSS keeps its whole life under
`data/`: the system configuration, and
one folder per reader holding their
settings and — with SQLite — their
entire database as a single file,
`db.sqlite`. The lab's whole `data/`
for two readers and 88 articles was
about **1.1 MB**. Backing up FreshRSS
is copying that folder somewhere else,
ideally while nothing is writing, and
it fits on any medium you own.

```text
data/
  config.php            the system settings
  users/
    marta/
      config.php        her settings (and password hashes)
      db.sqlite         her articles, feeds, read state
    kenji/
      config.php
      db.sqlite
```

## Three layers, three jobs

1. **The folder copy** (above) is the
   real backup: settings, articles,
   read state, everything. Restore =
   put the folder back, fix ownership
   for the web user, sign in.
2. **The OPML export** is the safety
   net, not the backup: subscriptions
   only, no read state — but it is tiny,
   human-readable, and restores into
   *any* reader, including a FreshRSS
   you rebuilt from nothing. Take one
   whenever the subscription list
   changes meaningfully:

   ```bash
   php cli/export-opml-for-user.php \
     --user marta > marta-subscriptions.opml
   ```

   The lab's round trip (transcript
   `t09`) is the proof this net holds:
   Marta's export imported into Kenji
   rebuilt his two feeds and all 44
   articles — as unread, which is what
   "no read state" means in practice.
3. **Per-user database exports** — the
   CLI offers `export-sqlite-for-user.php`
   and `db-backup.php` for stores that
   want database-shaped backups, and a
   full ZIP export per user (articles
   included) from the web UI. Worth
   knowing they exist; the folder copy
   remains the household answer.

## A restore rehearsal, honestly scoped

The lab verified the *contents* of its
safety copies (the SQLite files open,
count, and answer questions — that is
how transcripts `t03`–`t10` quote their
numbers), and the OPML net was
exercised for real. A full
folder-restore onto a fresh install was
**not** rehearsed; the procedure above
is the project's documented one, and
the right time to rehearse it is with a
small install, exactly as chapter 10 of
every guide in this series keeps
saying: a backup you have not restored
is a hope with good filing.

## Upgrading

Same folder, new code: fetch the new
release archive, unpack over the old
(keeping `data/` and `extensions/`),
let the first request run the database
migrations, read the release notes
first — the project flags breaking
changes loudly when they exist. A
folder copy taken *before* the upgrade
is both your backup and your way back.

Check: copy `data/` somewhere else
right now, export one OPML, and open
the copied `db.sqlite` with sqlite3
and count the entries. If all three
worked, your backup is a procedure,
not a sentiment.
