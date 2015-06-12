# PHP code quality

## Coding standard

Please read the [Legal Things PHP coding standard](https://github.com/legalthings/php-coding-standard/STANDARD.md).


## Installation

All PHP projects of Legal Things should include this package. It can be installed through composer.

    composer require --dev legalthings/php-code-quality


## Toolchain

### Codeception
[Codeception](http://codeception.com/) is BDD-style PHP testing build on PHPUnit. It supports Unit testing, API testing and Acceptance testing.

    bin/codecept

### vfsStream
[vfsStream](https://github.com/mikey179/vfsStream) is a stream wrapper for a virtual file system that may be helpful in unit tests to mock the real file system.

### PHP_CodeSniffer
[phpcs](https://github.com/squizlabs/PHP_CodeSniffer) tokenises PHP files and detects violations of a defined set of coding standards. It is an essential development tool that ensures your code remains clean and consistent.
This package comes with a custom ruleset which embodies the Legal Things PHP coding standard.

    bin/phpcs . --standard=vendor/legalthings/php-code-quality --ignore=/bin/,/vendor/,/tests/

