# BOM Comparison

## BOM row updates

BOM row updates can occur in the primary or secondary datasource and is influenced by your settings for property mappings and their related import / export rules

 * [Primary source updates](#primary-source-updates)
 * [Secondary source updates](#secondary-source-updates)

### Primary Source updates

When updating BOM rows the following table illustrates how updates occur at the primary source.

A primary source is typically a CAD or PDM or PLM system. For primary sources, quantity values are typically not updated.

Using the default color scheme for BOM comparison, you can expect the following results: 

|Process Row|Row background|Result|
|---|---|---|
|Yes|White|Row properties will be updated in {Datasource}|
|Yes|Green|Row properties will be updated in {Datasource}|
|Yes|Orange|Row properties + qty will be updated in {Datasource}|
|Yes|Red|Row properties + qty will NOT be updated in {Datasource}. It will be unlinked (removed) from any parent items|
|No|White|Row properties + qty will not be updated {Datasource}|
|No|Green|Row will not be created in {Datasource}|
|No|Orange|Row properties + qty will not be updated in {Datasource}|
|No|Red|Row properties + qty will NOT be updated in {Datasource}. It will also not be unlinked (removed) from any parent items|

### Secondary Source updates


When updating BOM rows the following table illustrates how updates occur at the secondary source.

A secondary source is typically an ERP or PLM system. For secondary sources, quantity values are typically updated to reflect the quantities of the primary soruce.


Using the default color scheme for BOM comparison, you can expect the following results: 

|Process Row|Row Background|Item Creation|Bom Structure|Quantity|Item Properties|Routings|Derivatives
|:---:|---|:---:|---|:---:|:---:|:---:|:---:|
|☑️|⬜ White||Unchanged|Updated|Updated|Updated|Processed|
|☑️|🟩 Green|Created|Linked To Parent|Updated|Updated|Updated|Processed|
|☑️|🟨 Yellow||Linked To Parent|Updated|Updated|Updated|Processed|
|☑️|🟥 Red||Unlinked From Parent + Children Ignored|Ignored|Ignored|Ignored|Ignored|
||⬜ White||Unchanged|Ignored|Ignored|Ignored|Ignored|
||🟩 Green|Not Created|Not Linked To Parent|Ignored|Ignored|Ignored|Ignored|
||🟨 Yellow||Not Linked To Parent|Ignored|Ignored|Ignored|Ignored|
||🟥 Red||Link To Parent Kept + Children Ignored|Ignored|Ignored|Ignored|Ignored|
 
