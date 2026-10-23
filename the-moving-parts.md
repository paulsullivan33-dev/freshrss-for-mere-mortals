# The Moving Parts

**Scope:** the four parts of a working
FreshRSS — the web app, the database,
the actualizer, and the feeds
themselves — what each one holds, and
what you notice when each one stops.

FreshRSS is a single PHP application,
but it helps to think of it as four
parts doing four jobs. When something
misbehaves later, the fault almost
always belongs to exactly one of them,
and naming it is half the fix.

## The web app

One PHP program, served over HTTP. It
draws every page you read in, answers
every click, and also answers the
**API** calls from phone apps (chapter
8). It is stateless in the way web apps
usually are: it wakes for a request,
consults the database, answers, and
forgets. Stop the web server and
nothing is lost — your articles sit in
the database — but nothing can be read
or fetched until it runs again.

A detail that surprises people: the app
does not fetch feeds while you browse,
except when you press the refresh
button. Fetching belongs to the third
part.

## The database

Everything FreshRSS knows lives here:
users, subscriptions, categories, the
articles themselves, and — the part
that matters most — each reader's read
and starred state, kept per user. One
FreshRSS can serve many readers, and
each reader's data is separate: with
SQLite (this guide's default) each user
literally gets their own database file
under `data/users/<name>/db.sqlite`;
with MySQL or PostgreSQL the same
separation is by tables and rows.

Stop or lose the database and you lose
the record — the articles can be
re-fetched, but what you had read
cannot be reconstructed. This is why
chapter 10's backup is a database
story first and a settings story second.

## The actualizer

The background worker — not a daemon,
just a script (`app/actualize_script.php`)
that something must run on a schedule:
cron on a server, a systemd timer, or
the Docker image's built-in loop. Each
run walks every user's subscriptions,
asks each feed "anything new?", files
new articles, and applies each feed's
retention rules. The web app's refresh
button runs the same machinery for one
user, on demand.

Stop the actualizer and FreshRSS keeps
working perfectly — on yesterday's
news. A reader whose feeds "stopped
updating" with no error anywhere has
almost always lost this part; chapter
14 starts there.

## The feeds

The fourth part is not yours at all:
the files out on the web that your
subscriptions point at. Sites publish
them, rename them, move them, and
occasionally stop, and each of those
events arrives in your reader as a
symptom. FreshRSS keeps a per-feed
error state and mute switch for this
reason (chapter 6). A feed is also just
an address — which is why the whole
collection of subscriptions fits in one
small **OPML** file you can carry
elsewhere (chapters 4 and 10).

## How a new article travels

```text
a site publishes
      |
      v
the feed file changes  (out on the web)
      |
      v
the actualizer polls it  (cron, or your refresh click)
      |
      v
the database files it under your subscription,
unread, with the feed's category
      |
      v
the web app / API shows it; you read it;
the database flips one flag: read
```

Notice what is *not* in that picture:
no account with the site, no permission
asked, no trace left beyond an ordinary
web request for a small file. Feed
reading is one of the web's oldest and
quietest arrangements, and FreshRSS is
mostly a well-kept desk for it.

Check: for each of these, name the part
at fault — the page will not load; the
page loads but nothing is new since
Tuesday; one blog of thirty has gone
silent; you read everything twice after
moving house. (Web app; actualizer;
that feed; read state — the database.)
