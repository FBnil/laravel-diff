# Laravel-Diff tool

This package allows easy comparison of two texts and yields output in plain text, table and html format.

The original Laravel-Diff has a broken diff algorithm. The algorithm used in this fork is from http://code.stephenmorley.org/php/diff-implementation/
I tried to be compatible, but we are not API compatible.

Warning: Alpha code:
I am also still moulding it to be better code (exceptions, checks for is_readable() etc).

## Table of content

* [Features](#features)
* [Installation](#installation)
* [Configuration](#configuration)
* [Usage](#usage)
* [CSSStyling](#cssstyling)

---
[Back to top](#Laravel-Diff)

## Features

* compare **strings**
* compare **files**
* planned: group string differences into **hunk groups**
* Unicode support

## Installation

Via `composer`:

```bash
composer require FBnil/laravel-diff
```

---
[Back to top](#Laravel-Diff)

## Installation
If you have Laravel 5.5 installed, that's it. No additional configuration has to be done.
---
[Back to top](#Laravel-Diff)

## Usage

Simple oneliner:

```php
$htmlSnippet = \ViKon\Diff\Diff::compareFiles($file1, $file2)->toHtml();
```

Other examples:

```php
use \ViKon\Diff\Diff;
// Compare string line by line
$diff = Diff::compare("hello\na", "hello\nasd\na");
// Outputs span with ins and del HTML tags. You can embed this in a div.
$html = $diff->toHTML();

// Outputs a side-by-side <table> 
$html = $diff->toTable();

// Output is text; similar to the Unix command "diff -u"
$txt = $diff->toString();

// Get the raw data to have more control.
$struct = $diff->toStruct();
```

Compare two file:

```php
// Compare files line by line
$diff = Diff::compareFiles("a.txt", "b.txt");
echo $diff->toHTML();
if($diff->getInsertedCount() == 0 && $diff->getDeletedCount() == 0)
 echo "Files are identical!"
```

You can customize output by getting raw data:

```php


```

---
[Back to top](#Laravel-Diff)


## CSSStyling

A little bit of CSS is recommended to make <ins> and <del> look good, for example:

```css
del {
  text-decoration: none;
  background-color: #fbb6c2;
  color: #555;
}
ins {
  text-decoration: none;
  background-color: #d4fcbc;
}
```

---
[Back to top](#Laravel-Diff)

## License

This package is a mix between CC and MIT License. Give me some time to sort it out.

---
[Back to top](#Laravel-Diff)
