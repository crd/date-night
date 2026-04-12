# date-night

**A Claude Code skill that learns what makes your relationship tick — and plans dates worth remembering.**

Most "date idea" tools give you the same generic suggestions every time. This one remembers. It knows you prefer outdoor adventures and intimate performances over loud bars. It knows Suzanne loves hands-on experiences. It knows East Aurora is a reliable hit and sports games aren't your thing. Every date you log makes the next suggestion more personal.

## What makes this different

**Asking Claude "give me a date idea"** gets you a generic answer calibrated to no one.

**date-night** builds a portrait of your couple over time:
- A taste profile from day one (12 activity sketches, takes 2 minutes)
- Real event fetching — it checks Eventbrite and local event sites, never invents events
- History that compounds: liked/disliked reactions, full date ratings, what worked and what didn't
- A living synthesis of what actually makes your dates good

After 5–10 logged dates, suggestions start feeling like they're from someone who actually knows you.

## Example

```
User: plan something for Saturday

date-night: Checking what's on this weekend...

The Plan: Photography + Elmwood

The AKG has a new photography exhibit opening Saturday — right in your wheelhouse
given how much you two enjoyed the art museum sketch. Doors at 10am, free admission.

Afterward, Elmwood Village is a 5-minute walk. Grab lunch at Merge (creative American,
great for lingering). If the weather holds, walk south on Elmwood — there's a Saturday
farmers market at Bidwell Park.

Backup: If the exhibit is crowded, Delaware Park is right there — grab coffee and walk
the lake loop instead.

Tips: No reservation needed for the museum. Merge takes walk-ins for lunch but fills
up after noon on weekends.
```

## Installation

```bash
npx skills add crd/date-night
```

Or manually copy the `date-night/` folder to `~/.claude/skills/`.

## First run

The first time you ask for date ideas, you'll go through a short onboarding:
1. Your city (used to find local venues and events)
2. How far you'd typically travel
3. A 12-sketch taste profile — rate each 1–5, takes about 2 minutes
4. Alcohol preferences (explicitly — there's an important distinction between "drinking as the destination" and "ambient")
5. Budget (or "no filter")
6. Any hard constraints
7. Your partner's name and any special occasions worth tracking

After that, just ask for dates. The more you use it, the better it gets.

## Your data

All personal data lives at `~/.config/date-night/` — outside the skill directory, never overwritten by updates.

```
~/.config/date-night/
├── preferences.json   # Your profile: location, tastes, partner name, special occasions
└── history.json       # Upcoming dates, reactions, experience log, learned patterns
```

To reset and start fresh:
```bash
rm -rf ~/.config/date-night/
```

## Things you can say

Beyond "plan a date", the skill responds naturally to:

- **"I want to surprise [partner]"** — gets one strong committed recommendation, no clarifying questions
- **"Show our history"** — readable summary of your logged dates
- **"What's worked for us"** — the skill's running synthesis of your patterns
- **"We're in [city] this weekend"** — plans for a travel destination without changing your home config
- **"We moved to [city]"** — updates your location permanently
- **"How have our dates been?"** — summary with ratings
- **"Redo the taste profile"** — refresh preferences after a life change

## How it learns

**Weak signal** — reactions during planning ("I love that", "not for us") logged quietly  
**Strong signal** — post-date reports ("that was amazing" / "it fell flat") with ratings 1–5  
**Synthesis** — after every third logged date, the skill updates a plain-English summary of what actually works for your couple

It also watches for ruts: if your last few dates follow the same pattern, it'll push something genuinely different.

## Special occasions

Add your anniversary, birthdays, or other recurring dates during onboarding (or any time). The skill will give you a heads-up 3 weeks before each one.

## Cities

**Buffalo, NY** is the most complete city in the database. For any other city, the skill builds a venue list from scratch using Eventbrite and web searches — it gets smarter about your city the more you use it in that location.

To contribute a city database, add a `resources/{city}-{state}.json` file following the schema in `buffalo-ny.json` and open a PR.

## Contributing

PRs welcome:
- New city resource files (`resources/{city}-{state}.json`)
- Improvements to the taste profile sketches
- Better onboarding questions
- Bug reports

## License

MIT
