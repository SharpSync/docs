# Troubleshooting datasources

## Duplicate component paths

Sometimes the following error might occur onscreen when attempting to show BOM information

![BOM contains duplicate rows and cannot be displayed](images/bom_contains_duplicate_rows_error.png)

The reason this error is shown is because there are components with duplicate paths.
Duplicate paths cause problems such as incorrect quantities or duplicate entries in the destination system and are therefore blocked on a UI level.

To illustrate, given an assembly with the following structure:

 ```javascript
A1
 → P1
 → A2
  → P2
  → P3
 ```

You’ll have 4 entries in the SharpSync UI. These entries will all have a unique component path such as:

```javascript
A1
A1/P1
A1/A2
A1/A2/P2
A1/A2/P3
```

A problem can arise if you use part numbers to generate the item. Let’s say you make a copy of `P2` => `P3`, and you forget to update the part number. You have part numbers assigned as follows:

```javascript
A1 → A1
P1 → P1
A2 → A2
P2 → P2
P3 → P2
```

Then the component paths generated will look like this

```javascript
A1
A1/P1
A1/A2
A1/A2/P2  *
A1/A2/P2  *
```

The duplicate entries (bottom 2) are the ones causing the problem that you’re seeing onscreen with the error message. To resolve this, update the part number in the source system or change the way the data is being pulled. In some datasource add-ins (such as Inventor and SolidWorks and SolidWorks PDM) you have the ability to pick either the filename or a custom property to use as the component name.
