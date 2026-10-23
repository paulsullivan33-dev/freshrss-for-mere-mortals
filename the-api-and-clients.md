# The API and Clients

**Scope:** the **Google Reader API** —
the interface phone and desktop reader
apps speak — proven end to end with
curl: login, unread counts, the unread
stream, marking read. The **Fever API**
and the client apps themselves are
documented and labelled; the protocol
they use is the one demonstrated here.

## Why an API at all

The web page is one reader of your
FreshRSS. The API lets *other* programs
be readers too: a phone app with
offline caching and push-style sync, a
desktop app, an e-ink reader. They all
need the same four abilities — prove
who you are, list what is unread, fetch
articles, mark them read — and the
Google Reader API (kept alive as a
common dialect by its many clients
after Google retired the original
service in 2013) is the dialect most
of them share.

Two switches stand between you and it,
both met already: the API enabled at
install (chapter 3, `--api-enabled`),
and a per-user **API password**
(chapter 4) — *not* the web password.

## The four calls, proven

All of this ran against the lab server
with curl (transcripts `t06`–`t08`).

**1. ClientLogin.** Exchange the user
name and API password for a token:

```bash
curl -X POST \
  http://localhost:8080/api/greader.php/accounts/ClientLogin \
  --data-urlencode "Email=marta" \
  --data-urlencode "Passwd=<api password>"
```

```text
SID=marta/e73ecafdcddd4c5b2f590f1ebf630c07e26d73c9
LSID=null
Auth=marta/e73ecafd… (truncated)
```

Every later call carries the header
`Authorization: GoogleLogin auth=<Auth>`.

**2. Unread counts.** One JSON answer,
per feed, per category label, and a
total — the same numbers the web page
showed:

```text
"max": 43
feed/3 (The Allotment Journal)  4
feed/1 (BBC News - World)       39
```

**3. The unread stream.**
`stream/contents/user/-/state/com.google/reading-list`
with `xt=user/-/state/com.google/read`
("exclude read") returned the 43 unread
items with ids like
`tag:google.com,2005:reader/item/00065e7765a2ef9d`,
titles, origins, and categories —
everything a client needs to render a
reading list offline.

**4. Mark read.** `edit-tag` takes an
item id, the tag
`a=user/-/state/com.google/read`, and a
short-lived token from
`reader/api/0/token`. Its whole reply
is `OK` — and the unread count fell
43 → 42, the Gardening label 4 → 3
(transcript `t08`). A client marking
articles read all day makes exactly
this call, repeatedly.

## The Fever API (documented)

FreshRSS also emulates the older
**Fever** API (a `fever.php` endpoint
beside `greader.php`), kept for clients
that speak it. Same API password, same
idea, smaller dialect. It was not
exercised by the lab; the chapters
claim nothing about it beyond that it
is there and documented by the project.

## Client apps (documented)

The apps are how most people *meet*
FreshRSS daily — the server is plumbing
behind a phone's icon. The project's
documentation keeps the current list of
Google-Reader- and Fever-compatible
clients for Android, iOS, and desktop.
The lab installed none of them — there
was no phone on the bench — but note
what "compatible" now means in
evidence: any client speaking this
dialect can do the four calls above,
because the lab just did them with the
world's plainest HTTP tool.

Check: log in with curl, ask for the
unread count, and compare it with your
web page's title. Two surfaces, one
number — that agreement is the API
keeping its promise.
