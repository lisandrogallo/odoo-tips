# Database

## Search without accented characters

Install unaccent on Postgresql 9.1+:

    sudo apt-get install postgresql-contrib-9.1

Install unaccent using the new CREATE EXTENSION command:

    psql <database> -c "CREATE EXTENSION \"unaccent\"";

Add the option on the Odoo configuration file (*odoo.conf*)

    unaccent = True
