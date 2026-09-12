# Nuzlocke Team Advisor

A three-screen tool for Pokémon Nuzlocke runners: pick your game, pick the battle that's ending your run, and see the exact teams other runners already beat it with.

- **Live:** https://beninburley.github.io/3_Screen/
- **Repo:** https://github.com/beninburley/3_Screen

## 1. The four questions

|                        |                                                                                                                                                                                                                                                                                                              |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Need**               | When facing a hard or unfamiliar battle in a Nuzlocke, players don't know which of their limited, permadeath-restricted Pokémon can realistically win, so they dig through scattered forum threads, YouTube videos, and Discord messages for team ideas, which eats into their evening and breaks immersion. |
| **Persona**            | The person who will use this product plays pokemon nuzlockes, both vanilla games and ROM hacks evey evening to blow off steam while also seeking to challenge themselves and their strategic thinking.                                                                                                       |
| **Primary capability** | The product will show them what other teams other nuzlockers have brought for each specific battle.                                                                                                                                                                                                          |
| **Fundamental value**  | Speed and convenience. Users are able to access vast amounts of nuzlocke knowledge in one simple page.                                                                                                                                                                                                       |

_Need, capability, and value are kept distinct on purpose: the need is the workaround cost, the capability is the literal feature (game → battle → results), and the value is the feeling it buys back (confidence/momentum), not the feature restated._

## 2. The three screens

| Screen             | Single job                                                                         | Why it earned a slot                                                                                                                      | Design question it tests                                                     |
| ------------------ | ---------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| **Start**          | State the capability and get the runner into the flow in one move                  | Every entry point risks diluting itself with secondary content; this one had to prove the payoff shows _before_ any browsing starts       | Does it signal the capability and value at a glance? (Q1, Q2)                |
| **Pick the Fight** | Narrow 31 games and hundreds of battles down to one, in two choices                | The payoff on screen 3 means nothing without a fast way to name the fight — this is where "look it up mid-run" either holds up or doesn't | Does a two-step filter match how runners actually search while playing? (Q3) |
| **Winning Teams**  | Deliver the actual payoff: proven teams for that exact battle, and why they worked | This is the reason the product exists; the other two screens exist only to get here quickly                                               | Is the team-card grouping intuitive in a five-second glance? (Q4)            |

## 3. Design question plan

| #   | Question asked                                                                                           | Predicted answer                                                                          | What it tests                                                                                                                      |
| --- | -------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| 1   | "Tell me about the last time you got stuck on a tough Nuzlocke fight. What did you end up doing?"        | They describe hopping between a subreddit, a Discord server, and a YouTube video mid-run. | Whether the workaround cost in the Need statement is real — a quick single-source answer would mean "speed" isn't a novel payoff.  |
| 2   | "If there was a solution for the issue we've talked about, how would you describe that solution?"        | "Faster" / "more convenient."                                                             | Whether speed/convenience is really the dominant payoff, not something else (e.g. trust, completeness).                            |
| 3   | "How often does this come up, and what are you usually doing right when you decide to look it up?"       | Multiple times per run, checked in the moment while playing.                              | Whether a fast, mid-play "browse while playing" flow is actually the right shape for the tool.                                     |
| 4   | "I'll show you this for five seconds, then hide it. What do you think this does?" (Winning Teams screen) | "It shows teams other people used to beat a specific fight in a Nuzlocke."                | Whether the design is legible on sight, and whether the card grouping communicates "these are the same kind of thing" fast enough. |

## 4. Design justification & first read

Opening the live URL fresh, against the same four checks from class:

- **Does the landing screen signal the capability and value before reading?** Yes — kicker line, one short headline naming the capability, and a single accent-colored CTA (`Pick the fight →`); the caption under it ("Two choices. No forum tabs.") names the exact workaround the Need statement assumes, which doubles as the value pitch.
- **Does everything on landing earn its place?** The "how it works" band and the stat band sit below strong dividers, in smaller type, with no CTA of their own — they support the one primary action instead of competing with it.
- **What groups together, and by which Gestalt principle?** On Pick the Fight, the search field sits directly under the step-2 heading and above the list it filters — **proximity** binding it to the list, not the game column. Team cards on Winning Teams share identical shape and rhythm in a grid with 2px gutters that double as dividers — **similarity** plus **common region**, signaling "these four are equal, comparable options."
- **Do screens 2 and 3 stay on mission, and is landing always reachable?** Yes — a persistent step control (`Home / 1 — Pick the fight / 2 — Winning teams`) is identical across all three screens, with Home always enabled.
- **What did the AI's first pass get wrong, skip, or oversimplify?** See the comparison below — the biggest miss was a single 28-word sentence doing the job a headline should have done, plus a duplicate nav link competing with the one primary button.
- **What motivated each change?**

| Change                                                                                    | Question / vocabulary behind it                                                                                                                                    |
| ----------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Split the hero into a short headline + subhead, cut the duplicate "Pick a fight" nav link | Q1/Q2 signaling — the hero gave a paragraph and a duplicate CTA equal weight to the one primary action, so nothing signaled the capability at a glance             |
| Added a persistent step control (Home / 1 / 2) on every screen                            | "Return to landing from everywhere" — the only way back had been a small text link with no sense of where you were in the flow                                     |
| Moved the search field directly under the Step 2 heading, above the list                  | Proximity — the field had no visual owner; it read as floating between the game list and the battle list                                                           |
| Added an "their ace / what ends runs here" band above the team cards                      | Q4 — a five-second glance showed six mons and a level, not _why_ that team beat this specific fight                                                                |
| Replaced per-row `border-right` rules with 2px grid gutters throughout                    | Common region/consistency — the old rule left a stray vertical line when cards wrapped on a narrower screen, and the three screens didn't share one grouping idiom |

**Before / after.** The clearest single comparison is the landing hero and navigation:

- **Before:** [`3eee261` — initial AI pass](https://github.com/beninburley/3_Screen/blob/3eee261cfb0249e56c6b1074eb48e7ce5307f544/Nuzlocke%20Team%20Advisor.dc.html#L39-L45) — one 28-word sentence at display size as the entire pitch, a "Pick a fight" link in the nav _and_ a "Pick a fight" button in the hero, and the only way back to landing was a 12px text link.
- **After:** [`3402765` — revision](https://github.com/beninburley/3_Screen/blob/34027655287802adc20210933b6200c910a9c1be/Nuzlocke%20Team%20Advisor.dc.html#L47-L60) — full diff: https://github.com/beninburley/3_Screen/compare/3eee261...3402765

The problem in class vocabulary: the first pass had **competing calls to action** (two "pick a fight" affordances, one in nav and one in hero) and **no visual hierarchy** separating the primary capability from supporting copy — not simply "it looked generic."
