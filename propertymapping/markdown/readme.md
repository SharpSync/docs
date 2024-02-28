# Sample rules

This is a WIP collection of rules that we often use. The rules below are useful for common scenarios.

* You may copy and paste them as you wish.
* Multiline text will be converted to a single line

  
*Text evaluation:* Check that part files have a material
```Javascript
if (!rowData.isAssemblyRow)
{
  if (!s)
    return { status: 'failure', message: `Parts must have materials assigned`, passOrBlock: `pass`};
}
```
