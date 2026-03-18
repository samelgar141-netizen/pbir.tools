# Configuration and Assistant Setup

These commands are not about editing report content directly. They control how `pbir` behaves on your machine and help you set up assistant-friendly local files.

Most users will only touch this section occasionally, usually when:

- setting a preferred output or debug mode
- checking where config and schema files live
- installing local instructions or skills for an assistant they already use

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

`pbir setup` installs assistant-specific files for local AI-assisted workflows.

It is useful when you already work with tools like Claude Code, Cursor, Copilot, Gemini CLI, or Pi and want `pbir`-specific instructions or helper files in the right place.

Common examples:

```bash
pbir setup --claude-code
pbir setup --cursor
pbir setup --copilot
pbir setup --gemini
pbir setup --pi
pbir setup --claude-code --memory claude.md
pbir setup --claude-code --user
pbir setup --claude-code --project
pbir setup report "Sales.Report" --claude-hooks
pbir setup uninstall
```

What it supports:

- Claude Code skills and hook files
- Cursor rules
- GitHub Copilot instructions
- Gemini CLI instructions
- Pi instructions
- user-level or project-level installation
- optional memory files

Use `pbir setup report "Report.Report" --claude-hooks` when you want report-local Claude Code hook files for deployment-oriented workflows around a specific report.

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
