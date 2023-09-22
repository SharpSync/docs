# List of Property Mapping Rules
Property Mapping Rules are used to define the output format of the BOM data shown in SharpSync. When a rule is applied, all cells in a column mapped to a property will be evaluated. If the cell data does not fall within the rules applied, the cell will display an error color on its border, with a more detailed explanation in the cell overlay. Hover over a cell to see the applied rules evaluated in the overlay. Click on list icon in the Rules column of the desired Property Mapping to begin. Below is a comprehensive list of each Property Mapping Rule. Expand the Table of Contents and click a specific rule to jump to that rule. Learn more about Rule setup: [Configure Rules](propertymapping#configure-rules)  

<details open>
    <summary>Table of Contents</summary>
    <blockquote>
    <details>
        <summary>Display Rules</summary>
        <blockquote>

[Cell value evaluation](#cell-value-evaluation)  
[Maximum text length](#maximum-text-length)  
[Minimum text length](#minimum-text-length)  
[Number between](#number-between)  
[Text length must be between](#text-length-must-be-between)
</blockquote>
</details>
<details>
    <summary>Import/Export Rules</summary>
    <blockquote>

[Append text](#append-text)  
[Calculate number](#calculate-number)  
[Cell value manipulation](#cell-value-manipulation)  
[Format as decimal number](#format-as-decimal-number)  
[Parse JSON](#parse-json)  
[Prepend text](#prepend-text)  
[Replace text](#replace-text)  
[Round to nearest X](#round-to-nearest-x)  
[Set cell value](#set-cell-value)  
[Set empty cells](#set-empty-cells)  
[Text length must equal](#text-length-must-equal)  
[Text must be exactly](#text-must-be-exactly)  
[Text must contain string](#text-must-contain-string)  
[Text must end with string](#text-must-end-with-string)  
[Text must not be empty](#text-must-not-be-empty)  
[Text must not contain string](#text-must-not-contain-string)  
[Text must not end with string](#text-must-not-end-with-string)  
[Text must start with string](#text-must-start-with-string)  
[Value must be in list](#value-must-be-in-list)  
[Value must not be in list](#value-must-not-be-in-list)  
[Value must be a number](#value-must-be-a-number)  
[Values must not be a number](#values-must-not-be-a-number)  
        </blockquote>
    </details>
    <details>
        <summary>Interpreting the Results</summary>
        <blockquote>
        </blockquote>
    </details>
    </blockquote>
</details>

## Display Rules
### Cell value evaluation
![Alt text](../images/rule_cellValueEval.png "Cell value evaluation")  
Evaluates the cell value given the javascript expression. Available parameters:  
* s (original value)
* rowData (the existing row containing rowData.cells which is the accessors)  

[Return to Top](#list-of-property-mapping-rules)  

### Maximum text length
![Alt text](../images/rule_maxTextLength.png "Maximum text length")  
Limits the length of the cell value text to a number of characters.  

[Return to Top](#list-of-property-mapping-rules)  

### Minimum text length
![Alt text](../images/rule_minTextLength.png "Minimum text length")  
The number of characters in the cell value must be greater than the specified number.  

[Return to Top](#list-of-property-mapping-rules)  

### Number between
![Alt text](../images/rule_numberBetween.png "Number between")  
Converts cell value to a number and evaluates if number is within a range of values. Ignores text listed in Ignore text textbox.  

[Return to Top](#list-of-property-mapping-rules)  

### Text length must be between
![Alt text](../images/rule_textLengthBetween.png "Text length must be between")  
The number of characters in the cell value must be between the lower and upper limit.  

[Return to Top](#list-of-property-mapping-rules)  

## Import/Export Rules
### Append text
![Alt text](../images/rule_appendText.png "Append Text")  
Adds the specified text to the end of the cell value.  
Example:  
* Cell value: "this"
* Rule value: "-item" (applied to all cells in column)
* Final value: "this-item"  

[Return to Top](#list-of-property-mapping-rules)  

### Calculate Number
![Alt text](../images/rule_calcNumber.png "Calculate Number")  
Uses the cell value and performs a calculation. The result of the calculation replaces the cell value.  
Example:
* Cell value: .07
* Rule value: n * 100
* Final value: 7 (.07 * 100)

[Return to Top](#list-of-property-mapping-rules)  

### Cell value manipulation
![Alt text](../images/rule_cellValueMani.png "Cell value manipulation")  
Manipulates (and returns the result of) the cell value given the javascript expression. Available parameters:  
* s (original value)
* rowData (the existing row containing rowData.cells which is the accessors)  

[Return to Top](#list-of-property-mapping-rules)  

### Format as decimal number
![Alt text](../images/rule_formatDecNum.png "Format as decimal number")  
Converts the cell value to a number and adds the specified number of decimals. This formats the number as it is viewed and does not round it. Any text specified to be removed will be replaced/ignored during the number format.  

[Return to Top](#list-of-property-mapping-rules)  

### Parse JSON
![Alt text](../images/rule_parseJson.png "Parse JSON")  
Converts the cell value from text to a JSON object and returns the value given by the specified key. Supports nested key/values and arrays. You can use key.value[2].key to retrieve value for a given key.  

[Return to Top](#list-of-property-mapping-rules)  

### Prepend text
![Alt text](../images/rule_prependText.png "Prepend text")  
Adds the specified text to the beginning of the cell value.  

[Return to Top](#list-of-property-mapping-rules)  

### Replace text
![Alt text](../images/rule_replaceText.png "Replace text")  
Replaces any instances of the specified text with the new value.  

[Return to Top](#list-of-property-mapping-rules)  

### Round to nearest X
![Alt text](../images/rule_roundNearest.png "Round to nearest X")  
Rounds the number to the nearest specified digit. Supports integers only.  

[Return to Top](#list-of-property-mapping-rules)  

### Set cell value
![Alt text](../images/rule_setCellValue.png "Set cell value")  
Sets the cell value to the specified text.  

[Return to Top](#list-of-property-mapping-rules)  

### Set empty cells
![Alt text](../images/rule_setEmptyCells.png "Set empty cells")  
Set an empty (any cell that has whitespace or no value) cell value to the specified text.  

[Return to Top](#list-of-property-mapping-rules)  

### Text length must equal
![Alt text](../images/rule_textLengthEquals.png "Text length must equal")  
The number of characters in the cell value must be exactly the length specified.  

[Return to Top](#list-of-property-mapping-rules)  

### Text must be exactly
![Alt text](../images/rule_textExactMatch.png "Text must be exactly")  
The cell value must be an exact match with the specified text.  

[Return to Top](#list-of-property-mapping-rules)  

### Text must contain string
![Alt text](../images/rule_textContains.png "Text must contain string")  
The cell value must contain the specified text.  

[Return to Top](#list-of-property-mapping-rules)  

### Text must end with string
![Alt text](../images/rule_textEndWith.png "Text must end with string")  
The cell value must end with the specified string.  

[Return to Top](#list-of-property-mapping-rules)  

### Text must not be empty
![Alt text](../images/rule_textNotEmpty.png "Text must not be empty")  
The cell value must not be empty.  

[Return to Top](#list-of-property-mapping-rules)  

### Text must not contain string
![Alt text](../images/rule_textNotContains.png "Text must not contain string")  
The cell value must not contain the specified string.  

[Return to Top](#list-of-property-mapping-rules)  

### Text must not end with string
![Alt text](../images/rule_textNotEndWith.png "Text must not end with string")  
The cell value must not end with the specified string.  

[Return to Top](#list-of-property-mapping-rules)  

### Text must start with string
![Alt text](../images/rule_textStartWith.png "Text must start with string")  
The cell value must start with the specified string.  

[Return to Top](#list-of-property-mapping-rules)  

### Value must be in list
![Alt text](../images/rule_valueMustBeInList.png "Value must be in list")  
The cell value must match a value in a string list. Entries are separated by a comma.    

[Return to Top](#list-of-property-mapping-rules)  

### Value must not be in list
![Alt text](../images/rule_valueMustNotBeInList.png "Value must not be in list")  
The cell value must not match a value in a string list. Entries are separated by a comma.    

[Return to Top](#list-of-property-mapping-rules)

### Value must be a number
![Alt text](../images/rule_valueMustBeNumber.png "Value must be a number")  
The cell value must be a number.  

[Return to Top](#list-of-property-mapping-rules)  

### Value must not be a number
![Alt text](../images/rule_valueMustNotBeNumber.png "Value must not be a number")  
The cell value must not be a number.

[Return to Top](#list-of-property-mapping-rules)