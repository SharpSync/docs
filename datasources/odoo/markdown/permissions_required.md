# List of permissions required on models

The Odoo module integration requires the following permission to correctly read + update Bill of Material (BOM) information:


|Model name|Read|Write|Create|Delete|
|---|---|---|---|---|
|ir.model|:white_check_mark:|||
|ir.model.fields|:white_check_mark:|||
|ir.model.access|:white_check_mark:|||
|ir.model.fields.selection|:white_check_mark:|||
|ir.ui.view|:white_check_mark:|||
|mrp.bom|:white_check_mark:|:white_check_mark:|:white_check_mark:||
|mrp.bom.line||:white_check_mark:|:white_check_mark:|:white_check_mark:|:white_check_mark:|
|product.product|:white_check_mark:|:white_check_mark:|:white_check_mark:||
|product.template|:white_check_mark:|:white_check_mark:|:white_check_mark:||
|product.template.attribute.line|:white_check_mark:|:white_check_mark:|:white_check_mark:||

