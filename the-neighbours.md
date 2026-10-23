# The Neighbours

**Scope:** the other ways to read
feeds — hosted readers, other
self-hosted readers, and the apps that
skip servers — and what each trades
against FreshRSS's bargain. Descriptions
here are orientation, not reviews; the
honest question is which trade suits
your household.

## The hosted readers

**Feedly** and **Inoreader** are the
big subscription readers: polished apps,
discovery tools, AI summaries and
rule engines on the paid tiers, and
your reading list and read state on
their servers under their terms. For
many people they are simply the right
answer — the trade FreshRSS refuses is
the one they make easy: no server of
yours, no server of yours. **NewsBlur**
sits between: hosted, open-source,
unusual training features. All three
import and export OPML, which is why
chapter 4 calls OPML a suitcase — you
can leave in either direction.

## The self-hosted neighbours

**Miniflux** is the minimalist of the
family: one Go binary, PostgreSQL, a
deliberately spare interface, a fine
API. Readers who find FreshRSS busy
often land there; readers who want
categories, filters, and a friendlier
face land here. **Tiny Tiny RSS** is
the elder: powerful filtering, a
plugin culture, a sterner interface.
**CommaFeed** and others cover the
same ground with different tempers.
All of them keep your data home; the
differences are appetite and furniture,
not principle.

## The app-only readers

Plenty of phone and desktop apps read
feeds with no server at all, syncing
through a cloud account or not at all.
They are the lightest start — and the
read state lives in the app's world,
which is the thing chapter 1 said a
server exists to solve. Many of those
same apps can *also* speak the Google
Reader API, which makes them FreshRSS
clients (chapter 8): the app is a
face; whose server stands behind it is
a choice you can change later.

## The adjoining tools

Not rivals: **read-it-later** services
(wallabag and friends) keep the *whole
article* forever, where FreshRSS keeps
the stream; **feed generators** make
feeds for sites that lack them;
**newsletter-to-feed** bridges rescue
the one writer who only mails. A
mature setup often runs one of each —
FreshRSS in the middle, deciding what
deserves keeping.

Check: if a neighbour tempts you, the
question to ask is never "which is
best" but "where do my subscriptions
and read state live, and what does the
rent cost — money, attention, or a
server to feed?" OPML means the answer
is never a life sentence.
