# ARC-AGI-3 Arcade Agent

QOR-powered agent that plays ARC-AGI-3 arcade games. Learns from each attempt — wins are saved and replayed instantly on future runs.

## Quick Start

```bash
# Set your API key (get it from https://arcprize.org)
set ARC_API_KEY=your-api-key-here

# Run
arc3.exe
```

Or pass the key directly:
```bash
arc3.exe --api-key your-api-key-here
```

## How It Works

```
TRY → LEARN → REPLAY
```

1. **Try**: Plays each game using QOR reasoning rules
2. **Learn**: On level-up, saves the winning action sequence. On failure, saves the failed attempt
3. **Replay**: Next run, solved levels are replayed instantly (~1 second each)
4. **Score grows**: Same scorecard across runs, won games are skipped

## Options

| Flag | Description |
|------|-------------|
| `--api-key KEY` | ARC API key (or set `ARC_API_KEY` env var) |
| `--game PREFIX` | Only play games matching PREFIX (e.g., `--game ft`) |
| `--scorecard ID` | Use a specific scorecard ID |
| `--close-scorecard` | Close scorecard after this run (start fresh next time) |
| `--dna-dir PATH` | Custom path to DNA folder |
| `-h, --help` | Show help |

## Scorecard

The scorecard **stays open across runs** so your score accumulates:

```
Run 1:  New scorecard → plays games → wins some → scorecard stays OPEN
Run 2:  Same scorecard → skips won games → plays remaining → score grows
Run 3:  Same → keeps growing
```

To start fresh: `arc3.exe --close-scorecard`

## Files

```
arc3.exe                              The agent
dna/puzzle_solver/
    arcade.qor                        Game strategy rules
    game_rules.json                   Saved combos + game state (auto-updated)
    active_scorecard.txt              Current scorecard ID (auto-managed)
    arcade_memory.qor                 Learned knowledge (auto-created)
    arcade_rules_learned.qor          Discovered rules (auto-created)
```

## Requirements

- Windows 10/11
- Internet connection (API calls to arcprize.org)
- ARC API key
