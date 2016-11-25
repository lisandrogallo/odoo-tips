# Environment

## Get base URL

```
self.env['ir.config_parameter'].get_param('web.base.url')
```

## Get object id from XML external id

```
obj = self.env.ref('module_name.xml_external_id')
```
