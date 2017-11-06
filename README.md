# Laravel-Diff tool

This package allows easy comparison of two texts and yields output in plain text, table and html format.

The original Laravel-Diff has a broken diff algorithm. The algorithm used in this fork is from http://code.stephenmorley.org/php/diff-implementation/
I tried to be compatible, but we are not API compatible.

Warning: Alpha code:
I am also still molding it to be better code (exceptions, checks for is_readable() etc).

## Table of content

* [Features](#features)
* [Installation](#installation)
* [Configuration](#configuration)
* [Usage](#usage)
* [CSSStyling](#cssstyling)

---
[Back to top](#Laravel-Diff-tool)

## Features

* compare **strings**
* compare **files**
* Unicode support

## Installation

Via `composer`:

```bash
composer require FBnil/laravel-diff
```

---
[Back to top](#Laravel-Diff-tool)

## Installation

If you have Laravel 5.5 installed, that's it. No additional configuration has to be done.

---
[Back to top](#Laravel-Diff-tool)

## Usage

Simple oneliner:

```php
$htmlSnippet = \ViKon\Diff\Diff::compareFiles($file1, $file2)->toHtml();
```

Other examples:

```php
use \ViKon\Diff\Diff;
// Compare string line by line
$diff = Diff::compare("hello\n!", "hello\nworld\n!");
// Outputs span with ins and del HTML tags. You can embed this in a div.
$html = $diff->toHTML();

// Outputs a side-by-side <table> 
$html = $diff->toTable();

// Output is text; similar to the Unix command "diff -u"
$txt = $diff->toString();

// Get the raw data to do your own analysis.
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

You can process the raw data:

```php
$AoA = $diff->toStruct();
$MYTEXT = '';
foreach($AoA as $charArr){
	$char = $charArr[0];
	$stat = $charArr[1];
	if($stat == DIFF::UNMODIFIED) // 0
		$stat = ' ';
	if($stat == DIFF::DELETED) // 1
		$stat = '-';
	if($stat == DIFF::INSERTED) // 2
		$stat = '+';
	$MYTEXT .= "$stat:$char ";
}
echo($MYTEXT);
```

---
[Back to top](#Laravel-Diff-tool)


## CSSStyling

A little bit of CSS is recommended to make `<ins>` and `<del>` look good, for example:

```css
del,.diffDeleted {
  text-decoration: none;
  background-color: #fbb6c2;
  color: #555;
}
ins,.diffInserted {
  text-decoration: none;
  background-color: #d4fcbc;
}
```

---
[Back to top](#Laravel-Diff-tool)

## License

This package is a mix between CC and MIT License. Give me some time to sort it out.

---
[Back to top](#Laravel-Diff-tool)
