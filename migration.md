# Migration

# Use OpenUpgrade to migrate database between Odoo versions

    git clone git@github.com:OCA/OpenUpgrade.git
    virtualenv open-upgrade
    pip install -r requirements.txt
    pip install vobject --upgrade

Modify odoo configuration file to set db_port value:

    db_port = 5432

Run migrator script:

    wget https://raw.githubusercontent.com/OCA/OpenUpgrade/HEAD/scripts/migrate.py
    python migrate.py --config=odoo-8.conf --database=<database> --run-migrations=8.0,9.0 --branch-dir=/tmp/open-upgrade
