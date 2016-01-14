# Troubleshooting

## Imported objects are deleted after module update

If you get a message like this after module update:

```text
openerp.addons.base.ir.ir_model: Deleting 31932@module.model
openerp.addons.base.ir.ir_model: Deleting 31933@module.model
openerp.addons.base.ir.ir_model: Deleting 31934@module.model
...
```

This happens if you chooses an external id that is part of another model by using the period (e.g. 'product.external_id'). To solve this issue, find the external id in the Postgres table **ir_model_data** and delete it, or choose another external id format.
