# Getting Started

This guide is for Power BI users who are new to terminal-based workflows.

## Install

Download the latest installer for your platform from [GitHub Releases](https://github.com/maxanatsko/pbir.tools/releases), run it, then open a new terminal and verify:

```bash
pbir --version
```

### If Your OS Blocks the Installer

The installers do not currently ship with a developer certificate, so both platforms may warn before opening them.

#### macOS

If macOS refuses to open the installer:

1. Try to open the installer once.
2. Open `System Settings`.
3. Go to `Privacy & Security`.
4. Scroll down to the `Security` section that mentions the blocked installer.
5. Click `Open Anyway`.
6. When macOS prompts again, click `Open`.
7. Finish the installer.

#### Windows

If Windows SmartScreen blocks the installer:

1. Look for the SmartScreen dialog that says `Windows protected your PC`.
2. Click `More info`.
3. Confirm the installer name.
4. Click `Run anyway`.
5. Continue the installer normally.

## Terminal Basics

The terminal is just a text-based way to run commands.

### Open a Terminal

- macOS: open `Terminal`
- Windows: open `PowerShell`, `Command Prompt`, or `Windows Terminal`

### A Few Basics

```bash
pwd
cd "C:\Users\YourName\Documents\Reports"
cd ~/Documents/Reports
```

- `pwd` shows where you are.
- `cd` changes folders.
- Quote paths that contain spaces.
- Press `Tab` to autocomplete file and folder names.

## Your First 5 Minutes

### 1. Go to the folder that contains your PBIR report

```bash
cd "C:\Users\YourName\Documents\My Reports"
```

### 2. Find reports

```bash
pbir ls
```

### 3. Inspect the structure

```bash
pbir tree "Sales.Report" -v
```

This shows pages, visuals, and the fields each visual uses.

### 4. Inspect the semantic model

```bash
pbir model "Sales.Report" -d
```

Use this before adding or rebinding visuals so you know the table, column, and measure names available to you.

### 5. Make a simple change

```bash
pbir add visual card "Sales.Report/Overview.Page" --title "Revenue" -d "Values:Sales.Revenue"
```

### 6. Validate

```bash
pbir validate "Sales.Report"
```

## Path Syntax

`pbir` addresses report objects with filesystem-style paths:

```text
Report.Report/Page.Page/Visual.Visual
```

Examples:

```text
Sales.Report
Sales.Report/Overview.Page
Sales.Report/Overview.Page/Revenue.Visual
Sales.Report/**/*.Visual
My Workspace.Workspace/Sales.Report
```

Use quoted paths when names contain spaces.

## A Safe Default Workflow

For most report edits:

```bash
pbir backup "Sales.Report" -m "Before edits"
pbir tree "Sales.Report" -v
pbir validate "Sales.Report"
```

If something goes wrong:

```bash
pbir backup --list "Sales.Report"
pbir restore "Sales.Report"
```

## Working With AI Assistants

If you want local assistant integration, use `pbir setup` to install assistant-specific rules or skills:

```bash
pbir setup --claude-code
pbir setup --cursor
pbir setup --copilot
```

## Next Steps

- [CLI Docs](cli/README.md)
- [CLI Workflows](cli/workflows.md)

## Help

- `pbir --help`
- `pbir <command> --help`
