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

##  Translation of terms of base modules does not work

To modify the translation of a base module, export the translation as usual and translate the terms. Then update the module:

    odoo.py -u module

Go to Settings > Translations > Load a Translation, select your language and check the box 'Overwrite Existing Terms', then click on 'Load' button.

After that, press F5 to refresh the browser, then go to Settings > Translations > Application Terms > Synchronize Terms, select your language and click on 'Update'. Then press again F5 to see if your terms have been updated.

In your custom module (which modifies the base translation) edit the **__openerp__.py** and add:

    'sequence': 150
