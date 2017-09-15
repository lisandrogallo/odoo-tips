# Development

## Using nodemon to auto restart Odoo server

Install **nodemon** node package:

```
npm install -g nodemon
```

Run **nodemon** watching for changes on an addon:

> Odoo version 8 or 9

```
nodemon --watch <addon_path> -e py,xml --exec "odoo.py -c odoo.conf -u <addon>"
```

> Odoo version 10 or later

```
nodemon --watch <addon_path> -e py,xml --exec "./odoo-bin -c ../odoo-10.conf -u <addon>"
```

## Docker container for Odoo database

```
docker run --detach -e POSTGRES_USER=odoo -e POSTGRES_PASSWORD=odoo --name odoo_db --publish=5432:5432 --restart=always postgres:9.4
```

## Using Pylint Odoo plugin

Custom checks for Odoo modules: <https://github.com/oca/pylint-odoo>

Install plugin:

```
pip install --upgrade git+https://github.com/oca/pylint-odoo.git
```

Run tests:

```
pylint --load-plugins=pylint_odoo -d all -e odoolint {ADDONS-PATH}
```
