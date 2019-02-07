# Actions

## Open URL on new tab using a function

```python
@api.multi
def open_url(self):
    return {
        'type': 'ir.actions.act_url',
        'url': url,
        'target': 'new',
        'nodestroy': True,
    }
```

## Action declaration to open URL on a new tab

```
<!-- URL ACTION -->
<record model="ir.actions.act_url" id="action_siat_website">
    <field name="name">Name</field>
    <field name="view_mode">tree,form</field>
    <field name="target">new</field>
    <field name="url">www.example.com</field>
</record>
```

## Action flags

- initial_mode: 'view' or 'edit'
- mode: 'view' or 'edit'

For example:

```
'flags': {
    'initial_mode': 'view',
    'form': {
        'options': {'mode': 'view'},
        'action_buttons': True
    }
```

## Define specific (not default) views in window action

```xml
<field name="view_ids" eval="[(5, 0, 0),
    (0, 0, {'view_mode': 'tree', 'view_id': ref('xml.id.of.tree.view')}),
    (0, 0, {'view_mode': 'form', 'view_id': ref('xml.id.of.form.view')})]"/>
```