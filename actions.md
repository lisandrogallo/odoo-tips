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
