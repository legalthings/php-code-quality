# Legal Things PHP coding standard


## PSR-1

LegalThings follows the [PSR-1 basic coding standard](http://www.php-fig.org/psr/psr-1/) with the following exceptions:

### [3. Namespace and Class Names](3.-namespace-and-class-names)

[Project packages](https://getcomposer.org/doc/04-schema.md#type) SHOULD NOT use a vendor namespace.

[Library packages](https://getcomposer.org/doc/04-schema.md#type) MUST use the vendor namespace: "LegalThings".

Library packages must follow the [PSR-4](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md) autoloading standard.


## PSR-2

LegalThings follows the [PSR-2 coding style guide](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md) with the following exceptions:

### [2. General](http://www.php-fig.org/psr/psr-2/#2.-general)

#### [2.3. Lines](http://www.php-fig.org/psr/psr-2/#2.3.-lines)

Lines MAY be longer than 80 characters; Lines SHOULD NOT be longer than 120 characters; lines longer than that SHOULD be split into multiple subsequent lines of no more than 120 characters each.

### [5. Control Structures](http://www.php-fig.org/psr/psr-2/#5.-control-structures)

The body of each structure MUST be enclosed by braces, with the exception of an `if` structure.

#### [5.1. `if`, `elseif`, `else`](http://www.php-fig.org/psr/psr-2/#5.1.-if,-elseif,-else)

An `if` structure MUST be omit braces when the body is on the same line as the `if` statement. The `if` structure MUST include braces when the body is on the next line after the `if` statement.

    if ($expr) echo 'Expression is true';

An `if` structure SHOULD be on a single line, if the complete structure is equal to or shorter than 80 characters.


## Additional rules

### 1. Document blocks

Each class MUST have a [document blocks](https://en.wikipedia.org/wiki/PHPDoc).

Each public property MUST have a document block with an `@var` tag. Each protected of private property SHOULD have a document block with an `@var` tag.

Each function and method MUST have a document block with `@param` tags for all parameters and an `@return` tag if a value is returned.

Variables document block should be as precise as possible. Examples:

 * `@return string|boolean|array` is preferred to `@var mixed`
 * `@var Foo|Bar` is preferred to `@var object`
 * `@var Foo[]` is preferred to `@var array`

A document block for a method that follow the [fluent interface pattern](https://en.wikipedia.org/wiki/Fluent_interface) SHOULD have `@return $this`.

### 2. Keywords

The keywords `AND` and `OR` SHOULD NOT be used. Instead use `&&` and `||`.

### 3. Classes

Properties and methods SHOULD be public or protected, not private.

Classes SHOULD NOT have simple getter and setter functions as replacement for public properties.

### 4. Control Flow

Assertions and alternative flows SHOULD come before the normal flow to reduce nesting.

**Example of correct flow:**

```php
function fizz($a) {
    if (!$a) return;

    foo();
    bar();
}
```

**Example of incorrect flow:**

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
