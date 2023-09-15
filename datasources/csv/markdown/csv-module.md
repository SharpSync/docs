# CSV Setup

CSV (Comma Separated Values) files are utilized to import Bills of Materials from desktop-based CAD software such as Solidworks or Inventor into SharpSync. Follow the steps below to begin importing data into SharpSync using CSV files.

## CSV Prerequisites:
* Ensure your CSV output is complete. CSVs should contain BOM data only. Columns can be empty, but row data must not exceed the number of columns.
* Bill of Materials should be exported in an indented or structured format to encapsulate an assembly's hierarchy. Flattened BOMs are not recommended.
* For best results, ensure that the CSV is in UTF-8 format.

# Instructions

## Datasource
![Alt text](images/DataSources.png "Data Sources")
1. On the Data Sources admin page, select "Csv" and click on the Add Datasource button.
![Alt text](images/csvDatasource1.png "Add CSV Datasource")
2. Click the Configure button, then click on the BOM Configuration tab.
3. Enter the names of each column header. Make sure that the Column Headers you enter match your BOM output.
![Alt text](images/csvDatasource2.png "Set BOM Configuration")
4. Click on Save to save your changes and close the window. (No Authentication is needed for CSV files)
5. Enter the Primary and Alternative Identifiers. Your Primary Identifier will populate the Component Hierarchy in the BOM view.
![Alt text](images/csvDatasource3.png "Set Primary and Alternative Identifiers")
6. When you have finished, click on Update at the bottom to save.

## Property Mapping
![Alt text](images/PropertyMapping.png "Property Mapping")
1. On the Property Mapping page, select the Property you wish to map to the BOM.	
    * The column headers you entered in the Datasource BOM Configuration will populate each Property Mapping.
	* Each Property Mapping will be displayed as a column on the Component Assembly BOM page.
![Alt text](images/csvPropertyMapping1.png "Select Property Mapping")
2. 
