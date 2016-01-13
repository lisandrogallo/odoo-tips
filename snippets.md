# Code Snippets

## Create a new object

```python

vals = {
    'field': self.field,
    'field_id': self.field_id.id,
    'field_ids': [(6, 0, self.field_ids.ids)]
}

obj_model = self.env['module.model']
obj = obj_model.create(vals)
```
