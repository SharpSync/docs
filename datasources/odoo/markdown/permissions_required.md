# List of permissions required on models

The Odoo module integration requires the following permission to correctly read + update Bill of Material (BOM) information:

(Please check this regularly during setup as we may adjust this list according to new modules added)

|Model name|Read|Write|Create|Delete|
|---|---|---|---|---|
|ir.model.access|:white_check_mark:|||
|ir.model|:white_check_mark:|||
|ir.model.fields|:white_check_mark:|||
|ir.model.fields.selection|:white_check_mark:|||
|ir.model.fields.selection|:white_check_mark:|||
|ir.rule|:white_check_mark:|||
|ir.ui.view|:white_check_mark:|||
|mrp.bom|:white_check_mark:|:white_check_mark:|:white_check_mark:||
|mrp.bom.line|:white_check_mark:|:white_check_mark:|:white_check_mark:|:white_check_mark:|:white_check_mark:|
|product.category|:white_check_mark:|:white_check_mark:|:white_check_mark:||
|product.product|:white_check_mark:|:white_check_mark:|:white_check_mark:||
|product.template|:white_check_mark:|:white_check_mark:|:white_check_mark:||
|product.template.attribute.line|:white_check_mark:|:white_check_mark:|:white_check_mark:||
|product.template.attribute.value|:white_check_mark:|:white_check_mark:|:white_check_mark:||
|report.mrp.report_bom_structure|:white_check_mark:|||

Navigate to:
 - [Odoo source datasource](../readme.md)
 - [Property mappings](../../../propertymapping/readme.md)
 - [Home](../../../README.md)