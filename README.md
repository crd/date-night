# date-night

A Claude Code skill for planning dates in Buffalo, NY and Western New York. Gets smarter over time — it learns what you and your partner actually enjoy from your reactions and past experiences, so suggestions become more personal with every use.

## What it does

- Plans full date itineraries (not just lists of options) based on your preferences, the season, and what's happening this week
- Checks live event calendars (Step Out Buffalo, Buffalo Waterfront) for time-sensitive suggestions
- Tracks which date ideas you liked or skipped, and how actual dates went
- Builds a picture of what works for your specific relationship over time
- Maintains a growing database of Buffalo venues, updated as new places are discovered

## Installation

### Via skills.sh (recommended)

```bash
skills install date-night
```

### Manual

Copy the `date-night/` folder to your Claude Code skills directory:

```bash
cp -r date-night/ ~/.claude/skills/
```

## First run

The first time you ask Claude to plan a date, it will run a short onboarding — five conversational questions about alcohol preferences, activity level, budget, interests, and any hard constraints. This takes about a minute and makes every future suggestion significantly better.

Your answers are saved to `~/.config/date-planning/preferences.json`. This file lives outside the skill directory, so it won't be overwritten if you update the skill.

## Your data

All personal data lives at `~/.config/date-planning/`:

```
~/.config/date-planning/
├── preferences.json   # Your onboarding answers (alcohol, budget, interests, etc.)
└── history.json       # Concept reactions + experience logs
```

**preferences.json** — updated when you tell Claude something enduring has changed ("we stopped drinking", "tighter budget these days", "she has a bad knee now").

**history.json** — two kinds of signal:
- *Concept reactions*: when you say "I love that idea" or "not for us" during planning, Claude quietly logs it as a weak signal of taste
- *Experience logs*: when you come back after a date and say how it went, Claude logs the rating and what worked — this is the strongest signal and makes future suggestions meaningfully better

To reset your preferences and start fresh:
```bash
rm -rf ~/.config/date-planning/
```

To export your history:
```bash
cat ~/.config/date-planning/history.json
```

## Updating preferences

Just tell Claude directly:
- "We don't drink anymore" → updates `alcohol` preference
- "We're on a tighter budget" → updates `budget_typical`
- "She has a bad knee, avoid lots of stairs" → updates `hard_constraints.mobility`

Claude will confirm what it saved.

## Logging a date

After you go out, come back and tell Claude how it went. Even a quick "that was great" or "it was kind of a bust" gives Claude enough to log. The more detail you share, the more useful the history becomes.

Rating scale: 1 = disaster · 2 = meh · 3 = fine · 4 = good · 5 = great

## Expanding to other cities

The skill currently covers **Buffalo, NY and Western New York** including Niagara Falls. The venue database is at `resources/buffalo-resources.json`.

To add coverage for another city, ask Claude: "Can you start building a Rochester venue list?" It will create `resources/rochester-resources.json` following the same schema and add venues as it discovers them.

## Contributing

Pull requests welcome, especially:
- New Buffalo/WNY venues (add to `resources/buffalo-resources.json`)
- Coverage for other cities (new `resources/<city>-resources.json`)
- Improvements to the onboarding questions
- Bug reports

## License

MIT
