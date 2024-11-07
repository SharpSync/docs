# BOM Comparison

## BOM row updates

BOM row updates can occur in the primary or secondary datasource and is influenced by your settings for:
* [Property Mappings](../propertymapping/readme.md) 
* [Rules](../propertymapping/markdown/rules.md) 

BOM row updates are also influenced by whether the `PROCESS` checkbox is checked or unchecked. You can use the context menu of any given row's `PROCESS` cell to bulk check/uncheck the `PROCESS` checkbox of related rows and children rows.

### Primary Source updates

When updating BOM rows the following table illustrates how updates occur at the primary source.

A primary source is typically a CAD or PDM or PLM system. For primary sources, quantity values are typically not updated.

Using the default color scheme for BOM comparison, you can expect the following results: 

|Process Row|Row Background|Item Creation|Bom Structure|Quantity|Item Properties|Routings|Derivatives
|:---:|---|:---:|---|:---:|:---:|:---:|:---:|
|☑️|⬜ White|N/A|Unchanged|Unchanged|Updated|N/A|N/A|
|☑️|🟩 Green|N/A|Unchanged|Unchanged|Updated|N/A|N/A|
|☑️|🟨 Yellow|N/A|Unchanged|Unchanged|Updated|N/A|N/A|
|☑️|🟥 Red|N/A|Unchanged|Unchanged|Ignored|N/A|N/A|
||⬜ White|N/A|Unchanged|Unchanged|Ignored|N/A|N/A|
||🟩 Green|N/A|Unchanged|Unchanged|Ignored|N/A|N/A|
||🟨 Yellow|N/A|Unchanged|Unchanged|Ignored|N/A|N/A|
||🟥 Red|N/A|Unchanged|Unchanged|Ignored|N/A|N/A|

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
 
