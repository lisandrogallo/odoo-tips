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
