# SolidWorks Addin Setup

SWX  files are utilized to import Bills of Materials (BOMs) from desktop-based CAD software into SharpSync. Follow the steps below to begin importing data into SharpSync using CSV files.


* [Prerequisites](#prerequisites)
* [Setup Instructions](#setup-instructions) 
* [Push a Bill of Materials to SharpSync](#push-a-bill-of-materials-to-sharpsync)

## Prerequisites

* An installation of Solidworks 2023/4 or later (engage us for older versions)
* Download and install the SOLIDWORKS Addin from the `Downloads` section
* Installation of the addin
* An assembly or part file
* Drawings Bill of Materials are not supported yet, but talk to us about integration
  
## Setup Instructions

### Setup the CSV datasource in SharpSync

* From the `Datasources` section, add the CSV datasource as the Primary datasource
* Click the `Configure` button > `BOM Configuration`
* On a new line each, enter the Custom Properties to read
* These properties should be the standard properties that exist in any given SolidWorks file. If it does not exist, a blank value will be used
* Properties are read from the `Configuration` tab first, then the `Custom` tab
* Each value entered here will be available as an `Accessor` (Property) in the `Property Mappings` tab
* Make sure to add the Quantity / Qty / qty. column (this will be used later in the property mappings).
  (The exact naming is not important, as long as it reflects the quantity of parts in an assembly)

> For example if you want to display custom properties `Number`, `Description`, `Material`, then enter these on a new line each

* Click the `Save` button
* On the main datasource tab, make sure that the `Primary Component Identifier` matches with your `Number` custom property.

The primary component identifier is the identifier that is unique across data source domains. If this is `Number` or `No` or `PartNumber` then the assumption is this property exists in both SolidWorks and your ERP solution.
(NOTE: It does not have to be called `Number`. It can be called anything as long as it exists as a SolidWorks custom property. If it does not exist, the file name will be used as the fallback value)

### Configure the Addin

After installing the SOLIDWORKS addin, you'll need to configure how it will generate BOMs. Make sure your Solidworks files have the required properties. (Flattened BOMs are not supported)

* Click Tools > SharpSync > Login
* Enter your SharpSync username / pwd > Click Login
* If successful, the window will close
* Click Tools > SharpSync > Settings
* Click the radio button to use `Custom Property`
* If the login succeed you should see the `Primary Component Identifier` listed
* This is the preferred method of working with the BOM  

## Push a Bill of Materials to SharpSync
  
Pushing data from SolidWorks to SharpSync is easy and straight forward. To push a Bill of Materials (BOM) to SharpSync do the following:
  
* Open a part or assembly file
* Make sure you've logged in to SharpSync (Click the login button at least once)
* Click the Push BOM button

