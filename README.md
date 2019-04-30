# Arbitrary Base to Arbitrary Base Converter

***Allows the conversion of a value in a given `base(a)` to the corresponding value in some other `base(b)`.*** The symbols used in both the base-systems can be provided by the user.

## pip Install
`pip install change_base`

### Usage:
`change_base.change_base(value, initial_base, final_base, initial_base_symbols, final_base_symbols)`

### Description:
A value from a given set with `base = a` is converted to the equivalent value in some other `base = b`. 
*For example*, decimal values ***(Base10)*** can be transformed into Hex ***(Base16)*** or Octal ***(Base8)*** values.

Transformation is achieved by first converting to decimal equivalent and then to the final base version through the following 2 functions:
1. `base_to_decimal(val, base = 73, symbols = None)`
2. `decimal_to_base(d, base, symbols = None)`

In the `base_to_decimal` function, `val` is the original value (*inputted as a string*) with base = `base`. `symbols` is a list to pass custom symbols for the system.

In the `decimal_to_base` function, `d` represents the original decimal value and `symbols` list stores the symbols used for this system with base = `base`

The symbols used to represent the system can be provided as custom input e.g. a value `$$&$##` may belong to a system with base = *3* and symbols `#, &, $`. This value can be converted to a decimal equivalent by calling:
>`base_to_decimal("$$&$##", 3, ['#', '&', '$'])`

In case the symbol list is not provided, the default ordered symbol list is used up to maximum of ***(Base73)***. The 73 symbols used are (*in this order*):
***Digits* `(0-9)`, *Lowercase-Letters* `(a-z)`, *Uppercase-letters* `(A-Z)`, *Safe-symbols*** `[ $, -, _, ., +, !, *, ', (, ), , ]`

Thus, each of these symbols have a decimal equivalent = list index from *0* to *73* that is used for base conversion.

The two functions are combined in the definition of function `base_change`. Thus, to change some value *`'val'`* with base *`'ibase'`* and symbol set (in order) *`'isymbols'`* (***optional argument***) into the equivalent value in some base *'`fbase`'* and symbol set *'`fsymbols`'* (***optional argument***), call the function:
- `base_change(val, ibase, fbase, isymbols, fsymbols)` 

#### Example Usages:
- Converting from **Decimal** to **Binary**: `base_change('123',10,2)` -> `'1111011' #Output`
- Converting from **Binary** to **Decimal**:  `base_change('1111011',2,10)` -> `'123' #Output`
- Converting from **Decimal** to **Hex**: `base_change('123',10,16)` -> `'7b'`
- Converting from ***Base5*** (with default symbols `[0,1,2,3,4]`) to ***Base5*** (custom symbols `['t','w','i','s','t']`): `base_change('123',5,5,None,['t','w','i','s','t'])` -> `'wis'`
- Converting from ***Base5*** (with custom symbols `['t','w','i','s','t']`) to ***Base10*** (default symbols): `base_change('witsittitsisits',5,10,['t','w','i','s','t'],None)` -> `'9697104823'`
- Inverse of the last example: `base_change('9697104823',10,5,None,['t','w','i','s','t'])` -> `'witsittitsisits'`

**Note**:
- *The position of symbol in custom symbol list decides its decimal equivalent*
- *Default symbol list consists of only 73 symbols. Thus maximum base conversion with default symbols is upto Base73*
- *Since the apostrophe `'` sign is also usable as a default symbol, the input value strings should be enclosed with double quotes*
- *All outputs are generated as strings*
