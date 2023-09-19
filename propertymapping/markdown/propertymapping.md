# Property Mapping
![Alt text](../images/PropertyMapping.png "Property Mapping")  
Property Mapping defines the way BOM data is displayed in SharpSync. Property Mappings can display a variety of CAD information including (but not limited to) BOM columns, Part or Assembly properties, Configurations, or CAD model data. SharpSync has built-in rules and settings for each property mapping. These rules and settings are used to help codify, standardize, and push changes to the selected datasources.

## Instructions
### Adding Property Mappings
1. On the Property Mapping page, select the Property you wish to map to the BOM.	
    * The column headers you entered in the Datasource BOM Configuration will populate each Property Mapping.
	* Each Property Mapping will be displayed as a column on the Component Assembly BOM page.

![Alt text](../images/PropertyMapping1.png "Select Property Mapping")

2. Once you have selected the property mappings that you want to appear in the SharpSync BOM, confirm that the Accessors, Primary Datasource Accessors, and Secondary Datasource Accessors columns are correct. You can double click on the cells in each column to change the value SharpSync will be matching. The accessor must be present in the appropriate datasource.

![Alt text](../images/PropertyMapping2.png "Check Accessors")
### Configure Property Mapping Settings
#### Update Datasource
1. To change the settings of each Property Mapping, click on the gear in the Settings column.
2. Verify that the accessor for each Datasource is correct. Click on the checkbox "Update Source on Submit" for each Datasource that you want to make changes to from SharpSync.
    * If you only want the information from the CAD data (Primary Datasource) to change the ERP/PDM/PLM (Secondary Datasource), then check only the Secondary Datasource checkbox.
    * If you want both sources to change, check both checkboxes.
    * Settings are saved for each Property Mapping.

![Alt text](../images/PropertyMapping3.png "Select Source")
#### Rendering
3. Rendering defines how the Property Mapping is viewed and accessed in the BOM.
    * Rendering Types change the display of the Property Mapping:
        * Checkbox - Toggle checkbox
        * FreeText - Enter text
        * List - Select from a list. Enter the list set in the textbox and separate each entry with a Vertical Pipe (see example below)
        * Url - Web address hyperlink
    * The remaining checkboxes affect the way the column display and interface:
        * Enabled - When unchecked the column will not be visible in the BOM nor any related mapping rule will be processed
        * Read Only - When checked, BOM column will not be editable
        * Show in Totals - The total for that column will be shown in the Totals row at the bottom of the BOM
        * Visible - When unchecked, column will not be visible, but user cna unhide from the BOM column context menu

![Alt text](../images/PropertyMapping4.png "Rendering")  
4. Click Save to finish.
### Configure Property Mapping Rules