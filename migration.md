# Migration

## Migrate module to v10

> Odoo version 10 or later

- Bump module version to "10.0.1.0.0"
- Migrate code to new ORM API if not yet.
- Replace `openerp` imports to `odoo`. You can use this command:

  ```bash
  find . -type f -name '*.py' | xargs sed -i 's/from openerp/from odoo/g'
  ```

- Rename `__openerp__.py` to `__manifest__.py` if not yet renamed.

- Update README.rst from <https://raw.githubusercontent.com/OCA/maintainer-tools/master/template/module/README.rst> if not updated to the latest template.

- Add tests to increase code coverage.

- Update code to remove use of deprecated methods.

- Update code to take advantage of the new features.

- Replace `select = True` by `index = True`

- Replace string selectors in XML by name (if possible) or other attribute selector or even another equivalent path/reference. For example, change `<group string="x" position="after">` by `<group name="x" position="after">`

- Remove `<data>` and `</data>` in xml files if `noupdate="0"`

- Replace the `<openerp>`/`</openerp>` tags in xml files by `<odoo>`/`</odoo>`.

- Don't use `@api.one` with `@api.onchange` or it will crash.

- `base.group_configuration` has been renamed to `base.group_system`

- Change decorator of copy method `def copy(self):` from `@api.one` to `@api.multi`

- Do the changes you need to do for making the module works on new version.

## Use OpenUpgrade to migrate database between Odoo versions

```
git clone git@github.com:OCA/OpenUpgrade.git
virtualenv open-upgrade
pip install -r requirements.txt
pip install vobject --upgrade
```

Modify odoo configuration file to set `db_port` value:

```
db_port = 5432
```

Run migrator script:

> Odoo version 8 or 9

```
wget https://raw.githubusercontent.com/OCA/OpenUpgrade/HEAD/scripts/migrate.py
python migrate.py --config=odoo-8.conf --database=<database-odoo-8> --run-migrations=9.0 --branch-dir=/tmp/open-upgrade
```

> Odoo version 10 or later

```
wget https://raw.githubusercontent.com/OCA/OpenUpgrade/10.0/scripts/migrate.py
python migrate.py --config=odoo-9.conf --database=<database-odoo-9> --run-migrations=10.0 --branch-dir=/tmp/open-upgrade
```
