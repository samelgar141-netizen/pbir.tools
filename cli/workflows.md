# Workflows

These walkthroughs show how the CLI fits together in real work. Each one is a sequence you can copy and adapt, not just isolated command examples.

## Create a Simple Report

Use this flow when you are starting from a semantic model and want a minimal, valid report quickly.

```bash
pbir new report "Sales.Report" --connection "My Workspace.Workspace/SalesModel.SemanticModel"
pbir pages rename "Sales.Report/Page 1.Page" "Overview"
pbir model "Sales.Report" -d
pbir add visual card "Sales.Report/Overview.Page" --title "Revenue" -d "Values:Sales.Revenue"
pbir add visual lineChart "Sales.Report/Overview.Page" --title "Trend" -d "Category:Date.Date" -d "Values:Sales.Revenue"
pbir validate "Sales.Report"
```

Why this order works:

- `new report` gives you a clean starting point
- `model -d` shows the fields you can bind safely
- visuals are added only after the page and data model are clear
- validation closes the loop before more changes stack up

## Bulk-Format a Report

Use this when the report structure is already right and you want consistency across many visuals.

```bash
pbir backup "Sales.Report" -m "Before bulk formatting"
pbir set "Sales.Report/**/*.Visual.title.fontSize" --value 14 -f
pbir set "Sales.Report/**/*.Visual.border.show" --value true -f
pbir set "Sales.Report/**/*.Visual.border.radius" --value 8 -f
pbir validate "Sales.Report"
```

The backup matters here because bulk changes can touch dozens of visuals at once.

## Theme-First Styling

Use theme commands when you want consistent defaults rather than one-off overrides on each visual.

```bash
pbir theme set-colors "Sales.Report" --primary "#2B579A" --secondary "#217346"
pbir theme set-formatting "Sales.Report" "*.border.radius" --value 8
pbir theme set-formatting "Sales.Report" "card.*.border.show" --value true
pbir validate "Sales.Report"
```

This is usually easier to maintain than pushing the same formatting to every visual manually.

## Download, Edit, Publish

Use this flow when the source of truth starts in Fabric but the actual editing work happens locally.

```bash
pbir download "My Workspace.Workspace/Sales.Report" -o ./working --format pbir
cd working
pbir tree "Sales.Report" -v
pbir visuals title "Sales.Report/Overview.Page/Revenue.Visual" --text "Net Revenue" --bold
pbir validate "Sales.Report"
pbir publish "Sales.Report" "My Workspace.Workspace/Sales.Report" -f
```

The key point is that `download` and `publish` are the edges of the workflow. The real inspection and editing still happen against the local report folder.

## Audit an Existing Report

Use this when you inherit a report or need to understand it before changing anything.

```bash
pbir tree "Sales.Report" -v
pbir fields list "Sales.Report"
pbir filters list "Sales.Report"
pbir annotations list "Sales.Report"
pbir validate "Sales.Report" --all
```

This gives you a strong high-level picture:

- tree for structure
- fields for data bindings
- filters for report behavior
- annotations for internal metadata
- full validation for structural confidence

## Prepare a Report for Safer Changes

Use this mini-workflow before any risky operation such as convert, merge, split, or large formatting passes.

```bash
pbir backup "Sales.Report" -m "Before risky changes"
pbir tree "Sales.Report" -v
pbir validate "Sales.Report" --all
```

It is simple, but it prevents a large share of avoidable mistakes.
