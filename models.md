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

## Redefining name_search() function (on API v8)

```python
@api.model
def name_search(self, name, args=None, operator='ilike', limit=100):
    # For example, to change the domain in search
    args.extend([('field','=',True)])
    return super(Model, self).name_search(
        name=name,
        args=args,
        operator=operator,
        limit=limit)
```

## Set current user as default

```python
user_id = fields.Many2one(
    comodel_name='res.users',
    default=lambda self: self.env.user
)
```
