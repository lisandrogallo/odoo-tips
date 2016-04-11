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
