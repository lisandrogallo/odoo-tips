# Views

## Focus the create/edit cursor over a specific field rather than first

```xml
    <field name="field" default_focus="1"/>
```

## Highlight rows based on today in tree view

In XML side `< > <= >=` are not supported, so we need to use `< > ≤ ≥` instead.

```xml
<tree colors="blue:due_date < current_date;">
    <field name="due_date"/>
</tree>
```

## Domain filter based in date/time delta

```xml
<field name="domain">[('date', '>', (context_today().strftime('%Y-%m-%d'))), ('date', '<', ((context_today()+datetime.timedelta(days=365)).strftime('%Y-%m-%d')))]</field>
```

## Changing attrs based on an empty many2many relation

`False` or `None` comparison will not work.

```xml
<field name="name" attrs="{'invisible': [('field_ids', '=', [])]}">
```

## List of options for decoration attribute

```xml
<tree decoration-it="field=='value'">
```

- decoration-bf: BOLD
- decoration-it: ITALICS
- decoration-danger: LIGHT RED
- decoration-info: LIGHT BLUE
- decoration-muted: LIGHT GRAY
- decoration-primary: LIGHT PURPLE
- decoration-success: LIGHT GREEN
- decoration-warning: LIGHT BROWN
