# JSON - JavaScript ==Object== Notation
- Separators: ~~Newline (only to improve readability)~~, Squiggly braces, Comma (elements), Colon (Key-value pairs)
- Data types - [Json valid data types](https://www.w3schools.com/js/js_json_datatypes.asp)
	- Core types: 
		- String
		- Number
		- Boolean
		- Null
	- Complex types: 
		- Array 
		- Object (Dictionary in Python/ Key-value pairs), 

E.g., Array
``` 
{"employees":["John", "Anna", "Peter"]}
```
## Advantages ($\{\text{Json} - \text{Yaml}\}$):
### 1. Compact storage
### 2. Universality
- JSON was created in 1999, while YAML was created in 2001.
### 3. Merge friendliness (e.g., Git) 
- Reason: Lack of "whitespace" (Indentation, Tabs, Newlines)

**YAML - Indentation determines a nested data structure.**
``` 
person:
  name: Alice
  age: 30
  city: New York
```
> Change indentation structure ...
```
person:
  name: Alice
age: 30
  city: New York
```
> Result: Merge conflict!

**JSON - Braces determines a nested data structure**
```
{
  "name": "John Doe",
  "age": 30,
  "city": "New York",
  "email": "johndoe@example.com"  // Added new key-value pair
}
```
> Change indentation structure  ...
```
{ "name": "John Doe",
  "age": 35,   // Modified value
"city": "New York"
}
```
> Result: Merged!
```
{
  "name": "John Doe",
  "age": 30,
  "city": "New York",
  "email": "johndoe@example.com"
}
```
- This is because the Merge tool focuses on key-value pairs, disregarding the whitespace changes.

----
# YAML: Yet Another Markup Language
- Separators: Newline (elements. A replacement of json's squiggly braces), Indent, Dash (for lists), Colon (key-value pairs)
- Data types: [yaml data types](https://www.javatpoint.com/yaml-data-types)
	- Core types: 
		- String
		- Number
		- Boolean 
		- Null
		- Date
	- Complex types: 
		- Array/ Lists 
		- Key-value pairs (separated by indents (in json: squiggly braces) and newlines (in json: comma))

E.g., Array/ List
```
items: [6, 7, 8, 9, 10]
name: [six, seven, eight, nine, ten]
``` 
or 
```
items:   
- 6  
- 7  
- 8
```

## Advantages ($\{\text{Yaml} - \text{Json}\}$):
### 1. Indentation-based structure
### 2. More data types (`null`, `dates`)
### 3. Comments (`#`)
### 4. Aliases (`*`)
### 5. Anchor
### 6. Tags

