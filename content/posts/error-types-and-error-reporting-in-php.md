+++
title = 'Error types and error reporting in PHP'
date = 2022-12-04T00:00:00+00:00
draft = false
tags = ['php', 'errors', 'debugging', 'error-handling']
+++

It is important to know about error types in PHP. With this knowledge, it would be easier to find and solve errors. Basically, we have 4 types of errors in PHP and I will show them to you with examples.

## 1. Notice
PHP is not sure about whether it is an error or not!

## 2. Warning
An error that is important and should be fixed but does not stop code execution.

```php
include("external_file.php");

Warning: include(external_file.php): Failed to open stream: No such file or directory in /Users/hamid/Codes/error.php on line 4
```

## 3. Parse error
When the compiler is unable to parse your code correctly. For example, when a `;` is missing.

```php
if ($a == 1) {
    echo "something!"
}

Parse error: syntax error, unexpected token "}", expecting "," or ";" in /Users/hamid/Codes/error.php on line 12
```

## 4. Fatal error
When you have a critical error. **Your code execution will be halted**.

```php
$c = 1 / 0;

Fatal error: Uncaught DivisionByZeroError: Division by zero in /Users/hamid/Codes/error.php:7
Stack trace:
#0 {main}
  thrown in /Users/hamid/Codes/error.php on line 7
```

## Error reporting in PHP
You can ask PHP to show specific types of errors like these:

```php
// Turn off all error reporting
error_reporting(0);

// Report simple running errors
error_reporting(E_ERROR | E_WARNING | E_PARSE);

// Reporting E_NOTICE can be good too (to report uninitialized
// variables or catch variable name misspellings ...)
error_reporting(E_ERROR | E_WARNING | E_PARSE | E_NOTICE);

// Report all errors except E_NOTICE
// This is the default value set in php.ini
error_reporting(E_ALL ^ E_NOTICE);

// Report all PHP errors (see changelog)
error_reporting(E_ALL);

// Report all PHP errors
error_reporting(-1);

// Same as error_reporting(E_ALL);
ini_set('error_reporting', E_ALL);
```

Thank you for reading...
