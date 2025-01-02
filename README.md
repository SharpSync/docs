[![SharpSync Intro video](https://sharpsync.net/wp-content/uploads/2024/01/SharpSync_Home_Banner-1200x313.png)](https://sharpsync.net/wp-content/uploads/2024/06/SharpSync-Promo-1.mp4)
# SharpSync
 
 ## Resource links
Select an individual datasource to view the configuration setup for that source.

 
|Name|Type|Sync|Status|Documentation|
|---|---|---|----|----|
|CSV|Static / offline|single direction|:white_check_mark:|[Documentation](datasources/csv/markdown/csv-setup.md)|
|Inventor|CAD|single-directional|:white_check_mark:|[Documentation](datasources/inventor/markdown/readme.md)|
|MS Dynamics|ERP|bi-directional|[In progress]|[Documentation](datasources/ms-dynamics/readme.md)|
|NetSuite|ERP|bi-directional|:white_check_mark:|[Documentation](https://sharpsync.gitbook.io/sharpsync/data-sources/netsuite)|
|Odoo|ERP|bi-directional|:white_check_mark:|[Documentation](https://sharpsync.gitbook.io/sharpsync/data-sources/odoo)|
|Onshape|CAD|bi-directional|:white_check_mark:|[Documentation](https://sharpsync.gitbook.io/sharpsync/data-sources/onshape)|
|PropelPLM|ERP/PLM|bi-directional|:white_check_mark:|[Documentation](datasources/propel/readme.md)|
|SOLIDWORKS|PDM|bi-directional|:white_check_mark:|[Documentation](https://sharpsync.gitbook.io/sharpsync/data-sources/solidworks-pdm)|
|SOLIDWORKS|CAD|single-directional|:white_check_mark:|[Documentation](datasources/swx/readme.md)|

   
See also [Troubleshooting](datasources/troubleshooting_datasources.md)

 Important concepts:
 
* [What is SharpSync](#what-is-sharpsync)
* [Getting started](getting_started.md)
* [Datasources](datasources/readme.md)
* [Property mappings: Setup](propertymapping/readme.md)
* [Property mappings: Rules](propertymapping/markdown/rules.md)
* [Derivatives](derivatives/readme.md)
* [Subscriptions](subscriptions.md)


## What is SharpSync?

SharpSync is a cloud based data synchronization application in the CAD <> ERP space. 
CAD Systems (such as SolidWorks, SolidEdge, Inventor, Onshape) has lots of data that needs to move to ERP systems (such as Netsuite, Dynamics365, Odoo). This data includes things like BOM data, inventory detail, thumbnails, and revision information.
This synchronization space, although it's been around for a many years, leaves much to be desired as the main competitors are desktop based, and any changes to their apps requires manual updates on user machines by the developers, or copying and pasting settings between machine.
This means everytime there is a change, you're billed for something you should be able to do yourself.

To that end, the main goals of the application are:

* Easy to use.  
* Intuitive. 
* Web based - no manual updates!
* To let you move data:
  * From CAD => ERP => CAD or
  * From PDM => ERP => PDM or
  * From PLM => ERP => PLM
* It does this by identifying differences in meta data (or custom properties) and the BOM structure between the 2 systems
* Displays this data in an easy to digest format onscreen.
* Reporting on BOMs submitted. Users must be able to troubleshoot problems with their own data
* It then let's the user submit and write back the changes to the CAD, ERP, PDM or PLM system.

[Marketing video](https://sharpsync.net/wp-content/uploads/2024/06/SharpSync-Promo-1.mp4) here

##  What value does it provide?

Typically companies would employ a full time data entry person to manage the data between the 2 systems. This is an extremely time consuming and error prone process. Sharpsync automates this process and allows the user to focus on more value added tasks. We believe our product is well priced and provides great value for the price compared to traditional desktop solutions.

SharpSync was designed from the ground up to be used by users of the application, not to be silo'ed to the halls of developers. 
It has an very powerful rules engine that let's you, as the user, specify rules to massage your data when the data is imported, exported or displayed on screen.
This reduces the amount of time spent agonizing over individuals rows in BOMs.

These rules are setup for data sources for the entire organization and all your users will draw the benefit of having a unified rule set for your data. That means: 
* No need to copy + paste data from CAD => ERP.
* No need to employ someone to do said copying + pasting.
* No need to export + import settings across machines.
* Intuitive: You should be able to map your own mappings. Not pay a developer to do it.
  


