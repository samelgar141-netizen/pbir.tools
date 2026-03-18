# Theme and Schema

Use theme commands to set defaults across a report, then use schema commands to discover the exact containers and property names you need.

## `theme`

### Inspect a Theme

```bash
pbir cat "Report.Report/theme"
pbir theme colors "Report.Report"
pbir theme text-classes "Report.Report"
pbir theme fonts "Report.Report"
```

### Set Colors and Typography

```bash
pbir theme set-colors "Report.Report" --primary "#2B579A" --secondary "#217346"
pbir theme colors "Report.Report" --replace "#FF0000" "#CC0000"
pbir theme colors "Report.Report" --normalize
pbir theme set-text-classes "Report.Report" --class title --fontSize 20 --bold
```

### Set Visual Defaults

```bash
pbir theme set-formatting "Report.Report" "*.border.radius" --value 8
pbir theme set-formatting "Report.Report" "card.*.border.show" --value true
pbir theme set-formatting "Report.Report" "lineChart.lineStyles.showMarker" --value true
pbir theme push-visual "Report.Report/Page.Page/Visual.Visual"
```

### Background, Icons, and Templates

```bash
pbir theme background "Report.Report" --image wallpaper.png
pbir theme icons "Report.Report" --list
pbir theme icons "Report.Report" --add icon.svg --name "custom-icon"
pbir theme list-templates
pbir theme create-template "Report.Report" --name "my-brand"
pbir theme apply-template "Report.Report" --template "my-brand"
```

### Serialize, Build, Validate, Rename

```bash
pbir theme serialize "Report.Report" -o CustomTheme.Theme
pbir theme build "CustomTheme.Theme"
pbir theme validate "Report.Report"
pbir theme rename "Report.Report" "MyCustomTheme"
```

## `schema`

### Discover What a Visual Supports

```bash
pbir schema types
pbir schema containers card
pbir schema describe card.title
pbir schema roles card
```

### Manage Local Schemas

```bash
pbir schema status
pbir schema fetch --yes
pbir schema check "Report.Report"
pbir schema upgrade "Report.Report"
pbir schema regenerate
```

### Typical Workflow

```bash
pbir schema containers lineChart
pbir schema describe lineChart.lineStyles
pbir visuals format "Report.Report/Page.Page/Visual.Visual" -p lineStyles
pbir set "Report.Report/Page.Page/Visual.Visual.lineStyles.showMarker" --value true
```
