# Omroep Gelderland PHP Coding Standard

This package provides the official PHP_CodeSniffer standard for Omroep Gelderland.

It is the organisation standard for all PHP code within Omroep Gelderland and is used to keep projects consistent,
readable, and aligned with modern PHP conventions.

The ruleset builds on PSR-12 and adds a number of opinionated quality checks from the Generic and Slevomat coding
standards to enforce clean code, consistent structure, and maintainable PHP.

## Installation

Install the package as a development dependency:

```bash
composer require --dev omroepgelderland/php-coding-standard
```

This package is registered as a PHP_CodeSniffer standard, so Composer and the PHP_CodeSniffer installer should
automatically make it available to PHPCS.

## Usage

Run the standard against your project:

```bash
vendor/bin/phpcs --standard=OmroepGelderland .
```

Auto-fix issues where possible:

```bash
vendor/bin/phpcbf --standard=OmroepGelderland .
```

You can also reference the standard in a project-level PHPCS ruleset:

If a project needs to allow a narrow exception, you can override specific sniffs in the project ruleset.

A common override is multiple classes in a single file, for example for exception classes.

When adding exceptions for legacy code structures such as inline HTML or files with both executable code and function
definitions, make these cases generate a warning instead of excluding them from the standard.

```xml
<?xml version="1.0"?>
<ruleset
    name="kijkcijfersimporter"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:noNamespaceSchemaLocation="https://schema.phpcodesniffer.com/phpcs.xsd"
>
    <!-- Define which files to check -->
    <arg name="extensions" value="php" />
    <file>./</file>
    <exclude-pattern>*/node_modules/*</exclude-pattern>
    <exclude-pattern>*/vendor/*</exclude-pattern>

    <rule ref="OmroepGelderland" />

    <!-- Allow multiple classes in one file -->
    <rule ref="PSR1.Classes.ClassDeclaration.MultipleClasses">
        <exclude-pattern>*/src/php/exceptions\.php$</exclude-pattern>
    </rule>

    <!-- Warning instead of error for inline HTML. -->
    <rule ref="Generic.Files.InlineHTML">
        <type>warning</type>
    </rule>
</ruleset>
```

## What this standard enforces

This ruleset includes:

- PSR-12 base rules
- strict spacing and formatting rules
- modern class and property conventions
- consistent array handling
- code quality checks for redundant or unsafe patterns
- docblock and attribute structure checks
- stricter visibility and member ordering requirements

In practice, the standard helps keep PHP projects consistent across teams and repositories while still allowing
idiomatic application code.
