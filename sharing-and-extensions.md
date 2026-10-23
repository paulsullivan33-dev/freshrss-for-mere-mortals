# Sharing and Extensions

**Scope:** the doors FreshRSS opens
outward on purpose — share links, each
reader's public page, RSS feeds *of*
your FreshRSS — and the extension and
theme system for changing how it looks
and behaves. This chapter is mostly
**documented, not demonstrated**: the
lab installed no extension and changed
no theme, and it says so rather than
pretending a tour was a test.

## Sharing an article

Every article carries share actions:
send it to a read-it-later service,
post the link, mail it. The list of
destinations is configurable per user,
from a long built-in menu. This is the
small, deliberate kind of sharing — a
person choosing one article — and it
needs no setup beyond picking which
destinations appear.

## Your reading, published back

FreshRSS can also face outward in two
structured ways:

- **A public page per reader** (if the
  admin enables it): a read-only view
  of a reader's stream at a public
  address — the household member who
  curates the good links gets a page
  the others can bookmark.
- **Feeds of your reader**: your
  starred articles, a category, a tag,
  or a search can each be exported as
  an RSS feed of their own (with a
  token in the address, since the
  contents are yours). Point another
  tool — or another FreshRSS — at it.

Both are off or private by default in
spirit: you turn a stream public
deliberately, per reader. Treat a
tokenised feed address like a password
to exactly that list, because it is
one.

## Extensions

Extensions are small PHP/JavaScript
add-ons that hook the application:
extra themes, new share destinations,
reading tweaks, integrations. They live
in the `extensions/` folder (the
project ships a few core ones, such as
custom CSS/JS injectors), are enabled
per user or site-wide, and come from
the project's extension library. Two
honest cautions, both documented by
the project and repeated here:
extensions run with the application's
powers, so install them the way you
install any software — from sources you
trust; and an extension can break on
upgrade in ways core features should
not, so the standing install keeps its
list short.

## Themes

The web UI's look is themeable —
several themes ship in the box, from
dense and dark to paper-like — and a
reader's theme is their own setting,
not the server's. Custom CSS via the
core extension is the usual last step
for "almost what I want".

Check: this chapter has no lab
transcript behind it, deliberately.
Decide which of these doors you
actually want open — a shared-stars
feed is a delight; three public
surfaces you forgot about are a small
liability — and open exactly those.
