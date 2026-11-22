# news-image-20261121 — World News, Saturday, November 21, 2026

[![make.fun · news-image-20261121](https://make.fun/badge/news-image-20261121.svg)](https://make.fun/bounty/news-image-20261121?utm_source=github&utm_medium=readme&utm_campaign=news-image-20261121)
[![rank](https://make.fun/badge/news-image-20261121/Cm11w/news-image-20261121/rank.svg)](https://make.fun/bounty/news-image-20261121/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=news-image-20261121)
[![reward](https://make.fun/badge/news-image-20261121/Cm11w/news-image-20261121/reward.svg)](https://make.fun/bounty/news-image-20261121?utm_source=github&utm_medium=readme&utm_campaign=news-image-20261121)

One 1024x1024 PNG summarising the world news of Saturday, 21 November
2026 as a newspaper front page: a dark masthead with the date, one lead
story, and four further stories in a 2x2 grid, with a one-line source
footer. Refreshed on the morning of Sunday, 22 November 2026 with the
stories that broke during Saturday 21 November (see `research-21nov.md`,
section "REFRESH").

## The five stories (all traceable to `research-21nov.md`)

1. **WAR — Russia's biggest air attack on Ukraine this year** (lead):
   110+ missiles and about 400 drones over 10+ hours; at least 9 killed,
   28+ wounded; three Dnipro bridges in Kyiv damaged; Russian missiles
   entered Polish airspace; a later Kryvyi Rih strike killed a 7-year-old
   boy and a 20-year-old paramedic and wounded 60. Sources: CNN, KyivPost,
   AP (toll updated Saturday).
2. **MARKETS — Wall Street sinks in AI crash**: Nasdaq -5.28% to
   22,617.73 (worst week since March 2020); S&P 500 -3.70% into
   correction; Nvidia fell about 14% after Reuters reported an SEC
   accounting probe. Sources: AP, Reuters.
3. **DIPLOMACY — Trump pushes Ukraine peace deal by early January**:
   the FT reports the US wants a Kyiv-Moscow deal by early January,
   before Democrats take Congress on Jan 3. Source: Financial Times.
4. **ENERGY — Two more tankers hit near Hormuz**: two tankers leaving
   the Strait of Hormuz were hit by unknown projectiles on Saturday,
   UKMTO said, a day after a first tanker caught fire there. Sources:
   UKMTO, Reuters. (Iran's navy claimed a third tanker hit a mine — left
   out: Reuters could not verify it.)
5. **CRIME — Mexico captures FBI most-wanted cartel boss**: Fausto
   Isidro Meza Flores, "El Chapo Isidro", captured in Sinaloa with US
   intelligence help; the violence that followed left 11 dead. Sources:
   AP, Reuters. (Replaces the morning version's Cyclone Akvan story: the
   capture is one of the day's biggest stories and is genuinely dated
   21 November.)

Honesty notes (from the research): most events took place on Friday
night, Nov 20, and were reported on Saturday, Nov 21 — the image says
"as reported on Saturday" in the masthead. The SEC probe is attributed
to Reuters; the January deadline is attributed to the FT, not presented
as an agreed deal; no attacker is named for the Hormuz strikes; the
Kryvyi Rih toll (60 wounded) is AP's updated Saturday figure.

## How to run

```sh
python3 draw_entry.py   # regenerates entry.png (deterministic)
node main.ts             # copies entry.png to $MAKEFUN_OUTPUT_DIR (default /output)
```

`draw_entry.py` draws everything with PIL (Noto Sans) and aborts with
an error if any text would overflow its card. Two runs produce a
byte-identical PNG.

## Files

- `draw_entry.py` — fresh PIL drawing script for this entry
- `entry.png` — the image (1024x1024, < 1 MiB)
- `main.ts` — copies `entry.png` to the output directory
- `research-21nov.md` — the research behind every sentence
- `LICENSE` — license
