# Testing

## Run server with nodemon

```
nodemon --watch <addon_path> -e py,xml --exec "odoo.py -c odoo-9.conf --test-enable --log-level=test --log-handler=:ERROR -u <addon>"
```

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
