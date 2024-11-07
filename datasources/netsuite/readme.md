# NetSuite
NetSuite is an ERP from Oracle and support OAuth integration.


* [Setting up permissions required for OAuth](markdown/netsuite_oauth.md)
* [Setting up a thumbnail folder](#setup-thumbnail-folder) (not necessary but recommended)
* [Setting up an item Type mapping](#setup-item-type-mapping)
* [Setting up accounts from a list](#setting-up-accounts-from-a-list)
* [Setting up advanced BOMs](markdown/advanced_boms.md)
* [Setting up server-side script (restlet)](markdown/advanced_boms.md#setup-the-server-side-script)
* [Configuring Routings](markdown/configure_routings.md) 

See also
* [Common Scenarios](markdown/common-scenarios.md)
* [Integration tips](markdown/developer-tips.md)
* [Feature matrix for Netsuite](markdown/feature_matrix_netsuite.md)

## Setup Thumbnail Folder

While not strictly necessary, it is recommended to setup a thumbnails folder in NetSuite. This lets you generate an image preview for a file in NetSuite.

See [Setup thumbnail folder in NetSuite](markdown/netsuite_setup_thumbnail_folder.md)

## Setup Item Type mapping 

At least one property mapping for NetSuite _must_ be set as an item type mapping. You can leave the Netsuite mapping as _(Unmapped)_ and invisible, but the mapping must exist.
Typically you'd want to set this as 'prefer NetSuite value' as well, but that's optional.

When an item is created in NetSuite, it is typically one of the following 
* assemblyitem
* noninventoryresaleitem
* inventoryitem
* noninventorypurchaseitem

As such, add this as a list of options to pick from. You can include any items in this list that is supported by your installation of NetSuite.

![image](https://github.com/SharpSync/docs/blob/main/datasources/netsuite/images/item-type-mapping.png)

In addition to this you'll want to create 2 rules:
1. A text manipulation rule for NetSuite / Onshape that runs the following script (or similar based on your setup) on data import:

```Javascript
if (rowData.isAssemblyRow) return 'assemblyitem'; return 'noninventorypurchaseitem';
```

2. A `Text not empty` rule. This will prevent errors when submitting the BOM

> On a more technical note: These items are derived by calling the endpoint /GET `{{netsuite-api}}/services/rest/record/v1/metadata-catalog` with an empty body

## Selecting array values

Array values are values that are limited in scope. The user may only specify that value. Internally in NetSuite this is known as enum values, but SharpSync displays it as an `array` type.

![image](https://github.com/SharpSync/docs/assets/5020751/241706db-2b2e-4a35-ac27-9ac8fe814d2e)

When a column is mapped as an array value, the default values for that column should typically be mapped as a `Select List` instead of `FreeText`

![image](https://github.com/SharpSync/docs/blob/main/datasources/netsuite/images/array_values_select_list.png)

When a  value is received from NetSuite it will come in the form of a Json Object.

```Json
"costingMethod": {
        "id": "AVG",
        "refName": "AVG"
},
```

In order to parse this correctly, one would have to use at least 1 rule: `Select From Json`, using the key `refName`. In this case the value of `refName`, "AVG" will be selected from the imported json object and displayed onscreen in the BOM for new and existing rows

![image](https://github.com/SharpSync/docs/assets/5020751/f181838b-f92e-4438-a68c-c34022774b05)

## Setting up accounts from a list
Netsuite has lists which can be queried using the UI of property mappings.

One such list is `accounts`. To show account names, do the following:
* Add a new property mapping for `expenseAccount`
* Add a list value selector `{acctNumber} : {acctName}`

![image](https://github.com/SharpSync/docs/blob/main/datasources/netsuite/images/account_name_selection.png)

** A list value selector is a string that selects token values (text items wrapped in curly braces) from the returned JSON object.
In our example above, when specifying the list name of `account`, the object returned for each list may look something like this:

```Json
{
  "links": [
    {
      "rel": "self",
      "href": "https://[customerId].suitetalk.api.netsuite.com/services/rest/record/v1/account/677"
    }
  ],
  "accountContextSearch": {
    "links": [
      {
        "rel": "self",
        "href": "https://[customerId].suitetalk.api.netsuite.com/services/rest/record/v1/account/677/accountContextSearch"
      }
    ]
  },
  "acctName": "Beginning Equity AP",
  "acctNumber": "5305",
  "acctType": {
    "id": "Equity",
    "refName": "Equity"
  },
  "balance": 0.0,
  "eliminate": false,
  "id": "677",
  "inventory": false,
  "isInactive": false,
  "isSummary": false,
  "lastModifiedDate": "2024-05-06T14:55:00Z",
  "localizations": {
    "links": [
      {
        "rel": "self",
        "href": "https://[customerId].suitetalk.api.netsuite.com/services/rest/record/v1/account/677/localizations"
      }
    ]
  },
  "parent": {
    "links": [
      {
        "rel": "self",
        "href": "https://[customerId].suitetalk.api.netsuite.com/services/rest/record/v1/account/188"
      }
    ],
    "id": "188",
    "refName": "5800 Amanda L. Perry"
  },
  "revalue": false,
  "subsidiary": {
    "links": [
      {
        "rel": "self",
        "href": "https://[customerId].suitetalk.api.netsuite.com/services/rest/record/v1/account/677/subsidiary"
      }
    ]
  }
}
```

### Example 1
Suppose we want to display the account name from the above example as `5305 - Beginning Equity AP` then our list value selector would be made up of 2 seperate json tokens.
1. `5305` - the json token `acctNumber`
2. `Beginning Equity AP` - the json token `acctName`

We then specify a token selection string of `{acctNumber} - {acctName}`

### Example 2
Suppose we want to display the account name from the above example as `5800 Amanda L. Perry` then our list value selector would be made up of a single json tokens.

We then specify a token selection string of `{parent.refName}` because we're selecting the child `refName` from the token called `parent`

Both the examples above will result in a list seperated by the pipe symbol |

note: if you don't specify the selector string, then the entire json object will the shown as the listitem.

note2: The difference between a `list value selector` and an `object value selector` is that the former will construct a text item from a json object, and return a list of items separated by pipe symbol |. The latter will select a value from a single nested object, and return only a single item, not a list of strings.

note3: Should you want to change the selector string or any of the tokens being selected, then you have to first remove the list name, save, change the tokens, then enter the list name again. The selection is generated at the time of loading the list from NetSuite, and since this can be a data intensive process, SharpSync doesn't store all the details all the time, it only stores the specified details.
