# Advanced BOMs

Advanced BOMs are Netsuite's way of keeping track of bill of materials (BOM) snapshots. You can think of an advanced BOM as the revision of a BOM at a certain point in time

## Using advanced BOMs
There are some limitation with the use of advanced BOMs via the API. For this reason (at the time of writing), we make use of a custom script to create advanced BOMS

Server side scripting uses a script in Netsuite to set field values.
The important bit to take note of here is that the `injectionScriptId` needs to be configured (see below).

To use serverside scripting to create items, in SharpSync do the following under `Data Sources`:

## Major steps

* [Setup the server side script](#setup-the-server-side-script)
* [Configure SharpSync to use server side scripting](#configure-sharpsync-to-use-server-side-scripting)

### Setup the server side script

In Netsuite, create a new script for SharpSync to use (example at the bottom)

* Click Setup > Customization > Scripts 
* Select the `Script File` box > click the + sign
* Upload the script file from your computer 
    * Attach from: `Computer`
    * Filename: Specify with the `.js` extension at the back
    * Folder: <span style='color:orange'> This must be `SuiteScripts`. DO NOT use another folder</span>
    * Choose file: choose the file you saved (you can use the example below after some customization of fields)
    * Click Save
* Click > Create Script Record
    * Specify a name: `sharpsync-item-create.js`
    * Click the `Deployments` tab > Enter any name
        * Deployed: `Yes`
        * Status: `Released`
    * Click `Save`
* After clicking Save and the page has loaded:
    * Under the `Scripts` tab > click `Edit`. You can make changes here
    * Under the `Deployments` tab > Click the script name
        * A new page is shown `Script Deployment`
        * In the `URL` field you'll see a deployment url, something like 
        * <span style='color:orange'> /app/site/hosting/restlet.nl?script=3187&deploy=1 </span>
        * Take note of the id of the script (in the example above it's `3187`)

You are now done configuring the script in Netsuite. The next step is to use this ID in the setup of the script in SharpSync.

### Configure SharpSync to use server side scripting

Server side scripting allows SharpSync to configure fields in NetSuite that are not available via the REST api.

* Add Netsuite as a data source
* Click the `Configure` button
* Navigate to the `Configuration` section
* Add a servlet url
    > https://[companyId].restlets.api.netsuite.com/app/site/hosting/restlet.nl?script=3187&injectionScriptId=3187&deploy=1&folderId=3561
* The `injectionScriptId` param above is the same as the one in the previous step
* Select `Use server side scripting`
* Select `Use advanced BOMs`
* Configure your `Bom Naming scheme`
* Configure your `Bom Revision Naming Scheme`
* Click the Save button


A custom script example follows below. You can certainly modify this to your heart's content, but the overarching details are captured here

Before uploading to Netsuite, save the below contents to a `*.js` file
```Javascript
/*
  Created for SharpSync.net
  Description: 
*/

/**
 * @NApiVersion 2.x
 * @NScriptType Restlet
 */
/**
 * @param {string} assemblyId
 */
define(['N/record', 'N/search', 'N/log', 'N/encode', 'N/error'], function (record, search, log, encode, error) {

  const itemTypes_e = {
    INVENTORY_ITEM: 'inventoryItem',
    NON_INVENTORY_ITEM: 'nonInventoryItem',
    NON_INVENTORY_RESALE_ITEM: 'nonInventoryResaleItem',
    NON_INVENTORY_PURCHASE_ITEM: 'nonInventoryPurchaseItem',
    ASSEMBLY_ITEM: 'assemblyItem'
  };

  /* 
      SharpSync always uses the following appState to confirm validity
      X-APPLICATION => header naming the application
      X-USERID => header naming the user (uuid)
      X-ORG_ID => header naming the organization
  */
  function get(context) {

    validateAppState(context.appState, encode, error)

    log.debug({
      title: 'gettingRecord',
      details: context
    });

    if (context.recordId) {
      var requestedRecord = record.load({
        type: "nonInventoryResaleItem",
        id: context.recordId,
        isDynamic: true
      });

      return {
        expAcc: requestedRecord.getValue({ fieldId: 'expenseaccount' }),
        incAcc: requestedRecord.getValue({ fieldId: 'incomeaccount' }),
        itemDetails: requestedRecord
      };
    }


    // Check any /GET query parameters here with context.{parameterName}
    if (!context.name) {
      throw error.create({
        name: 'MISSING_NAME',
        message: 'Missing required argument: item name',
        notifyOff: true
      });
    }

    //getValidTaxSchedules()
    return { name: context.name, itemDetails: itemDetails };
  }

  /* SharpSync always uses the following headers to confirm:
     X-APPLICATION => header naming the application
     X-USERID => header naming the user (uuid)
     X-ORG_ID => header naming the organization
  */
  function post(context) {

    /* TODO: Remove log.debug({ title: 'POST body', details: context }); */
    validatePostRequestPrereqs(context);
    validatePostRequestItemType(context, error, log);

    var itemRecord = CreateItemFromContext(context, record, log);

    log.debug({
      title: 'Item record',
      details: itemRecord
    });
    setCustomerSpecificDefaultValues(itemRecord, context.itemType);

    var itemId = itemRecord.save();
    var serializedItemRecord = JSON.parse(JSON.stringify(itemRecord));
    // must parse. For some reason when accessing it directly you get null
    return {
      applicationName: context.applicationName,
      sharpsyncId: context.sharpsyncId,
      organizationId: context.organizationId,
      itemId: itemId,
      itemName: context.name,
      destinationTypeRequested: context.itemType,
      baseRecordTypeName: serializedItemRecord.fields.baserecordtype || "unknown",
      url: '/services/rest/record/v1/' + serializedItemRecord.fields.baserecordtype + '/' + itemId + '/?expandSubResources=true'
    };
  }

  return {
    get: get,
    post: post
  };
});

function CreateItemFromContext(context, record, log) {

  var itemRecord;
  var isDynamic = true;

  switch (context.itemType) {
    case "inventoryitem":
      itemRecord = record.create({ type: record.Type.INVENTORY_ITEM, isDynamic: isDynamic });
      break;
    case "assemblyitem":

      log.debug({
        title: 'Context.itemMethod',
        details: context.itemMethod
      });

      if (context.itemMethod == "createBomLink") {
        linkBomToAssemblyItem(context, record);
      }
      else {
        itemRecord = record.create({ type: record.Type.ASSEMBLY_ITEM, isDynamic: isDynamic });
      }

      break;
    case "noninventoryresaleitem":
      itemRecord = record.create({ type: record.Type.NON_INVENTORY_ITEM, isDynamic: isDynamic });
      itemRecord.setValue({ fieldId: 'subtype', value: 'resale' });
      break;
    case "noninventorypurchaseitem":
      itemRecord = record.create({ type: record.Type.NON_INVENTORY_ITEM, isDynamic: isDynamic });
      itemRecord.setValue({ fieldId: 'subtype', value: 'purchase' });
      break;
    case "bom":
      itemRecord = createBomFromContext(context, record);
      break;
    default:
      throw error.create({
        name: 'INVALID_ITEM_TYPE',
        message: 'Invalid item type (' + context.itemType + '), must be one of {inventoryitem|assemblyitem|noninventoryresaleitem|noninventorypurchaseitem|bom}',
        notifyOff: true
      });
  }

  itemRecord.setValue({
    fieldId: 'itemid',
    value: context.name, // Change this to the actual item name
  });

  return itemRecord;
}

function linkBomToAssemblyItem(context, record) {
  var bomRecord = record.load({
    type: record.Type.BOM,
    id: context.bomId,
    isDynamic: true
  });

  var assemblyItemRecord = record.load({
    type: record.Type.ASSEMBLY_ITEM,
    id: context.assemblyItemId,
    isDynamic: true
  });

  assemblyItemRecord.setValue({
    fieldId: 'billofmaterials',
    value: context.bomId
  });

  assemblyItemRecord.setValue({
    fieldId: 'billofmaterialsrevision',
    value: context.bomRevisionId
  });

  assemblyItemRecord.save();
}

// These values are customized per customer implementation
// You would set your default values here for values that are not exposed through the API
// At the time of writing, it was not possible to set the taxSchedules for type inventoryItem
function setCustomerSpecificDefaultValues(itemRecord, destinationType) {

  itemRecord.setValue({
    fieldId: 'taxschedule',
    value: 2,
  });

  itemRecord.setValue({
    fieldId: 'costcategory',
    value: 4,
  });

  // value below can be any of {Purchase|Resale|Sale}
  if (destinationType === "noninventoryresaleitem") {
    itemRecord.setValue({
      fieldId: 'subtype',
      value: 'resale'
    });

    itemRecord.setValue({
      fieldId: 'incomeAccount',
      value: 54
    });

    itemRecord.setValue({
      fieldId: 'expenseAccount',
      value: 616
    });

  }
}

function getValidTaxSchedules() {

  var types = Object.keys(search.Type);
  var taxTypes = types.filter(function (type) {
    return type.toLowerCase().indexOf('tax') !== -1;
  });

  log.debug({
    title: 'Searchable tax types',
    details: taxTypes
  });

  var taxScheduleSearch = search.create({
    type: search.Type.TAX_TYPE,
    columns: ['internalid']
  });

  var taxSchedules = taxScheduleSearch.run().getRange({
    start: 0,
    end: 10
  });

  return taxSchedules;
}

function decodeBase64(base64String, encode) {
  // Decode the Base64 string using N/encode module
  var decodedString = encode.convert({
    string: base64String,
    inputEncoding: encode.Encoding.BASE_64,
    outputEncoding: encode.Encoding.UTF_8
  });
  return decodedString;
}

function validateApplicationName(applicationHostName, error) {
  if (applicationHostName !== 'dev.sharpsync.net' && applicationHostName !== 'localhost') {
    throw error.create({
      name: 'INVALID_APPLICATION',
      message: 'Invalid application',
      notifyOff: true
    });
  }
}

function validateSharpSyncId(sharpsyncId, error) {
  if (!sharpsyncId) {
    throw error.create({
      name: 'MISSING_SHARPSYNC_ID',
      message: 'Missing SharpSync Id',
      notifyOff: true
    });
  }
}

function validateOrganizationId(organizationId, error) {
  if (!organizationId) {
    throw error.create({
      name: 'MISSING_ORG_ID',
      message: 'Missing organization id',
      notifyOff: true
    });
  }
}

function validateAppState(base64String, encode, error) {

  const jsonString = decodeBase64(base64String, encode);
  const jsonObject = JSON.parse(jsonString);

  validateApplicationName(jsonObject['applicationName'], error);
  validateSharpSyncId(jsonObject['sharpsyncId'], error);
  validateOrganizationId(jsonObject['organizationId'], error);
}

function validatePostRequestPrereqs(requestBody, error) {
  validateApplicationName(requestBody['applicationName'], error);
  validateSharpSyncId(requestBody['sharpsyncId'], error);
  validateOrganizationId(requestBody['organizationId'], error);
}

function validatePostRequestItemType(context, error, log) {

  if (context.itemType !== "inventoryitem" && context.itemType !== "assemblyitem" && context.itemType !== "noninventoryresaleitem" && context.itemType !== "bom" && context.itemType !== "bom") {
    log.error({
      title: 'Invalid item type',
      details: 'Invalid item type (' + context.itemType + '), must be one of {inventoryitem|assemblyitem|noninventoryresaleitem|noninventorypurchaseitem|bom}',
      notifyoff: true
    });

    throw error.create({
      name: 'INVALID_ITEM_TYPE',
      message: 'Invalid item type (' + context.itemType + '), must be one of {inventoryitem|assemblyitem|noninventoryresaleitem|noninventorypurchaseitem|bom}',
      notifyOff: true
    });
  }
}

function createBomFromContext(context, record) {
  var itemRecord = record.create({
    type: record.Type.BOM,
    isDynamic: true,
    name: context.name,
    includechildren: true,
    usecomponentyield: true,
  });

  // set the subsidiary 
  itemRecord.setValue({
    fieldId: 'subsidiary',
    value: 1,
  });

  for (var key in context) {
    if (itemRecord.hasOwnProperty(key)) {
      itemRecord.setValue({
        fieldId: key,
        value: context[key]
      });
    }
  }

  return itemRecord;
}
```