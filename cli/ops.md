# Operations

This section covers the commands you use around the edit loop rather than inside it.

Think of these as the commands that make CLI work safe and practical:

- validate the report after changes
- create backups before risky edits
- recover from mistakes
- move reports between local PBIR folders and Fabric
- open the result in Power BI Desktop

## `validate`

`pbir validate` is the command you should trust most. Run it after every mutation.

```bash
pbir validate "Report.Report"
pbir validate "Report.Report" --qa
pbir validate "Report.Report" --all
pbir validate "Report.Report" --fields
pbir validate "Report.Report" --strict
```

Use different validation levels depending on what changed:

- plain `validate` for everyday structure checks
- `--fields` after rebinding or field changes
- `--qa` after layout and formatting passes
- `--all` before publishing or handing the report to someone else

| Flag | Purpose |
|---|---|
| `--fields` | Confirm fields still exist in the connected model |
| `--qa` | Run quality checks such as overlaps and hidden visuals |
| `--all` | Run schema, field, and QA checks together |
| `--strict` | Treat warnings as errors |
| `--json` | Machine-readable output |
| `--tree` | Tree view of results |

## `backup` and `restore`

These commands protect you from yourself.

Use backups before larger edits, especially:

- bulk formatting
- report conversion
- merge and split operations
- publish workflows with tight deadlines

```bash
pbir backup "Report.Report"
pbir backup "Report.Report" -m "Before restyle"
pbir backup --list "Report.Report"
pbir backup --prune "Report.Report" --keep 5

pbir restore "Report.Report"
pbir restore "Report.Report" --backup-id 20260312T143000Z
pbir restore "Report.Report" -f
```

## `download`

`pbir download` is the handoff from Fabric to local PBIR work.

Use it when the report starts in a workspace and you want a local folder you can inspect, edit, validate, and version.

```bash
pbir download "My Workspace.Workspace"
pbir download "My Workspace.Workspace/Sales.Report" -o ./working --format pbir
pbir download "My Workspace.Workspace/Sales.Report" -o ./working --format pbip --open
```

This requires Microsoft Fabric CLI to be installed and authenticated.

## `publish`

`pbir publish` is the reverse flow: local report back to Fabric.

```bash
pbir publish "Sales.Report" "My Workspace.Workspace/Sales.Report"
pbir publish "Sales.Report" "My Workspace.Workspace/Sales.Report" -f -o
pbir publish
```

Use `-f` carefully. It is for overwrite scenarios, not ordinary publishing by default.

## `open`

`pbir open` is a convenience command for jumping back into Power BI Desktop after CLI work.

```bash
pbir open "Sales.Report"
pbir open "Sales.Report/Overview.Page"
```

If you pass a page path, `pbir` sets that page active before opening the report.

## Advanced: `script`

`pbir script` exists for advanced Python-based automation when the built-in command surface is not enough.

```bash
pbir script --list-examples
pbir script my_script.py "Sales.Report"
```

This is deliberately an advanced escape hatch, not the primary way most end users should approach `pbir`. If you need it, start with `pbir script --help`.
