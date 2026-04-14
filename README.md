# ccusagegraph

Terminal-based usage graph for [Claude Code](https://claude.ai/claude-code), powered by [ccusage](https://github.com/ryoppippi/ccusage).

Displays daily token usage and API costs as stacked bar charts, broken down by project. Automatically resolves project directory paths to readable short names and adapts the graph width to your terminal.

## Requirements

- Bash 4+
- [ccusage](https://github.com/ryoppippi/ccusage) installed and on `$PATH`
- [jq](https://jqlang.github.io/jq/)

## Installation

```bash
# Clone the repo
git clone https://github.com/cghamburg/ccusagegraph.git
cd ccusagegraph

# Make it available on your PATH
ln -s "$(pwd)/ccusagegraph" /usr/local/bin/ccusagegraph
```

## Usage

```
ccusagegraph [OPTIONS]

Time range:
  -s, --since YYYYMMDD   Start date
  -u, --until YYYYMMDD   End date
  -d, --days N           Last N days (default: 28)

Display:
  -c, --cost             Size bars by cost instead of tokens
  -n, --top N            Show top N projects (default: 8)

Projects:
  -l, --list             List all projects with costs
  -p, --project NAMES    Filter by project name (comma-separated)

  -v, --version          Show version
      --help             Show this help
```

## Examples

```bash
ccusagegraph                        # last 28 days, stacked by project
ccusagegraph -d 7                   # last week
ccusagegraph -d 30 -c              # last 30 days, bars sized by cost
ccusagegraph -l                    # list all projects
ccusagegraph -p myapp,tracker      # filter specific projects
```

### Sample output

```
  Claude Code Usage — Stacked by Project

  Date               Tokens   Cost $  Stacked
  ──────────────── ──────── ────────  ──────────────────────────────────────────
  2026-04-07 Tue      76.1M    43.89  ██████████████████
  2026-04-08 Wed     159.3M   101.38  █████████████████████████████████████████
  2026-04-09 Thu      58.4M    73.68  ████████████████
  2026-04-10 Fri      54.4M    47.24  ██████████████

  ── 4 days (2026-04-07 → 2026-04-10) | 348.2M tokens | $266.19 ──

  Legend: ██ project-a  ██ project-b  ██ other
```

Each project gets a distinct color. The graph width adapts to your terminal width.

## License

MIT
