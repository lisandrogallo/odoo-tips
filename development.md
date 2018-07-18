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

Listen uses inotify by default on Linux to monitor directories for changes. If you get an error like `OSError: inotify watch limit reached` you must set a new watch limit.

You can get your current inotify file watch limit by executing:

    cat /proc/sys/fs/inotify/max_user_watches

To make a new limit permanent:

    echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf
    sudo sysctl -p

```
./odoo-bin -c ../odoo-10.conf --dev=all
```

## Docker container for Odoo database

```
docker run --detach -e POSTGRES_USER=odoo -e POSTGRES_PASSWORD=odoo --name odoo_db --publish=5432:5432 --restart=always postgres:latest
```

## Pylint Odoo plugin to enable custom checks for modules

Custom checks for Odoo modules: <https://github.com/oca/pylint-odoo>

Install plugin:

```
pip install --upgrade git+https://github.com/oca/pylint-odoo.git
```

Run tests:

```
pylint --load-plugins=pylint_odoo -d all -e odoolint {ADDONS-PATH}
```
