# NetSuite
NetSuite is an ERP from Oracle and support OAuth integration.

## Selecting array values

Array values are values that are limited in scope. The user may only specify that value. Internally in NetSuite this is known as enum values, but SharpSync displays it as an `array` type.

![image](https://github.com/SharpSync/docs/assets/5020751/241706db-2b2e-4a35-ac27-9ac8fe814d2e)

When a column is mapped as an array value, the default values for that column should typically be mapped as a `List` instead of `FreeText`

![image](https://github.com/SharpSync/docs/assets/5020751/6dfe8e56-5911-4b11-9e4c-022528cc81b0)

When a  value is received from NetSuite it will come in the form of a Json Object.

```Json
"costingMethod": {
        "id": "AVG",
        "refName": "AVG"
},
```

In order to parse this correctly, one would have to use at least 1 rule: `Select From Json`, using the key `refName`. In this case the value of `refName`, "AVG" will be selected from the imported json object and displayed onscreen in the BOM for new and existing rows

![image](https://github.com/SharpSync/docs/assets/5020751/f181838b-f92e-4438-a68c-c34022774b05)



