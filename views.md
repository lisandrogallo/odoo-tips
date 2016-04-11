# Views

### Highlight rows based on today in tree view

In XML side ```< > <= >=``` are not supported, so we need to use ```&lt; &gt; &le; &ge;``` instead.

```xml
<tree colors="blue:due_date &lt; current_date;">
    <field name="due_date"/>
</tree>
```
