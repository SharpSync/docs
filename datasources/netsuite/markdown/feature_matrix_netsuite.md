
# NetSuite supported features

Out of the box, the Netsuite integration supports the following features:

 ## Bom level features
|Feature|Differences|Modifications|Updates|
|:---------------------------|:---:|:---:|:---:|
|Bom hierarchy|:white_check_mark:|:white_check_mark:|:white_check_mark:|
|Bom meta data|:white_check_mark:|:white_check_mark:|:white_check_mark:|
|Bom quantities|:white_check_mark:|:white_check_mark:|:white_check_mark:|
|Component thumbnails|||:white_check_mark:|
|Advanced BOMs|:white_check_mark:|:white_check_mark:|:white_check_mark:|[in testing (development completed)]|
|File derivative transfers (e.g. STEP, DXF)**|||[In progress]|
|Routings|||[In progress]|

** It should be noted that there are many ways to transfer files. We're in the process of adding file transfers for NetSuite, but please note that consultation services are required to understand your use case + configuration options. More information to follow in the configuration of file transfers from the CAD system.

## Item level features

The list of items that are supported are shown below. These have been officially tested and are supported. Please note that we're open for discussion on other item types, and we treat them as part of our consulation services. Most item types would not require any implementation as they follow the same standard in the NetSuite API. 

|Item type|Differences|Modifications|Updates|
|:---------------------------|:---:|:---:|:---:|
|inventoryitem|:white_check_mark:|:white_check_mark:|:white_check_mark:|
|assemblyitem|:white_check_mark:|:white_check_mark:|:white_check_mark:|
|noninventoryresaleitem|:white_check_mark:|:white_check_mark:|:white_check_mark:|
|noninventorypurchaseitem|:white_check_mark:|:white_check_mark:|:white_check_mark:|
|bom|:white_check_mark:|:white_check_mark:|:white_check_mark:|
|bomrevision|:white_check_mark:|:white_check_mark:|:white_check_mark:|
|routing operation|||:white_check_mark:|
|routing step|||:white_check_mark:|
|serializedinventoryitem|[on roadmap]|[on roadmap]|[on roadmap]|
|serializedassemblyitem ||[on roadmap]|[on roadmap]|[on roadmap]|
