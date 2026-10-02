# prixbase-node-r

Read-only Reddit Data API node for **prixbase.com** — a price-comparison and
product-recommendation website (monetized via affiliate commissions).

## Purpose

The site recommends products by measured user demand. Reddit threads are where
NAS/storage buyers ask real questions ("best NAS for Plex under €300",
"Synology or QNAP for my setup"). This node extracts product signals from public
discussions — product models, use cases, price ranges, common complaints — which
an LLM on the server side turns into product slots on the website.

## What it does on the Reddit platform

- Reads **public** posts and comments only.
- Subreddits: `r/homelab`, `r/synology`, `r/selfhosted`, and a few adjacent
  NAS/storage subreddits.
- Typical daily pattern: list recent posts in those subreddits (listing
  endpoints), then fetch top-level comments of posts that mention specific
  products.
- No posting, no commenting, no voting, no chat, no private data, no user
  profiling.
- Volume: at most a few hundred API calls per day, well under the free-tier
  100 QPM limit. One OAuth client, no account sharding, no proxy rotation.

## Authentication

Single OAuth2 client (`installed app`), device-flow token refresh, no
browser. The app is registered under `u/magnificoOrville`.

**User-Agent** (required format):

```
linux:prixbase-node-r:v1.0.0 (by /u/magnificoOrville)
```

## Data handling (per Reddit Data API Terms)

- Product-derived facts stored only: product names, use cases, prices mentioned.
- Raw post bodies are not stored as content; no user profiles are built.
- Any stored data linked to deleted posts, deleted comments, or deleted user
  accounts (including author IDs and references to them) is deleted routinely,
  within 48 hours.
- Credit: published slots link back to the source Reddit threads.

## Status

In development — the prixbase.com site is in a private build phase and goes
public at launch (late 2027). This repo will contain the bot source code as it
is built; the README documents the intended behavior for the API access
request.

## Contact

`axalainsanchez@gmail.com`
