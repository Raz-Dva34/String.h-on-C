# Implementation of the string.h library with additions.
## Introduction

Implementation of the string.h library in the C programming language with some additions (with its own implementation of the sprintf and sscanf functions). The string.h library is the main C library for string processing.

## Chapter III

## Part 1. Implementation of the string.h library functions

- The library is developed in the C language of the C11 standard using the gcc compiler;
- The library code, including header files, makefiles and the library itself is located in the src folder in the develop branch;
- Unit tests check the results of the implementation by comparing it with the implementation of the standard string.h library;
- A Makefile is provided for building the library and tests (with the all, clean, test, s21_string.a, gcov_report targets);
- The gcov_report target generates a gcov report as an html page. For this, unit tests must be run with gcov flags;
- No copying of the implementation and use of the standard string.h library and other string processing libraries everywhere except unit tests;
- Functions work with z-strings of single-byte ASCII characters.

## Part 2. Partial implementation of the sprintf function

- partial formatting is supported:
- Specifiers: c, d, f, s, u, %
- Flags: -, +, (space)
- Width: (number)
- Precision: .(number)
- Length: h, l

## Part 3. Additional. Implementation of some format modifiers of the sprintf function

- The following additional format modifiers are supported:

- Specifiers: g, G, e, E, x, X, o, p
- Flags: #, 0
- Width: *
- Precision: .*
- Length: L

## Part 4. Advanced. Implementation of the sscanf function

- Full formatting is supported (including flags, width, precision, modifiers, and conversion types).

## Part 5. Advanced. Implementation of special string processing functions

## Chapter II

## Information

The C programming language contains a set of functions implementing operations with strings (character strings and byte strings) in its standard library. It supports such operations as: copying, concatenation, marking and searching. For character strings, the standard library has a rule that strings must be terminated with a terminating null character: a string of n characters is represented as an array of n + 1 elements, the last of which is the "NULL" character. \
The only support for strings in the C programming language itself is that the compiler converts quoted string constants to null-terminated strings.

### string.h Types

| # | Variable | Description |
| ------ | ------ | ------ |
| 1 | size_t | An unsigned integer type that is the result of the sizeof keyword.

### string.h Macros

| № | Macro | Description |
| ------ | ------ | ------ |
| 1 | NULL | Macro that is the value of the null pointer constant.

### string.h Functions

| № | Function | Description |
| ------ | ------ | ------ |
| 1 | void *memchr(const void *str, int c, size_t n) | Searches for the first occurrence of the character c (unsigned type) in the first n bytes of the string pointed to by str. |
| 2 | int memcmp(const void *str1, const void *str2, size_t n) | Compares the first n bytes of str1 and str2. |
| 3 | void *memcpy(void *dest, const void *src, size_t n) | Copies n characters from src to dest. |
| 4 | void *memset(void *str, int c, size_t n) | Copies the character c (unsigned) to the first n characters of the string pointed to by str. |
| 5 | char *strncat(char *dest, const char *src, size_t n) | Appends the string pointed to by src to the end of the string pointed to by dest, up to n characters long. |
| 6 | char *strchr(const char *str, int c) | Searches for the first occurrence of the character c (unsigned) in the string pointed to by str. |
| 7 | int strncmp(const char *str1, const char *str2, size_t n) | Compares at most the first n bytes of str1 and str2. |
| 8 | char *strncpy(char *dest, const char *src, size_t n) | Copies up to n characters from the string pointed to by src to dest. |
| 9 | size_t strcspn(const char *str1, const char *str2) | Calculates the length of the initial segment of str1, which consists entirely of characters not included in str2. |
| 10 | char *strerror(int errnum) | Searches the internal array for the error number errnum and returns a pointer to a string with the error message. You must declare macros containing arrays of error messages for mac and linux operating systems. Error descriptions are in the original library. The current OS is checked using directives. |
| 11 | size_t strlen(const char *str) | Calculates the length of the string str, not including the terminating null character. |
| 12 | char *strpbrk(const char *str1, const char *str2) | Finds the first character in str1 that matches any character specified by str2. |
| 13 | char *strrchr(const char *str, int c) | Searches for the last occurrence of the character c (unsigned) in the string pointed to by str. |
| 14 | char *strstr(const char *haystack, const char *needle) | Finds the first occurrence of the entire string needle (not including the terminating null character) that appears in haystack. |
| 15 | char *strtok(char *str, const char *delim) | Splits str into a series of tokens separated by delim. |

### sprintf and sscanf

- int sscanf(const char *str, const char *format, ...) - reads formatted input from a string.
- int sprintf(char *str, const char *format, ...) - sends formatted output to the string pointed to by str.

where:
- str is a C string that the function treats as a source for retrieving data;
- format is a C string containing one or more of the following: a whitespace character, a non-whitespace character, and format specifiers. The format specifier for the printing functions follows the prototype: %[flags][width][.precision][length]specifier. The format specifier for the scanning functions follows the prototype: %[*][width][length]specifier.

