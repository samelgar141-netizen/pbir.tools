# Report Operations

These commands affect the report as a whole rather than an individual page or visual.

Use them when the task is structural:

- rename the report
- point it at a different semantic model
- convert between formats
- combine reports
- split reports apart

Because these commands operate at report scope, they are usually more consequential than everyday formatting commands. Back up first.

## `rename`

Use this when you want the report folder and display name to stay in sync.

```bash
pbir report rename "Report.Report" "New Report Name"
```

This updates the folder name and the `.platform` display name.

## `rebind`

Use this when the report should stay the same visually but connect to a different semantic model.

```bash
pbir report rebind "Report.Report" "Workspace.Workspace/Model.SemanticModel"
```

Run `pbir validate "Report.Report" --fields` after rebinding.

## `convert`

Use this when moving between PBIR, PBIP, and PBIX packaging.

```bash
pbir report convert "Report.Report" -F pbix
pbir report convert "Report.Report" -F pbip
pbir report convert "Report.pbip" -F pbir
```

Conversion uses atomic staging, which reduces the chance of leaving a broken target behind if the conversion fails.

## `merge`

Use this when you want to combine multiple reports into one deliverable.

```bash
pbir report merge "R1.Report" "R2.Report" -o "Combined.Report"
```

This is a good candidate for a backup-first workflow because name collisions and layout cleanup often follow.

## `merge-to-thick`

Use this when you need to combine a thin report with a semantic model into a thick PBIP package.

```bash
pbir report merge-to-thick "Report.Report" "Model.SemanticModel"
```

## `split-pages`

Use this when a multi-page report should become separate single-page reports.

```bash
pbir report split-pages "Report.Report" -o ./split
```

## `split-from-thick`

Use this when you need to break a thick PBIP into a thin report flow.

```bash
pbir report split-from-thick ThickReport --target "Workspace/Model"
```

## `clear-diagram`

Use this when you want to remove the semantic model diagram layout file.

```bash
pbir report clear-diagram "Report.Report"
```
