# Common scenarios

*  [Setup a list of accounts to pick from for Income and Expense accounts](#i-want-to-setup-a-list-of-accounts-to-pick-from-for-income-and-expense-accounts)
*  [Setting up accounts from a list](#setting-up-accounts-from-a-list)
*  [Setting up a default value for income and expense accounts](#setting-up-a-default-value-for-income-and-expense-accounts)
*  [Set all new assemblies as isPhantom with rulecheck + evaluation](#set-all-new-assemblies-as-isphantom-with-rulecheck--evaluation)
*  [Discovering property (accessor) names](#discovering-property-accessor-names)


## I want to setup a list of accounts to pick from for Income and Expense accounts
This will require list selection from NetSuite. Use the following setup:

|Option|Value|Description| 
|:--|:------|:--|
|Object Value Selector|`refName`|The object to select from the Object returned|
|List Name|`account`|The list to query in NetSuite|
|List Value Selector|`{acctNumber}`&#160;:&#160;`{acctName}`|Which values to select from the selected object to show as the display name| 

To setup a list of accounts to pick from in NetSuite, we'll query the `accounts` list and select some values from it.

What we’re doing here is that we’re getting back a list of values from NetSuite

Those values are a list that look something like this: [item1, item2, item3]

Where Items 1-3 contain at least the following data:

```json
[{
 "acctName" : "Income",
 "refName" : "Income account",
 "acctNumber" : 1234
},
{
 "acctName" : "Expense",
 "refName" : "Expense account",
 "acctNumber" : 1235
}] 
```

So we’re  selecting the values from that list and using it as a display name
 
Our selector of `{acctNumber} : {acctName}`

Will render a result of 

`1234: Income|1235: Expense`

The reason we use this more complicated method of selection is because this lets us pull data from any list in netsuite, not just accounts, which greatly amplifies the flexibility of the software

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

## Setting up a default value for income and expense accounts

To setup a default value, you can use a rule such as this

### New Rule
Rule: `Set cell Text` (Import Rule)

Value: 

`7116 : Indirect Materials and Supplies - Absorbed` (this must match the pattern you use in your `Object value selector`)

### New Rule
Rule: `Text Evaluation` (Display Rule)

Value: 

```javascript
if (rowData.cells.expenseAccount == rowData.cells.incomeAccount) return { 'status': 'failure' }
```
## Set all new assemblies as isPhantom with rulecheck + evaluation

This setup will cause all new assemblies in NetSuite to be marked as Phantom. 
Onscreen you will also see any new assemblies (not marked as Phantom) showing with an error.

![image](https://github.com/SharpSync/docs/blob/main/datasources/netsuite/images/set-as-phantom.png)

Prerequisites:
You have a property mapping set where the accessorName is `phantomYN`
### New Rule
Accessor name: `isPhantom`
Property Mapping in Netsuite: `isPhantom`
Rule: `Text manipulation` (Import)

Value:
```Javascript
const isNewAssemblyRow = rowData.isAssemblyRow && rowData.isMissingInSecondaryDatasource == true && rowData.isFoundInSecondaryDatasource == false;

if (isNewAssemblyRow)
  { return true; }
else
  { return rowData.cells.isPhantom || rowData.differences.isPhantom || true; }
```

### New Rule
Accessor name: `isPhantom`
Property Mapping in Netsuite: `isPhantom`
Rule: `Text evaluation` (Display Rule)
Value:

```Javascript
const isNewAssemblyRow = rowData.isAssemblyRow && rowData.isMissingInSecondaryDatasource == true && rowData.isFoundInSecondaryDatasource == false;

if (isNewAssemblyRow && (rowData.cells.isPhantom === "false" || (`isPhantom` in rowData.modifications === true && rowData.modifications.isPhantom === false)))
{
  return { status: 'failure', message: `New Assemblies must be set to isPhantom=true` }
}
```

## Discovering property (accessor) names
NetSuite item types have different backing properties depending on the area of NetSuite you're working in as well as for the item type.
For example, `InventoryItem` types will not have the same values as `AssemblyItem` types.

When creating new `InventoryItem` items you'll have to set certain item properties that are required such as (but not limited to)
* Country of manufacture
* Tax schedule
* Unit Type

However the name of thse values will not correspond to what you're seeing onscreen. In the backend they may be called 
* countryOfManufacture
* taxSchedule
* baseUnit


In order to discover what they are named, you can query a NetSuite `InventoryItem` resource using the following request

> {{netsuite-api}}/services/rest/record/v1/inventoryItem/{itemId}?expandSubResources=true
> 
For example

> https://123456-sb1.suitetalk.api.netsuite.com/rest/record/v1/inventoryItem/20567?expandSubResources=true

This will yield a result such as this 
```json
{
    "links": [
        {
            "rel": "self",
            "href": "https://4293129-sb1.suitetalk.api.netsuite.com/services/rest/record/v1/inventoryItem/20567?expandSubResources=true"
        }
    ],
    "assetAccount": {
        "links": [
            {
                "rel": "self",
                "href": "https://4293129-sb1.suitetalk.api.netsuite.com/services/rest/record/v1/account/133"
            }
        ],
        "id": "133",
        "refName": "1420 Inventory : Inventory Parts"
    },
    "atpMethod": {
        "id": "CUMULATIVE_ATP_WITH_LOOK_AHEAD",
        "refName": "Cumulative ATP with Look Ahead"
    },
    "autoLeadTime": true,
    "autoPreferredStockLevel": true,
    "autoReorderPoint": true,
    "availableToPartners": false,
    "averageCost": 1,
    "baseUnit": "1",

    // ... more 
}
```
  
From the example response above we can get accessor names to be shown in SharpSync. The names in the above sample start with 
* links
* assetAccount,
* atpMethod
* autoLeadTime
* autoPreferredStockLevel
* autoReorderPoint
* availableToPartners
* averageCost
* baseUnit
* ... more

In SharpSync you're then able to select accessors from this list. Reminder that an accessor is just a property on a type. So `assetAccount` is an accessor (the data we're accessing) or property on `InventoryItem`
  
