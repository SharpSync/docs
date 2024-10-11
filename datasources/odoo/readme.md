# Odoo

<em>This document is a work in progress</em>

## Limitations at the time of writing

SharpSync supports 
* Odoo version 17
* Odoo version 16 (in progress)
Should you require access to a different version please make contact with us at [SharpSync](https://sharpsync.net/about/)


Odoo is an open source ERP available in a selfhosted or cloud hosted option. Please also see [https://www.odoo.com/](https://www.odoo.com) and [hosting options](markdown/hosting-options.md)

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
 
## Property mappings
After successfully authenticating with Odoo, navigate to the [property mappings](propertymapping/markdown/readme.md)
The update should automatically trigger. If it does not, click the *Update* button

The custom fields from Odoo has now succesfully been pulled into SharpSync.

<span style='color:orange'>Take note!:</span> If you ever add new properties to Odoo, make sure to come back to the property mapping page and click the *Update* button again.
 

SharpSync requires the MRP module (mrp) at a minimum in order to support an Odoo integration.
This is because BOM information, more specifically the Quantities of individual items.

Routings are not currently supported but we are working towards it

## Extra information

Please see  [hosting options](markdown/hosting-options.md)