# Odoo

<em>This document is a work in progress</em>

Odoo is an open source ERP available in a selfhosted or cloud hosted option. Please also see [https://www.odoo.com/](https://www.odoo.com)

To configure an Odoo intance you need 4 things
* Odoo version number
* Database name (case sensitive)
* Username
* Password

## Setup steps

* Login on the application
* Navigate to data sources
* On the right > Select Odoo > Add
* Click the configure button
* On the first tab, enter the Database name, Username and password
* On the second tab (BOM Configuration) enter the version number (Only version 17 supported at the time of writing, but contact us if you require access to older version)
* Click the `Save` button
* Click the `Authenticate` button

![Configure Odoo](odoo-config-values.png "Register new Organization")
 

## Limitations at the time of writing

SharpSync supports (but we can add upon request)
* Odoo version 17


SharpSync requires the MRP module (mrp) at a minimum in order to support an Odoo integration.
This is because BOM information, more specifically the Quantities of individual items.

Routings are not currently supported but we are working towards it
