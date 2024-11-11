# Common List names
When setting up an Odoo source, it is useful to query the Odoo instance for lists of values for use in nestedObject property mappings.
This provides a way for you to keep the values that users can select in sync with those in Odoo.

> [!NOTE]
> For this to work the type in Odoo must be `nestedObject`. We don't currently support other types like `array` 

|List name|Returns|Sample data|
|----|----|----|
|product.category|Product template categories | `[ 1, "All" ], [ 9, "All / Consumable" ], `|
|product.tag|Tags assigned on the `General Information` tab | ` [ 11, "Kit" ], [ 12, "Assemble" ], [ 81, "Switches" ]`|
|stock.location|Locations you can assign for warehouses|`[ 14986, "MP" ], [ 14995, "MP/Assemble" ], [ 14990, "MP/Output" ],`|