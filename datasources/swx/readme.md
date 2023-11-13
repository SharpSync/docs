# SWX Setup

SWX  files are utilized to import Bills of Materials (BOMs) from desktop-based CAD software into SharpSync. Follow the steps below to begin importing data into SharpSync using CSV files.

## Prerequisites
* Download and install the SOLIDWORKS Addin from the Downloads section
* Install the addin

  
## Instructions

### Setup the CSV datasource

* From the `Datasources` section, add the CSV datasource as the Primary datasource
* Click the `Configure` button > `BOM Configuration`
* On a new line each, enter the Custom Properties to read
* Each value entered here will be available as an Accessor in the `Property Mappings` tab
* Make sure to add the Quantity / Qty / qty. column (this will be used later in the property mappings)

> For example if you want to display custom properties `Number`, `Description`, `Material`, then enter these on a new line each

* Click the `Save` button
* On the main datasource tab, make sure that the `Primary Component Identifier` matches with your `Number` custom property.

The primary component identifier is the identifier that is unique across datasources. If this is `Number` or `No` or `PartNumber` then this should be the first in both the `BOM Columns`
* It does not have to be called `Number`. It can be called anything as long as it is in the BOM columns list and used as a `Primary Component Identifier`

### Configure the Addin

After installing the SOLIDWORKS addin, you'll need to configure how it will generate BOMs. Make sure your Solidworks files have the required properties. (Flattened BOMs are not supported)

* Click Tools > SharpSync > Login
* Enter your SharpSync username / pwd > Click Login
* If successful, the window will close
* Click Tools > SharpSync > Settings
* Click the radio button to use `Custom Property`
* If the login succeed you should see the `Primary Component Identifier` listed
* This is the preferred method of working with the BOM  

  
