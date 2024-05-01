# Autodesk Inventor Setup

CSV (Comma Separated Values) files are utilized to import Bills of Materials (BOMs) from desktop-based CAD software such as Solidworks or Inventor into SharpSync. Follow the steps below to begin importing data into SharpSync using CSV files.

## Prerequisites
* Download and install the Autodesk Inventor Addin from the `Downloads` section
* Install the addin

## Instructions

### Setup the CSV datasource

* From the `Datasources` section, add the CSV datasource as the Primary datasource
* Click the `Configure` button > `BOM Configuration`
* On a new line each, enter the Custom Properties to read, the current built-in properties in Autodesk Inventor 2025 in the `Design Tracking Properties` Property Set are:
  * Appearance
  * Authority
  * Catalog Web Link
  * Categories
  * Checked By
  * Cost
  * Cost Center
  * Creation Time
  * Date Checked
  * Defer Updates
  * Density
  * Description
  * Design Status
  * Designer
  * Document SubType
  * Document SubType Name
  * Engineer
  * Engr Approved By
  * Engr Date Approved
  * External Property Revision Id
  * Flat Pattern Area
  * Flat Pattern Defer Update
  * Flat Pattern Length
  * Flat Pattern Width
  * Language
  * Last Updated With
  * Manufacturer
  * Mass
  * Material
  * Material Identifier
  * Mfg Approved By
  * Mfg Date Approved
  * Parameterized Template
  * Part Icon
  * Part Number
  * Part Property Revision Id
  * Project
  * Proxy Refresh Date
  * Sheet Metal Area
  * Sheet Metal Length
  * Sheet Metal Rule
  * Sheet Metal Width
  * Size Designation
  * Standard
  * Standard Revision
  * Standards Organization
  * Stock Number
  * SurfaceArea
  * Template Row
  * User Status
  * Valid MassProps
  * Vendor
  * Volume
  * Weld Material
* Each value entered here will be available as an Accessor in the `Property Mappings` tab
* Make sure to add an extra line with the `Quantity` property which is not an Inventor property but will be used later in the property mappings configuration.
* Click the `Save` button

* On the main datasource tab, make sure that the `Primary Identifier` matches with the `Part Number` Inventor property or any other Inventor property that you use as unique component identifier. The primary component identifier is the identifier that is unique across datasources.

### Setup the Property Mappings

You can follow the instructions in the following link to setup your property mappings
* [Property mappings: Setup](../../../propertymapping/readme.md)
* Make sure you add the property `Quantity` as a property mapping and check its `Quantity Property` checkbox in the Property Mappings Settings panel.

### Configure the Addin

After installing the Autodesk Inventor addin, you'll need to configure how it will generate BOMs.

* Click on the `SharpSync` ribbon tab
* Click on the `Login` button
* Enter your SharpSync username & pwd then click on the `Login` button
* If successful, the window will close
* Click on the `Settings` button
* If the login succeed you should see the `Primary Component Identifier` & `Secondary Component Identifier` listed
* Once your Inventor assembly is ready, click on the `Export Bom` button which will automatically export the Bom to SharpSync by opening a new web browser page
* The addin supports exporting any Inventor Assembly `Model State`, make sure that the appropriate `Model State' is active before clicking on the `Export Bom` button 
