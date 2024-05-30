# Datasources

A datasource is exactly that - a source of data that you configure to read/write data from, or a source of data with an add-in to push data ➡️ SharpSync. Each source may be registered as either a _primary_ or a _secondary_ datasource.

It works as follows:

_primary datasource_ ↔️ SharpSync ↔️ _secondary datasource_

## Core concepts
* A _primary_ datasource is typically a CAD / PDM / PLM source. It is the origin of your CAD data.
* A _secondary_ datasource is typically an ERP / MRP source.
* SharpSync uses both sources to do bi-directional synchronization, meaning it pulls information from the _primary_ and writes to the _secondary_. It can also pull information from the _secondary_ and write to the _primary_.
* Currently the application is limited to a single _primary_ source and a single _secondary_ source

## Resource links
Select an individual datasource to view the configuration setup for that source.

 
|Name|Type|Sync|Status|Documentation|
|---|---|---|----|----|
|CSV|Static / offline|single direction|:white_check_mark:|[Documentation](csv/markdown/csv-setup.md)|
|NetSuite|ERP|bi-directional|:white_check_mark:|[Documentation](netsuite/readme.md)|
|Odoo|ERP|bi-directional|:white_check_mark:|[Documentation](odoo/readme.md)|
|Onshape|CAD|bi-directional|:white_check_mark:|[Documentation](onshape/markdown/onshape-setup.md)|
|SOLIDWORKS|PDM|bi-directional|:white_check_mark:|[Documentation](swpdm/markdown/swxpdm-setup.md)|
|SOLIDWORKS|CAD|single-directional|:white_check_mark:|[Documentation](swx/readme.md)|
|Inventor|CAD|single-directional|:white_check_mark:|[Documentation](inventor/markdown/readme.md)|
|MS Dynamics|ERP|bi-directional|[In progress]|[Documentation](ms-dynamics/readme.md)|

   
See also [Troubleshooting](troubleshooting_datasources.md)
