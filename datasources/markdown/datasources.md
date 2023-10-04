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

 
|Name|Type|Status|Documentation|
|---|---|---|----|
|CSV|Static / offline|[done]|[Documentation](../csv/markdown/csv-setup.md)|
|NetSuite|ERP|[done]|[Documentation](../netsuite/markdown/netsuite-setup.md)|
|Onshape|CAD|[done]|Documentation (coming soon)|
|SOLIDWORKS|CAD|[In progress]|Documentation (coming soon)|
|SOLIDWORKS|PDM|[In progress]|Documentation (coming soon)|
   
