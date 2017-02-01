# Testing

## Models and decorators

```python
# -*- coding: utf-8 -*-

from openerp.tests import common


@common.at_install(False)
@common.post_install(True)
class TestModel(common.TransactionCase):

    def test_create(self):
        Models = self.env['module.model']
        vals = {}
        model = Models.create(vals)
```

## Run server with tests enabled

```
odoo.py -c odoo.conf --test-enable --log-level=test --log-handler=:ERROR -u <addon>
```
