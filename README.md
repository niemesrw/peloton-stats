# Peloton Stats

A Claude Code skill that fetches your weekly Peloton cycling stats directly from the Peloton API. Zero dependencies — uses only Python stdlib.

## What It Does

Pulls your last 7 days of cycling workouts and reports:

- Total rides, duration, calories, and output (kJ)
- Average power (watts), resistance (%), and cadence (RPM)
- A table of recent rides with class name, instructor, and metrics

Output is formatted as markdown.

## Setup

### 1. Set Credentials

```bash
export PELOTON_USERNAME="your-email@example.com"
export PELOTON_PASSWORD="your-password"
```

Add to your shell profile (`~/.zshrc`, `~/.bashrc`) to persist across sessions.

### 2. Install as a Claude Code Skill

Copy or clone into your Claude Code skills directory:

```bash
git clone https://github.com/niemesrw/peloton-stats.git ~/.claude/skills/peloton-stats
```

Then use it in Claude Code by asking for your Peloton stats — the skill triggers automatically.

### 3. Standalone Usage

```bash
python3 scripts/fetch_stats.py
```

## Example Output

```
## Peloton Weekly Cycling Stats

**4 rides** | **95 min** | **782 cal** | **395 kJ**

**Avg Power:** 146W | **Avg Resistance:** 42% | **Avg Cadence:** 82 RPM

### Recent Rides

| Date | Class | Instructor | Duration | Output | Calories |
|------|-------|------------|----------|--------|----------|
| Mon 03/10 | 30 min Pop Ride | Cody Rigsby | 30min | 285kJ | 310 |
| Sat 03/08 | 20 min Low Impact Ride | Sam Yo | 20min | 110kJ | 172 |
```

## How It Works

1. Authenticates via Peloton's OAuth2 endpoint
2. Fetches your recent workouts from `/api/user/{id}/workouts`
3. Pulls per-ride performance data from `/api/workout/{id}/performance_graph`
4. Filters to cycling workouts from the last 7 days
5. Aggregates and formats the results

## Notes

- Only fetches **cycling** workouts (not running, strength, yoga, etc.)
- Requires an active Peloton subscription
- Uses the unofficial Peloton API at `api.onepeloton.com`

## License

MIT

## Disclaimer

This project is not affiliated with, endorsed by, or connected to Peloton Interactive, Inc. It uses Peloton's unofficial API, which could change or break at any time. Use at your own risk.