### sprintf and sscanf Specifiers

| # | Specifier | Result of sprintf | Result of sscanf |
| --- | --- | --- |
| 1 | c | Character | Character |
| 2 | d | Signed decimal integer | Signed decimal integer |
| 3 | i | Signed decimal integer | Signed integer (can be decimal, octal, or hexadecimal) |
| 4 | e | Scientific notation (mantissa/exponent) using the e symbol (numbers must match up to e-6) | Decimal floating point or scientific notation (mantissa/exponent) |
| 5 | E | Scientific notation (mantissa/exponent) using the E symbol | Decimal floating point or scientific notation (mantissa/exponent) |
| 6 | f | Decimal floating point | Decimal floating point or scientific notation (mantissa/exponent) |
| 7 | g | Uses the shortest possible decimal representation | Decimal floating point or scientific notation (mantissa/exponent) |
| 8 | G | Uses the shortest possible decimal representation | Decimal floating point or scientific notation (mantissa/exponent) |
| 9 | o | Unsigned octal | Unsigned octal |
| 10 | s | Character string | Character string |
| 11 | u | Unsigned decimal integer | Unsigned decimal integer |
| 12 | x | Unsigned hexadecimal integer | Unsigned hexadecimal integer (any letters) |
| 13 | X | Unsigned hexadecimal integer (uppercase letters) | Unsigned hexadecimal integer (any letters) |
| 14 | p | Pointer address | Pointer address |
| 15 | n | Number of characters printed before %n | Number of characters read before %n |
| 16 | % | % character | % character |

### sprintf Flags

| # | Flag | Description |
| --- | --- | --- |
| 1 | - | Left-aligned within the specified field width. Right-aligned is the default (see the width subspecifier). |
| 2 | + | Forces an explicit plus or minus sign (+ or -) even for positive numbers. By default, only negative numbers are preceded by a - sign. |
| 3 | (space) | If no sign is to be printed, a space is inserted before the value. |
| 4 | # | When used with the o, x, or X specifiers, 0, 0x, or 0X is inserted before the number, respectively (for values ​​other than zero). When used with e, E, and f, causes the written output to contain a decimal point even if no digits follow. By default, no decimal point is written if no digits follow. When used with g or G, the result is the same as with e or E, but trailing zeros are not removed. |
| 5 | 0 | Pads the number on the left with zeros (0) instead of spaces where the width specifier is specified (see the width subspecifier). |

### sprintf and sscanf Width

| # | Width | Description |
| --- | --- | --- |
| 1 | (number) | Minimum number of characters to print. If the output value is shorter than this number, the result is padded with spaces. The value is not truncated even if the result is longer. |
| 2 | * | In sprintf, * means that the width is not specified in the format string, but as an additional integer argument preceding the argument to be formatted. In sscanf, * after % and before the format specifier reads data of the specified type but suppresses its assignment. |

### sprintf Precision

| # | .precision | Description |
| --- | --- | --- |
| 1 | .number | For integer specifiers (d, i, o, u, x, X), the precision specifies the minimum number of digits to write. If the value to write is shorter than this number, the result is padded with leading zeros. The value is not truncated even if the result is longer. A precision of 0 means that for a value of 0, no characters are written. For specifiers e, E, and f, this is the number of digits to be printed after the decimal point. For specifiers g and G, this is the maximum number of significant digits to be printed. For s, this is the maximum number of characters to print. By default, all characters are printed until a terminating zero is encountered. For type c, − has no effect. If precision is not specified for the e, E, f, g, and G specifiers, it defaults to 6. If precision is not specified for the other specifiers, it defaults to 1. If no number is specified (no explicit precision value), it defaults to 0. |
| 2 | .* | The precision is not specified in the format string, but as an additional integer argument preceding the argument to be formatted. |

### sprintf and sscanf Length

| # | Length | Description |
| --- | --- | --- |
| 1 | h | The argument is interpreted as a short int or unsigned short int (applies only to the integer specifiers: i, d, o, u, x, and X). |
| 2 | l | The argument is interpreted as a long int or unsigned long int for the integer specifiers (i, d, o, u, x, and X), and as a wide character or wide character string for the c and s specifiers. |
| 3 | L | The argument is interpreted as a long double (applies only to the floating-point specifiers − e, E, f, g, and G). |

### Special string handling functions (inspired by the C# String class)

| # | Function | Description |
| ------ | ------ | ------ |
| 1 | void *to_upper(const char *str) | Returns a copy of the string (str) converted to uppercase. If any error occurs, NULL should be returned. |
| 2 | void *to_lower(const char *str) | Returns a copy of the string (str) converted to lowercase. On error, return NULL. |
| 3 | void *insert(const char *src, const char *str, size_t start_index) | Returns a new string with the specified string (str) inserted at the specified position (start_index) in the given string (src). On error, return NULL. |
| 4 | void *trim(const char *src, const char *trim_chars) | Returns a new string with all leading and trailing occurrences of the specified characters (trim_chars) removed from the given string (src). On error, return NULL. |
