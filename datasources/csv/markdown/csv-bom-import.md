# Importing a CSV BOM

Once the Datasource and Property Mapping sections have been set up, you can now begin importing CSV Bills of Materials.

### Get the CSV BOM
![Alt text](../images/csvImportBom1.png "CSV BOM Page")  
In the SharpSync BOMs page you will see a section at the bottom of the page with a dash-lined border around it. You can drag and drop your .csv file from a File Manager (Explorer for Windows, Finder for Mac). Alternatively, you can click inside the box and navigate to where the file is located and upload it.

### Pre-Process Specifications
![Alt text](../images/csvImportBom2.png "CSV Pre-process")  
1. *Does the first row contain headers.* Toggle the checkbox to indicate if the CSV file has headers.
2. *CSV Delimiter.* Typically, a CSV file will separate each "cell" with a common delimiter, typically a comma. Enter the delimiter used.
3. *Row Number Column.* Type in the column that contains the Row Numbers. This is important as these numbers are what is used to establish the assembly hierarchy. Every cell in this column should have a different Row Number.
4. *Row Number Delimiter.* Enter the row number delimiter. SharpSync parses the hiearchy for each item using its row number.
    * Row Numbers with a Period: 1.2.3.4
    * Row Numbers with a Comma: 1,2,3,4
5. *Component Number/Name.* Enter the Top Level Assembly name or number in this field. Typically, the name/number will match the .csv filename.
6. *Primary Component Identifier.* This is usually synonymous with the Component Name or Number. In the above example, PartNo is the column used.
7. *Configuration Name.* Enter the Top Level Assembly Configuration name, typically set to default.
8. *Process CSV.* Click this button to finish. The BOM page will show the newly added BOM.  

![Alt text](../images/csvImportBom3.png "CSV BOM Page Imported")  

### Import Success
The BOM is now ready to be accessed once it is uploaded. Click on the BOM to view its contents.  
![Alt text](../images/csvImportBom4.png "CSV BOM Import Success")  