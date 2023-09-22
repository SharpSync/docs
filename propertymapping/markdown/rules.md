# List of Property Mapping Rules
Property Mapping Rules are used to define the output format of the BOM data shown in SharpSync. When a rule is applied, all cells in a column mapped to a property will be evaluated. If the cell data does not fall within the rules applied, the cell will display an error color on its border, with a more detailed explanation in the cell overlay. Text rules are not case-sensitive unless otherwise specified. Hover over a cell to see the applied rules evaluated in the overlay. Click on list icon in the Rules column of the desired Property Mapping to begin. Below is a comprehensive list of seach Property Mapping Rule. Expand the Table of Contents and click a specific rule to jump to that rule. Learn more about Rule setup: [Configure Rules](propertymapping#configure-rules)  

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
<details>
    <summary>Example</summary>  
    
* Cell value: Description
* Rule value: 4
* Result: Fail - number of characters > rule.  
</details>

[Return to Top](#list-of-property-mapping-rules)  

### Minimum text length
![Alt text](../images/rule_minTextLength.png "Minimum text length")  
The number of characters in the cell value must be greater than the specified number.  
<details>
    <summary>Example</summary>  
    
* Cell value: Description
* Rule value: 4
* Result: Pass - number of characters > rule.  
</details>

[Return to Top](#list-of-property-mapping-rules)  

### Number between
![Alt text](../images/rule_numberBetween.png "Number between")  
Converts cell value to a number and evaluates if number is within a range of values, and ignores text listed in textbox.  
<details>
    <summary>Example</summary>  
     
* Cell value: 12.5 kg
* Rule values:
    * Min val: 1
    * Max val: 100
    * Ignore text: kg,Kg,g,mg,m,mm,each,L,ml,oz,fl
* Result: Pass - "kg" ignored, cell value between min\max.  
</details>

[Return to Top](#list-of-property-mapping-rules)  

### Text length must be between
![Alt text](../images/rule_textLengthBetween.png "Text length must be between")  
The number of characters in the cell value must be between the lower and upper limit.  
<details>
    <summary>Example</summary>  
    
* Cell value: Part
* Rule values:
    * Min length: 5
    * Max length: 15
* Result: Fail - number of characters outside of min/max range.  
</details>

[Return to Top](#list-of-property-mapping-rules)  

## Import/Export Rules
### Append text
![Alt text](../images/rule_appendText.png "Append Text")  
Adds the specified text to the end of the cell value.  
<details>
    <summary>Example</summary>  
     
* Cell value: this
* Rule value: -item (applied to all cells in column)
* Result: this-item  
</details>

[Return to Top](#list-of-property-mapping-rules)  

### Calculate Number
![Alt text](../images/rule_calcNumber.png "Calculate Number")  
Uses the cell value and performs a calculation. The result of the calculation replaces the cell value.  
<details>
    <summary>Example</summary>  
    
* Cell value: .07
* Rule value: n * 100
* Result: 7 (.07 * 100)
</details>

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
<details>
    <summary>Example</summary>  
     
* Cell value: 12.53 m
* Rule values:
    * Number of decimals: 4
    * Remove text: kg|Kg|g|mg|m|mm|each|L|ml|oz|fl
* Result: 12.5300
</details>

[Return to Top](#list-of-property-mapping-rules)  

### Parse JSON
![Alt text](../images/rule_parseJson.png "Parse JSON")  
Converts the cell value from text to a JSON object and returns the value given by the specified key. Supports nested key/values and arrays. You can use key.value[2].key to retrieve value for a given key.  

[Return to Top](#list-of-property-mapping-rules)  

### Prepend text
![Alt text](../images/rule_prependText.png "Prepend text")  
Adds the specified text to the beginning of the cell value.  
<details>
    <summary>Example</summary>  
    
* Cell value: 123
* Rule value: ABC-
* Result: ABC-123
</details>

[Return to Top](#list-of-property-mapping-rules)  

### Replace text
![Alt text](../images/rule_replaceText.png "Replace text")  
Replaces any instances of the specified text with the new value.  
<details>
    <summary>Example</summary>  
    
* Cell value: Hello, world
* Rule values:
    * Replace text: world
    * With text: there
* Result: Hello, there
</details>

[Return to Top](#list-of-property-mapping-rules)  

### Round to nearest X
![Alt text](../images/rule_roundNearest.png "Round to nearest X")  
Rounds the number to the nearest specified digit. Supports integers only.  
<details>
    <summary>Example</summary>  
    
* Cell value: 1234.5678 mm
* Rule values:
    * Round to nearest X: 2
    * Ignore text: kg|Kg|g|mg|m|mm|each|L|ml|oz|fl
* Result: 1234.57
</details>

[Return to Top](#list-of-property-mapping-rules)  

### Set cell value
![Alt text](../images/rule_setCellValue.png "Set cell value")  
Sets the cell value to the specified text.  
<details>
    <summary>Example</summary>  
    
* Cell value: Hello, world
* Rule value: Description
* Result: Description
</details>

[Return to Top](#list-of-property-mapping-rules)  

### Set empty cells
![Alt text](../images/rule_setEmptyCells.png "Set empty cells")  
Set an empty (any cell that has whitespace or no value) cell value to the specified text.  
<details>
    <summary>Example</summary>  
    
* Cell value is empty 
* Rule value: Description
* Result: Description  
</details>

[Return to Top](#list-of-property-mapping-rules)  

### Text length must equal
![Alt text](../images/rule_textLengthEquals.png "Text length must equal")  
The number of characters in the cell value must be exactly the length specified.  
<details>
    <summary>Example</summary>  
    
* Cell value: Description
* Rule value: 12
* Result: Fail - Description is only 11 characters
</details>

[Return to Top](#list-of-property-mapping-rules)  

### Text must be exactly
![Alt text](../images/rule_textExactMatch.png "Text must be exactly")  
The cell value must be an exact match with the specified text.  
<details>
    <summary>Example</summary>  
    
* Cell value: Description
* Rule value: Description1
* Result: Fail - Description1 does not match Description
</details>

[Return to Top](#list-of-property-mapping-rules)  

### Text must contain string
![Alt text](../images/rule_textContains.png "Text must contain string")  
The cell value must contain the specified text.  
<details>
    <summary>Example</summary>  
    
* Cell value: Final Description
* Rule value: Final
* Result: Pass - Cell value contains text "Final"
</details>

[Return to Top](#list-of-property-mapping-rules)  

### Text must end with string
![Alt text](../images/rule_textEndWith.png "Text must end with string")  
The cell value must end with the specified string.  
<details>
    <summary>Example</summary>  
    
* Cell value: Description
* Rule value: abc
* Result: Fail - Cell value does not have suffix of abc
</details>

[Return to Top](#list-of-property-mapping-rules)  

### Text must not be empty
![Alt text](../images/rule_textNotEmpty.png "Text must not be empty")  
The cell value must not be empty.  
<details>
    <summary>Example</summary>  
    
* Cell value: Description
* Result: Pass - Cell value is not empty
</details>

[Return to Top](#list-of-property-mapping-rules)  

### Text must not contain string
![Alt text](../images/rule_textNotContains.png "Text must not contain string")  
The cell value must not contain the specified string.  
<details>
    <summary>Example</summary>  
    
* Cell value: Description
* Rule value: rip
* Result: Fail - Cell value "Description" contains "rip"
</details>

[Return to Top](#list-of-property-mapping-rules)  

### Text must not end with string
![Alt text](../images/rule_textNotEndWith.png "Text must not end with string")  
The cell value must not end with the specified string.  
<details>
    <summary>Example</summary>  
    
* Cell value: Description
* Rule value: ion
* Result: Fail - Cell value "Description" ends with "ion"
</details>

[Return to Top](#list-of-property-mapping-rules)  

### Text must start with string
![Alt text](../images/rule_textStartWith.png "Text must start with string")  
The cell value must start with the specified string.  
<details>
    <summary>Example</summary>  
    
* Cell value: Description
* Rule value: Desc
* Result: Pass - Cell value "Description" begins with "Desc"
</details>

[Return to Top](#list-of-property-mapping-rules)  

### Value must be in list
![Alt text](../images/rule_valueMustBeInList.png "Value must be in list")  
The cell value must match a value in a string list. Entries are separated by a comma.    
<details>
    <summary>Example</summary>  
    
* Cell value: Desc
* Rule value: abc,def,ghi
* Result: Fail - Cell value "Desc" does not match any list value
</details>

[Return to Top](#list-of-property-mapping-rules)  

### Value must not be in list
![Alt text](../images/rule_valueMustNotBeInList.png "Value must not be in list")  
The cell value must not match a value in a string list. Entries are separated by a comma.    
<details>
    <summary>Example</summary>  
    
* Cell value: Desc
* Rule value: abc,def,ghi
* Result: Pass - Cell value "Desc" does not match any list value
</details>

[Return to Top](#list-of-property-mapping-rules)

### Value must be a number
![Alt text](../images/rule_valueMustBeNumber.png "Value must be a number")  
The cell value must be a number.  
<details>
    <summary>Example</summary>  
    
* Cell value: 12.5a
* Result: Fail - Cell value contains non-numeric character "a"
</details>

[Return to Top](#list-of-property-mapping-rules)  

### Value must not be a number
![Alt text](../images/rule_valueMustNotBeNumber.png "Value must not be a number")  
The cell value must not be a number.
<details>
    <summary>Example</summary>  
    
* Cell value: 12.5a
* Result: Pass - Cell value contains non-numeric character "a"
</details>

[Return to Top](#list-of-property-mapping-rules)