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

_Tip: To check if it works you can group or filter data using context values passed to a window action._

## Translation of terms of base modules does not work

To modify the translation of a base module, export the translation as usual and translate the terms. Then update the module:

```
odoo.py -u module
```

Go to Settings > Translations > Load a Translation, select your language and check the box 'Overwrite Existing Terms', then click on 'Load' button.

After that, press F5 to refresh the browser, then go to Settings > Translations > Application Terms > Synchronize Terms, select your language and click on 'Update'. Then press again F5 to see if your terms have been updated.

In your custom module (which modifies the base translation) edit the `__openerp__.py`and add:

```
'sequence': 150
```

## Errors restoring database from dump

Errors:

```python
raise Exception('Command `%s` not found.' % name)
Exception: Command `pg_restore` not found.
```

```python
raise Exception('Postgres subprocess %s error %s' % (args2, rc))
Exception: Postgres subprocess ('/usr/bin/pg_restore', '--username=odoo', '--host=localhost', u'--dbname=dbname', '--no-owner', '/tmp/tmpxTpUyL') error 1
```

Solution:

Install the _pg_restore_ version that fits the PostgresSQL version used to dump the database:

```
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ xenial-pgdg main" >> /etc/apt/sources.list.d/postgresql.list'

apt update
apt install postgres-client-9.3
```

## Error creating a new database

> Odoo version 10

Error:
```
ProgrammingError: column res_lang.active does not exist
LINE 1: SELECT count(1) FROM "res_lang" WHERE ("res_lang"."active" =...
```

Solution:

Check if there is any addon with an empty **\__manifest__.py** file and complete it.

## Database backup with 0 bytes size

Error:

You are getting a 0 bytes size dump or having the following error:

```
Exception: Postgres subprocess ('/usr/bin/pg_dump', '--no-owner', '--file=/tmp/tmpVtzIfN/dump.sql', u'database') error 1
```

Solution:

`pg_dump` command version mismatch Postgres version running on server. Install the appropriate `postgres-client-9*` version.

## Database restore error: Command `psql` not found

Install `postgresql-client` package.

## 'Invalid view definition' migrating modules

> Odoo version 9 or later

Error:

```python
ParseError: "Invalid view definition

Error details:
View inheritance may not use attribute 'string' as a selector.
```

Solution:

Now in Odoo 9 using _string_ as selector in XPATH is not allowed. Instead of this you can use _id_ or _name_:

```
<page name="page" position="replace"/>
```

or

```
<xpath expr="//group" position="after">
```

or

```
<xpath expr="/FULL_XML_TREE/group" position="after">
```

## 'Sender address rejected' when sending mail from Odoo

Error:

```
(504, '5.5.2 <postmaster-odoo@localhost>: Sender address rejected: need fully-qualified address')
```

Solution:

Remove all catchall parameters (_mail.catchall.domain_ and _mail.catchall.alias_) under _"Settings" > "Technical" > "Parameters" > "System Parameters"_ does the trick.

## "unknown comodel_name 'module.model'"

Solution:

In `__openerp.py__` add the 'module' string in the 'depend' list.

## 'http' Python module ImportError with some base modules

Error:
```
File "/opt/odoo/server/addons/board/__init__.py", line 24, in <module>
File "/opt/odoo/server/addons/board/controllers/__init__.py", line 4, in <module>
File "/opt/odoo/server/addons/board/controllers/main.py", line 6, in <module>

ImportError: No module named http
```

Solution:

Go to the module directory and remove .pyc files like **__init__.pyc** and/or **main.pyc**

## Installation

### Could not execute command 'lessc' error

> Odoo version 9 or later

```
apt install nodejs-legacy
sudo npm install -g less
sudo npm install -g less-plugin-clean-css
```

### Password authentication failed for user 'postgres' using pgAdmin

Need to set a password to 'postgres' user:

```
sudo -u postgres psql postgres
alter user postgres with password 'postgres';
```