# Configuration and Agent Setup

These commands control how `pbir` behaves on your machine and help you set up agent-friendly local files.

Most users will only touch this section occasionally, usually when:

- setting a preferred output or debug mode
- checking where config and schema files live
- installing skills and plugins for an agent they already use

## `pbir config`

`pbir config` manages the CLI configuration file.

```bash
pbir config show
pbir config init
pbir config set debug true
pbir config set output json
pbir config paths
```

Use it when you want to make the CLI behave more predictably across sessions instead of passing the same flags every time.

| Command | Purpose |
|---|---|
| `show` | Display the current configuration |
| `init` | Create a default config file |
| `set` | Update a config value |
| `paths` | Show where config, templates, and schemas are resolved from |

## `pbir setup`

`pbir setup` installs Power BI plugins from the [power-bi-agentic-development](https://github.com/data-goblin/power-bi-agentic-development) marketplace. These plugins provide skills, hooks, and agents that teach your coding agent how to use `pbir` effectively.

It auto-detects which agents you have installed and lets you pick which plugins to install interactively.

```bash
pbir setup                                      # Interactive (detect agents)
pbir setup --all                                # Install all plugins, all agents
pbir setup --agent claude-code --all            # Claude Code only, all plugins
pbir setup --plugin reports --plugin fabric-cli # Specific plugins
pbir setup --force                              # Force reinstall
pbir setup uninstall                            # Show removal instructions
```

| Flag | Purpose |
|---|---|
| `--agent` / `-a` | Target agent: `claude-code`, `copilot`, `cursor`, `gemini`, `codex` |
| `--plugin` / `-p` | Specific plugin(s) to install (repeatable) |
| `--all` | Install all available plugins |
| `--force` / `-f` | Force reinstall plugins |

For report-specific Claude Code hooks:

```bash
pbir setup report "Sales.Report" --claude-hooks
```

## Environment Variables

Environment variables are useful when you want the same behavior in every terminal session.

| Variable | Purpose |
|---|---|
| `PBIR_QUIET=1` | Reduce tips, spinners, and animations |
| `PBIR_DEBUG=1` | Show debug logging and tracebacks |
| `PBIR_CONFIG` | Override the config file path |

## Global Flags

Global flags go before the subcommand:

```bash
pbir -q ls "Report.Report"
pbir --debug validate "Report.Report"
```

| Flag | Purpose |
|---|---|
| `-q`, `--quiet` | Reduce non-essential output |
| `--debug` | Enable debug logging |
| `-V`, `--version` | Show version |
| `-i`, `--interactive` | Launch interactive browser mode |
| `--show-legacy` | Include legacy reports that still need conversion |
