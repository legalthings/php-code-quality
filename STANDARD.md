# Legal Things PHP coding standard

This guide defines a set of rules aimed to create consistent code across all PHP projects of Legal Things.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.

The term Project is used for deliverables that are typically served by a web server or run on the command line. The term Library is used for a collection of classes and/or functions which is consumed by projects or other libraries.


## 1. PSR-1

LegalThings follows the [PSR-1 basic coding standard](http://www.php-fig.org/psr/psr-1/) with an exception on [Section 3 - Namespace and Class Names](3.-namespace-and-class-names):

Projects SHOULD NOT use a vendor namespace.

Libraries MUST use the vendor namespace: "LegalThings".

Libraries must follow the [PSR-4](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md) autoloading standard.


## 2. PSR-2

LegalThings follows the [PSR-2 coding style guide](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md) with a number of exceptions.

### 2.1. Exception on [Section 2.3 - Lines](http://www.php-fig.org/psr/psr-2/#2.3.-lines)

Lines MAY be longer than 80 characters; Lines SHOULD NOT be longer than 120 characters; lines longer than that SHOULD be split into multiple subsequent lines of no more than 120 characters each.

## 3. General

### 3.1. Keywords

The keywords `AND` and `OR` SHOULD NOT be used. Instead use `&&` and `||`.

### 3.2. File length

PHP files SHOULD be 500 lines or less.

### 3.3. Function length

Functions and methods SHOULD be 30 lines or less.

### 3.4. Alternative syntax for control structures

The [alternative syntax for control structures](http://php.net/manual/en/control-structures.alternative-syntax.php) MUST NOT be used in files containing only PHP.


## 4. Directory structure

Directories MAY be omited if they're not used.

Cache, user generated content and external (composer and bower) libraries SHOULD be excluded from distribution.

### 4.1. Projects

A project SHOULD follow the following directory structure:

- bin - Executables and command line scripts
- cache - Cached files, may be deleted at any time
- config - Configuration files
- controllers - Controller classes
- dev - Development resources
- lib - Library classes and functions
- locale - Translation files
- models - Model classes
- static - User generated content _(development environment only)_
- tests - Unit and API tests
- vendor - Installed [composer](http://getcomposer.org) packages
- views - View templates
- www - Document root
  - bower_components - Installed [bower](http://bower.io) packages
  - css - Stylesheets
  - img - Images _(except user generated content)_
  - js - JavaScript

On staging and production environments, user generated content MUST be stored on secure, persistent, redundant and backed-up storage (e.g. [AWS S3](https://aws.amazon.com/s3/) or [Elastic file system](http://aws.amazon.com/efs/)).

### 4.1 Libraries

A library SHOULD follow the following directory structure:

- bin - Executables and command line scripts
- dev - Development resources, eg a database dump
- locale - Translation files
- src - Library classes and functions
- tests - Unit and API tests
- vendor - Installed [composer](http://getcomposer.org) packages

## 5. Classes

Properties and methods SHOULD be public or protected, not private.

Classes SHOULD NOT have simple getter and setter functions as replacement for public properties.

## 6. Nesting

### 6.1. Nested blocks

Within the body of a function or method, there SHOULD be no more than 4 levels of nesting. With this many levels of nesting, introduce a new function rather than to use more nested blocks.

```php
function foo() {
    foreach (/* ... */) {
        if (/* ... */) {
            while (/* ... */) {
                if (/* ... */) {
                    // No more nested blocks
                }
            }
        }
    }
}
```

### 6.2. Control flow

Assertions and alternative flows SHOULD come before the normal flow to reduce nesting.

**Examples of good flow:**

```php
function fizz($a) {
    if (!$a) return;

    foo();
    bar();
}
```

```php
function buzz($b) {
    while ($b as $i) {
        if (!$i) continue;
       
        $i->foo();
        $i->bar();
    }
}
```

**Examples of bad flow, with unnecessary nesting:**

```php
function fizz($a) {
    if ($a) {
        foo();
        bar();
    }
}
```

```php
function fizz($a) {
    if ($a) {
        foo();
    } else {
        return;
    }
    
    bar();
}
```

```php
function buzz($b) {
    while ($b as $i) {
        if ($i) {
            $i->foo();
            $i->bar();
        }
    }
}
```


## 7. Documentation

### 7.1. README

Each project MUST include a `README.md` document in the root folder.

The README document SHOULD include the title of and a short description the project.

The README document SHOULD include a list of prerequisites.

The README document SHOULD include installation instructions.

The README document SHOULD include API documentation or a link to the API documententation.

The README document MAY include additional information which can be useful for developers.

### 7.2. Document blocks

Each class MUST have a [document blocks](https://en.wikipedia.org/wiki/PHPDoc).

Each public property MUST have a document block with an `@var` tag. Each protected of private property SHOULD have a document block with an `@var` tag.

Each function and method MUST have a document block with `@param` tags for all parameters and an `@return` tag if a value is returned.

Variables document block SHOULD be as precise as possible. Examples:

 * `@return string|boolean|array` is preferred to `@var mixed`
 * `@var Foo|Bar` is preferred to `@var object`
 * `@var Foo[]` is preferred to `@var array`

A document block for a method that implements the [fluent interface pattern](https://en.wikipedia.org/wiki/Fluent_interface) SHOULD state `@return $this`.

## 8. Testing

### 8.1. Unit tests
 
Projects and libraries SHOULD include [unit tests](http://codeception.com/docs/06-UnitTests), runnable by codeception.

Each library class and function SHOULD be covered by unit tests, with a code coverage of 90% or more.

Each model class SHOULD be covered by unit tests, with a code coverage of 90% or more.

A controller class SHOULD NOT be covered by unit tests.

### 8.2. API tests

Projects with a web service API SHOULD include [API tests](http://codeception.com/docs/10-WebServices), runnable by codeception.

Controller methods related to a web service SHOULD be covered by unit tests, with a code covereage of 90% or more.

### 8.3. Functional tests

Projects with a user interface SHOULD have a test plan for manual acceptance testing.

Controller methods not related to a web service MAY be covered by automated [functional tests](http://codeception.com/docs/05-FunctionalTests), runnable by codeception.

