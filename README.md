# groovin_string_masks

A string formatter and validator based on masks. Forked from EmersonMoura's 'string_mask' package as it appears to be abandonded.

## SPECIAL MASK CHARACTERS

Character | Description
--- | ---
`0` | Any numbers
`9` | Any numbers (Optional)
`#` | Any numbers (recursive)
`A` | Any alphanumeric character
`a` | Any alphanumeric character (Optional) __Not implemented yet__
`S` | Any letter
`U` | Any letter (All lower case character will be mapped to uppercase)
`L` | Any letter (All upper case character will be mapped to lowercase)
`$` | Escape character, used to escape any of the special formatting characters.

### Special characters types

 - **Optional characters:** Used to parse characters that cold exist in the source string or not. See [Date and time](#date-and-time).

 - **Recursive characters:** Used to parse patterns that repeat in the end or in the start of the source string. See [Two decimal number with thousands separators](#two-decimal-number-with-thousands-separators)

> _Note: Any character of the mask positioned after a recursive character will be handled as a non special character._

## USAGE

 **Use it creating an mask instance with the StringMask contructor:**

```dart
/**
 * - optionsObject parameter is optional in the constructor
 * - apply will return the a masked string value
 * - validate will return `true` if the string matchs the mask
 */
var mask = new StringMask('some mask', options: new MaskOptions()); //optionsObject is optional
var maskedValue = mask.apply('some value string');
var isValid = mask.validate('some value string to validate');
```

**Or by the static interface:**

```dart
/**
 * - optionsObject parameter is optional in all methods
 * - apply will return the a masked string value
 * - validate will return `true` if the string matchs the mask
 * - process will return a object: {result: <maskedValue>, valid: <isValid>}
 */
var maskedValue = StringMask.apply_('some value string', 'some mask', optionsObject); 
var isValid = StringMask.validate_('some value string', 'some mask', optionsObject);
var result = StringMask.process_('some value string', 'some mask', optionsObject);
```

### Some masks examples

#### Number

```dart
    var maskOptions = new MaskOptions()
      ..reverse = true;

    var formatter = new StringMask("#0", options: maskOptions);
    var result = formatter.apply('123'); // 123
```

#### Two decimal number with thousands separators

```dart
    var maskOptions = new MaskOptions()
      ..reverse = true;

    var formatter = new StringMask('#.##0,00', options: maskOptions);
    var result = formatter.apply('100123456'); // 1.001.234,56
    var result2 = formatter.apply('6'); // 0,06
```

#### Phone number

```dart
    var formatter = new StringMask('+00 (00) 0000-0000');
    var result = formatter.apply('553122222222'); // +55 (31) 2222-2222
```

#### Percentage

```dart
    var maskOptions = new MaskOptions()
      ..reverse = true;

    var formatter = new StringMask('#.##0,00', options: maskOptions);
    var result = formatter.apply('001'); // 0,01%
```

#### Brazilian CPF number

```dart
    var formatter = new StringMask('000.000.000-00');
    var result = formatter.apply('12965815620'); // 129.658.156-20
```

#### Date and time

```dart
    var formatter = new StringMask('90/90/9900');
    var result = formatter.apply('1187'); // 1/1/87
```

#### Convert Case

```dart
    var formatter = new StringMask('UUUUUUUUUUUUU');
    var result = formatter.apply('To Upper Case'); // TO UPPER CASE
```

```dart
    var formatter = new StringMask('LLLLLLLLLLLLL');
    var result = formatter.apply('To Lower Case'); // to lower case
```

#### International Bank Number

```Dart
    var formatter = new StringMask('UUAA AAAA AAAA AAAA AAAA AAAA AAA');
    var result = formatter.apply('FR761111BBBB69410000AA33222');
	// result: FR76 1111 BBBB 6941 0000 AA33 222
```

## LICENSE

Licensed under the MIT license.


## Getting Started with Flutter

For help getting started with Flutter, view our online [documentation](https://flutter.io/).

For help on editing package code, view the [documentation](https://flutter.io/developing-packages/).
