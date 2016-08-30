# Development

## Using nodemon to auto restart Odoo server

Install **nodemon** node package:

```
npm install -g nodemon
```

Run **nodemon** watching for changes on an addon:

```
nodemon --watch <addon_path> -e py,xml --exec "odoo.py -c odoo-9.conf -u <addon>"
```

## Docker container for Odoo database

```
docker run --detach -e POSTGRES_USER=odoo -e POSTGRES_PASSWORD=odoo --name odoo_db --publish=5432:5432 --restart=always postgres:9.4
```
