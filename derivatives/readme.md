# Derivatives

<details open>
<summary>Table of Contents</summary>
<blockquote>

[Adding Derivative Types](#adding-derivative-types)  
[Configure Derivative Types](#configure-derivative-types)  
[Auto Generate Default Derivatives](#auto-generate-default-derivatives)  
[Configure BOM Row Derivatives](#configure-bom-row-derivatives)  
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
2. Second, click on the `DERIVATIVE TEMPLATE NAME` input to list the available derivative types to select from, then select a derivative type, and finally click on the `ADD DERIVATIVE` button to add the derivative type.
![Alt text](images/Derivatives2.png "Add Derivative Type")
3. After adding all the desired derivative types, you can now start to configure their settings

### Configure Derivative Types

There are different types of mappings for derivatives:

* Model geometry for assemblies (e.g. STEP, IGES)
* Model geometry for components (e.g. STEP, IGES)
* Drawing derivative (e.g. DRAWING) (search patterns) (e.g. first find DRAWING matching the pattern DRW-{componentName})
* Drawing derivatives (e.g. PDF / DXF / DWG) based on the found DRAWING

For each type of mapping you can select one or more (depending on the type) of option:

* Transfer URL: creates a copy of the URL value int the selected property mapping <sup>**</sup>
* Transfer File: creates a copy of the file in the destination ERP

<sup>**</sup>*Not available for **offline sources** at the time of writing*

It is important to note the following logic:

<span style='color:orange'>[Work in progress - can change]</span>

* When mapping assembly derivatives [checkbox `FOR ASSEMBLIES`] (e.g. STEP, IGES):
  * The derivative is *always* generated based on the version + configuration provided for the component.
  * The derivative is searched for (opt-in) (Not Yet Implemented)
* When mapping component derivatives [checkbox `FOR COMPONENTS`] (e.g. STEP, IGES):
  * The derivative is *always* generated based on the version + configuration provided for the component.
  * The derivative is searched for (opt-in) (Not Yet Implemented)
* When mapping the DRAWING derivative [checkbox `FOR DRAWINGS`] (e.g. SLDDRW / ONSHAPE DRAWING documents):
  * No new drawings will be generated in the source.
  * A new DRAWING BOM Row will be created in the BOM view in SharpSync as child of each item (assemblies + parts) during the BOM loading process, only if a corresponding DRAWING is found in the source matching the defined file pattern exactly (the search will be based on the DRAWING derivative template file pattern and the metadata of the parent item. e.g.: If the parent item part name is P1-PN The pattern DRW-{componentName} will search for a source DRAWING exactly named DRW-P1-PN).
  * This created row will be read only and will not be included as part of bom submission, instead it will act as a placeholder for possible drawing derivatives (DRAWING, PDF, DWG, etc...).
  * The DRAWING row derivative can be configured in the DERIVATIVES menu but can only be added to a DRAWING BOM Row.
  * When processing derivatives, the application will use the found source DRAWING. The application will then make a copy of the link only (in the case of online CAD document system (e.g. Onshape)) or a copy of the link and/or file (in the case of online CAD file system (e.g. SolidWorks PDM))
* When mapping drawing derivatives [checkbox `FOR DRAWINGS`] (e.g. PDF / DXF / DWG ):
  * Drawing derivatives can be configured in the DERIVATIVES menu but can only be added to DRAWING BOM Rows as defined above.
  * The derivative is *always* generated based on the DRAWING Bom Row and its parent item metadata. This means that the application will use the found source DRAWING, and convert it to the supported format specified, and copy the link and/or the file to the destination.
  * The derivative is searched for (opt-in) (Not Yet Implemented)

### Configure Derivative Name (or Search) Patterns

1. You can double click on the `PATTERN` cell of each derivative type to change the file naming pattern of the derivative that will be transfered to your ERP source. If the naming pattern is for a drawing document type, then this will be the _search pattern_ used to search for drawings. Not that when searching for drawings, only exact matches are considered. Partial matching is not supported at the time of writing due to the possibility of 1000s of results being returned.
![Alt text](images/Derivatives3.png "Configure Derivative Type Naming Pattern")
2. You can check/uncheck the `GENERATE FOR ASSEMBLIES` or the `GENERATE FOR COMPONENTS` checkbox of a derivative type to control which BOM row derivatives can be generated for which BOM component type (assemblies or components). For example, if the "STEP" derivative type is checked for assemblies, then the "STEP" BOM row derivative can be generated for any assembly row of your loaded BOM. (See also [Configure BOM Row Derivatives](#configure-bom-row-derivatives))
![Alt text](images/Derivatives4.png "Configure Derivative Type Generate For")
3. You can check/uncheck the `TRANSFER FILE` or the `TRANSFER URL` checkbox of a derivative type to have the corresponding BOM row derivative checkbox `Store File` or `Store Url` checked by default when the BOM row derivative is generated. (See also [Configure BOM Row Derivatives](#configure-bom-row-derivatives))
![Alt text](images/Derivatives5.png "Configure Derivative Type Transfer File Or Url")
4. You can uncheck the `ENABLED` checkbox of a derivative type to prevent it from being available to be generated as a BOM row derivative. You can set a derivative type as `READ ONLY` to prevent the related generated BOM row derivatives from being configured on a per row basis. (See also [Configure BOM Row Derivatives](#configure-bom-row-derivatives))
![Alt text](images/Derivatives6.png "Configure Derivative Type Enabled And Read Only")

### Auto Generate Default Derivatives

* In `Settings` -> `Display` , you can check/uncheck the `Generate default BOM row derivatives` in order to auto-generate the BOM row derivatives on SharpSync BOM load according to the derivative type configurations that you have set up in the previous section. (See also [Configure BOM Row Derivatives](#configure-bom-row-derivatives))
![Alt text](images/Derivatives7.png "Auto Generate Default Derivatives")

### Configure BOM Row Derivatives

1. If you have the user setting `Generate default BOM row derivatives` checked, all the BOM row derivatives should be auto-generated each time you load your BOM according to the derivative types configurations that you have set up in the previous sections.
2. Otherwise you can always manually add BOM row derivatives per row by:
   * Clicking on each BOM row's `DERIVATIVES` icon
   * Selecting the required derivative type from the selection list
   * Clicking on the `ADD DERIVATIVE` button
3. Note that the available derivative type list changes based on you configured derivative types.
![Alt text](images/Derivatives8.png "Generate BOM Row Derivatives")
4. You can further configure your generated BOM row derivative (if your derivative types settings permit it) on a per row basis. For example, you can manually change the `File Name` that will be stored in you ERP source. (Note: Some ERP sources such as Propel PLM have a pre-set logic on where to store component derivatives; other sources have a more flexible logic. SharpSync features that support other sources are currently in development)
![Alt text](images/Derivatives9.png "Generate BOM Row Derivatives Edit File Name")
5. You can also change the `Store File` or `Store Url` option on a per row basis.
![Alt text](images/Derivatives10.png "Generate BOM Row Derivatives Edit Store File Or Url")

### Derivatives Transfer

The CAD source derivatives will automatically be transferred to your ERP source as part of the SharpSync BOM Submittal process (when you click on the `SUBMIT BOM` button) according to your configured Derivative Types and BOM Row Derivatives settings.
   
