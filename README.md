# Str Case Util
A lightweight utility library for working with various string casing.

## Supported Cases
| Example     | Case Names                                                | 
|-------------|-----------------------------------------------------------|
| HelloWorld  | Pascal Case<br/>Capital Camel Case                        |
| helloWorld  | Camel Case                                                |
| helloworld  | Flat Case<br/>Mumble Case                                 |
| HELLOWORLD  | Upper Flat Case                                           |
| Hello World | Title Case                                                |
| Hello world | Sentence Case                                             |
| hello world | Lower Case                                                |
| HELLO WORLD | Upper Case                                                |
| hello_world | Snake Case<br/>C Case                                     |
| HELLO_WORLD | Screaming Snake Case<br/>Constant Case<br/>Macro Case     |
| Hello-World | Train Case                                                |
| hello-world | Kebab Case<br/>Caterpillar Case<br/>CSS Case<br>Lisp Case |
| HELLO-WORLD | COBOL Case                                                |

## Features
Each of the above may be accessed within the `Case` Enum
```python
from case_util import Case
```

The `Case` Enum contains functions to format a `str`
```python
Case.SNAKE_CASE.format("Hello World")  # output = hello_world
```
and also to determine if a `str` is said format
```python
Case.CAMEL_CASE.is_formatted("MyClassName")  # output = False
Case.PASCAL_CASE.is_formatted("MyClassName")  # output = True
```
In addition, a class method is available to detect the format of a `str`
```python
Case.detect_format("my-test-string")  # output = Case.KEBAB_CASE
```

## Additional Functionality
While not intended to be used externally, the following functions are available if they are of use.
### Split String Into Words
```python
import case_util

words = case_util.words_of("MyFormattedClassName")
# output = ["My", "Formatted", "Class", "Name"]
```
### Word List Manipulation
If you already have a list of words, you may preform the following actions on each
1. `case_util.capitalize(words)`
2. `case_util.camel(words)` - Capitalizes all but the 1st word
3. `case_util.sentence(words)` - Capitalizes only the 1st word
4. `case_util.lower(words)`
5. `case_util.upper(words)`

## Caveats
Due to the nature of the various string formats, the correct case cannot always be detected.

### Flat Case Trumps All
A single word such as `name` will be detected as Flat Case. Similarly, `NAME` will be Upper Flat Case.
While this functionality may seem obvious, it gets more nuanced.
Perhaps the author wrote it in Camel Case or Snake Case which becomes clear when expanded: `nameClass` or `var_name`.
Without input from the original author, it is impossible to know for certain.

### Acronyms
Acronyms/abbreviations are treated as a single word. So `MyAPIClass` converted to snake case would be `my_api_class`.
Related, acronym case is not preserved which means `MyAPIClass` converted to camel case would result in `myApiClass`.
This unfortunately means that the format of such strings will not be properly detected.

### Multiple Cases Detected
Some strings, such as `the quick_brown-fox` could be one of many formats depending on the intended delimiter.
In these scenarios, `None` is returned

### Special Characters
This library was created with class/variable names in mind. Therefore, extensive test has not been conducted using special characters.
When it comes to Camel Case and Pascal Case, numbers are designed to be seen as uppercase.
This may result in unwanted behavior if placing numbers within the middle of words.
All other special characters are intended to be treated as lowercase.

### Additional Language Support
No design/testing has been conducted for characters outside of ASCII.
