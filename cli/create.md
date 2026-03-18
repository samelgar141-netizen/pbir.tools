# Create and Duplicate

Use these commands to create new reports, pages, visuals, and supporting objects, or to copy and move existing ones.

## `new report`

```bash
pbir new report "Sales.Report" --connection "Workspace/Model.SemanticModel"
pbir new report "Sales.Report" --from-template my-dashboard
pbir new report --list-templates
```

After creation, rename the default page, add visuals, and validate:

```bash
pbir pages rename "Sales.Report/Page 1.Page" "Overview"
pbir add visual card "Sales.Report/Overview.Page" --title "Revenue" -d "Values:Sales.Revenue"
pbir validate "Sales.Report"
```

## `add`

Common add flows:

```bash
pbir add page "Sales.Report/Dashboard.Page" -n "Dashboard"
pbir add visual card "Sales.Report/Overview.Page" --title "Revenue" -d "Values:Sales.Revenue"
pbir add title "Sales.Report/Overview.Page" "Executive Summary"
pbir add subtitle "Sales.Report/Overview.Page" "Q4 performance"
pbir add filter Date Year -r "Sales.Report"
pbir add annotation "Sales.Report" --name version --value "1.0"
pbir add image "Sales.Report" --source logo.png
pbir add visual --list
```

### Data Binding Shorthand

Use `-d` during visual creation:

```bash
pbir add visual card "path" -d "Values:Sales.Revenue"
pbir add visual columnChart "path" -d "Category:Products.Name" -d "Values:Sales.Revenue"
```

## `cp`

```bash
pbir cp "Source.Report" "Target.Report"
pbir cp "Source.Report" "Target.Report" --format pbix
pbir cp "Source.Report/theme" "Target.Report/theme"
pbir cp "Report.Report/Page1.Page" "Report.Report/Page2.Page"
pbir cp "Source.Report" "Target.Report" --measures
pbir cp "S.Report/P.Page/V1.Visual" "S.Report/P.Page/V2.Visual" --viscalcs
```

## `mv`

```bash
pbir mv "Report.Report/Old.Page" "Report.Report/New.Page"
pbir mv "Report1.Report/Page.Page" "Report2.Report/Page.Page"
pbir mv "Report.Report/Page.Page/Old.Visual" "Report.Report/Page.Page/New.Visual"
```

Use `pbir report rename` to rename the report itself.
