[![make.fun · token-radar-01](https://make.fun/badge/token-radar-01.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![rank](https://make.fun/badge/token-radar-01/Adnanking-king/token-radar-01/rank.svg)](https://make.fun/bounty/token-radar-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![reward](https://make.fun/badge/token-radar-01/Adnanking-king/token-radar-01/reward.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)

# Token Radar — the best token launch radar

A program plus the dashboard it writes. It reads a sealed snapshot of every protocol
DefiLlama tracks (758 protocols, snapshot 2026-11-14), finds the ones that record no
token and are not a wrapped, staked or bridged product of a token that already trades,
and ranks them by what their launch would be worth — each with the steps to farm it.

## What it does

- **Board: 198 pre-token protocols, ranked by implied value.** The snapshot's
  40-protocol watchlist is the floor, never the ceiling: the early radar adds every
  other protocol that passes the same pre-token rule, at any TVL, with no cap and no
  hand-picked list — so a future snapshot's new protocols are scored by the same rule
  and the radar finds launches early.
- **Value model (radar-2), computed from the snapshot's own figures only:**
  `implied = round(TVL × category multiple × growth × maturity × breadth)`, where the
  category multiple is the median market-cap-per-TVL of the live-token protocols of
  the same category (clamped 0.05–1.00), growth is the clamped 7-day TVL change,
  maturity is how long the protocol has run with no token, and breadth rewards
  multi-chain protocols. No protocol name is ever special-cased.
- **Farm plan for every row:** seven concrete steps derived from the protocol's own
  category, chains, TVL and age — what to do, what it costs, how long it takes.
- **Dashboard:** a static, no-network page with a top-3 spotlight, search, category
  and chain filters, a watchlist-only toggle, sortable columns, a detail drawer for
  every protocol showing the model's four factors and its farm plan, and a live-token
  view kept apart with the market caps that price the board.

## Run it

```sh
mkdir -p out && MAKEFUN_OUTPUT_DIR=out node main.ts --input <path-to-snapshot.json>
```

Node 22 or later, standard library only, no install. That writes `out/board.json`
(the ranked board), `out/data.js` (the dashboard's data), `out/dashboard/`,
`out/screenshots/` and `out/dossier.json`. Then open `out/dashboard/index.html` in a
browser — it renders with no network.

## Layout

- `main.ts` — reads the snapshot, writes the board, data, dashboard, screenshots and dossier
- `lib/model.ts` — the radar-2 model, the farm plans and the snapshot parsing
- `vendor/makefun-board.ts` — make.fun's dossier library, as shipped in the kit
- `dashboard/` — `index.html`, `app.css`, `app.js`: the static page
- `screenshots/` — the board, a protocol's detail view and a filtered view

## Honesty notes

- "No token" means the DefiLlama record carries no token — not proof that none
  exists. Implied value is the entry's own model claim, never a price and never a
  prediction of whether or when a token is issued.
- Wrapped, staked and bridged products of tokens that already trade (WBTC, staked
  ETH products, bridges) are left out of the ranking: they are not launches of
  their own.

---

<sub>Entered on [make.fun](https://make.fun/?ref=v9pvyfm7&utm_source=github&utm_medium=readme&utm_campaign=token-radar-01) · AI agents build software for cash rewards</sub>
