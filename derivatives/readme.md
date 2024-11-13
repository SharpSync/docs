# Derivatives

<details open>
<summary>Table of Contents</summary>
<blockquote>

[Adding Derivative Types](#adding-derivative-types)  
[Configure Derivative Types](#configure-derivative-types)  
</blockquote>
</details>

## Derivatives

!["Derivatives"](images/Derivatives.png)

### Overview

Derivatives are files or URLs that are derived from BOMs and Components in the CAD source, such as STEP, DWG, PDF, etc... files.
SharpSync's derivatives feature allows the manual or automated transfer of CAD BOM derivatives from the CAD Source to the ERP source.
The derivatives feature is currently only available for:
* CAD
  * Onshape
* ERP
  * Propel PLM

## Instructions

### Adding Derivative Types

1. First, make sure you have loaded all available derivatives from your source by clicking on the update source derivatives types button.
![Alt text](images/Derivatives1.png "Update Derivatives Types")
2. Second, click on the `DERIVATIVE TEMPLATE NAME` input to list the available derivative types to select from, then select a derivative type, andfinally click on the `ADD DERIVATIVE` button to add the derivative type.
![Alt text](images/Derivatives2.png "Add Derivative Type")
3. After adding all the desired derivative types, you can now start to configure their settings

### Configure Derivative Types

1. You can double click on the `PATTERN` cell of each derivative type to change the file naming pattern of the derivative that will be transfered to your ERP source.
![Alt text](images/Derivatives3.png "Configure Derivative Type Naming Pattern")
2. You can check/uncheck the `GENERATE FOR ASSEMBLIES` or the `GENERATE FOR COMPONENTS` checkbox of a derivative type to control which derivatives can be generated for which BOM component type (assemblies or components). For example, if the "STEP" derivative type is checked for assemblies, then the "STEP" derivative can be generated for any assembly row of your loaded BOM.
![Alt text](images/Derivatives4.png "Configure Derivative Type Generate For")
3. 

### Auto Generate Default Derivatives

