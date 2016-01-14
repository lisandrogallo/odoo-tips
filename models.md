# Models

## Restrict deletion of records that are still referenced for fields.Many2many

**ondelete** options will not work with Many2many fields, so in order to implement this restriction we must redefine unlink function:

```python
@api.one
def unlink(self):
    related_model = self.env['module.related']
    if related_model.search([('this_model_field_ids', 'in', self.ids)]):
        raise Warning(_(
            "You are trying to delete a record that is still referenced!"))
    return super(Model, self).unlink()
```
