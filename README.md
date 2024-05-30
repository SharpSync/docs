# SharpSync
 
## What is SharpSync?

SharpSync is a cloud based data synchronization application:
* Easy to use
* Intuitive
* Let's you moves data
  * From CAD => ERP or
  * From PDM => ERP or
  * PLM => ERP
* It does this by identifying differences in meta data (or custom properties) and the BOM structure between the 2 systems
* It then let's the user submit and write back the changes to the ERP, PDM or PLM system.


##  What value does it provide?

SharpSync has an incredibly powerful rules engine that let's you, as the user, specify rules to massage your data when the data is imported, exported or displayed on screen.

These rules are setup for all data imports for the entire organization and all your users will draw the benefit of having a unified rule set for your data.

Typically companies would employ a full time data entry person to manage the data between the 2 systems. This is an extremely time consuming and error prone process. Sharpsync automates this process and allows the user to focus on more value added tasks. We believe our product is well priced and provides great value for the price compared to traditional desktop solutions.
  
Important concepts:

* [Getting started](getting_started.md)
* [Datasources](datasources/readme.md)
* [Property mappings: Setup](propertymapping/readme.md)
* [Property mappings: Rules](propertymapping/markdown/rules.md)
* [Subscriptions](subscriptions.md)

## Resource links
Select an individual datasource to view the configuration setup for that source.

 
|Name|Type|Sync|Status|Documentation|
|---|---|---|----|----|
|CSV|Static / offline|single direction|:white_check_mark:|[Documentation](datasources/csv/markdown/csv-setup.md)|
|Inventor|CAD|single-directional|:white_check_mark:|[Documentation](datasources/inventor/markdown/readme.md)|
|MS Dynamics|ERP|bi-directional|[In progress]|[Documentation](datasources/ms-dynamics/readme.md)|
|NetSuite|ERP|bi-directional|:white_check_mark:|[Documentation](datasources/netsuite/readme.md)|
|Odoo|ERP|bi-directional|:white_check_mark:|[Documentation](datasources/odoo/readme.md)|
|Onshape|CAD|bi-directional|:white_check_mark:|[Documentation](datasources/onshape/markdown/onshape-setup.md)|
|SOLIDWORKS|PDM|bi-directional|:white_check_mark:|[Documentation](datasources/swpdm/markdown/swxpdm-setup.md)|
|SOLIDWORKS|CAD|single-directional|:white_check_mark:|[Documentation](datasources/swx/readme.md)|

   
See also [Troubleshooting](troubleshooting_datasources.md)
