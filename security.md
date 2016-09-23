# Security

## Views

### Modify field attributes based on group

```xml
<record id="module.model_form_view_modified" model="ir.ui.view">
    <field name="name">module.model.form.modified</field>
    <field name="model">module.model</field>
    <field name="inherit_id" ref="module.module_model_form_view"/>
    <field name="groups_id" eval="[(6, 0, [ref('module.group_manager')])]"/>
    <field name="arch" type="xml">
        <field name="field1" position="attributes">
            <attribute name="attrs">{'readonly': False}</attribute>
        </field>
        <field name="field2" position="attributes">
            <attribute name="attrs">{'readonly': True}</attribute>
        </field>
        <field name="field3" position="attributes">
            <attribute name="attrs">{'invisible': True}</attribute>
        </field>
    </field>
</record>
```

### Hide definitely menus and elements

Create a group with no members:

```xml
<record id="make_invisible" model="res.groups">
    <field name="name">Invisible</field>
</record>
```

Hiding a menu item:

```xml
<!-- HIDE CONTACTS -->
<record model="ir.ui.menu" id="base.menu_base_partner">
    <field name="groups_id" eval="[(6,0,[ref('make_invisible')])]"/>
</record>
```

Hiding a web element from a template:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<openerp>
    <data>
        <!-- HIDE SYSTRAY -->
        <template id="web.menu_custom"
            inherit_id="web.menu">
            <xpath expr="//ul[@class='nav navbar-nav navbar-right oe_systray']" position="attributes">
                <attribute name="groups">module.group_invisible</attribute>
            </xpath>
        </template>
    </data>
</openerp>
```
