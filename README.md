# Laravel-Diff tool

This package allows easy comparison of two texts and yields output in plain text, table and html format.

The original Laravel-Diff has a broken diff algorithm. The algorithm used in this fork is from http://code.stephenmorley.org/php/diff-implementation/
I tried to be compatible, but we are not API compatible.

Warning: Alpha code:
I am also still molding it to be better code (exceptions, checks for is_readable() etc).

![examples](diff_looks.jpg?raw=true "Different looks with basic css")


## Table of content

* [Features](#features)
* [Installation](#installation)
* [Configuration](#configuration)
* [Usage](#usage)
* [CSS Styling](#css-styling)

---
[Back to top](#laravel-diff-tool)

## Features

* compare two **strings**
* compare two text **files**
* Unicode support
* Outputs a html snippet you can embed into a `<div>`
* The output can be a side-by-side `<table>`, a line by line diff `<span>` or a minimal word analysis diff. 

## Installation

Using `composer`:

```bash
composer require FBnil/laravel-diff
```

---
[Back to top](#laravel-diff-tool)

## Configuration

If you have Laravel 5.5 installed, that's it. No additional configuration has to be done.

---
[Back to top](#laravel-diff-tool)

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
/* Returns the diff for two files. The parameters are:
*
* @param $file1      - the path to the first file
* @param $file2      - the path to the second file
* $compareCharacters - true to compare characters, and false to compare lines. Optional; defaults to false.
*/
$diff = \ViKon\Diff\Diff::compareFiles($file1, $file2, true);
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
[Back to top](#laravel-diff-tool)


## CSS Styling

A little bit of CSS is recommended to make `<ins>` and `<del>` look good, for example:

```css
del, .diffDeleted {
  text-decoration: none;
  background-color: #fbb6c2;
  color: #555;
}

ins, .diffInserted {
  text-decoration: none;
  background-color: #d4fcbc;
}

table.diff , table.diff th, table.diff td{
	border: 1px solid #EEE;
}

table.diff th, table.diff td{
	padding: 5px; /* Apply cell padding */
}
```

---
[Back to top](#laravel-diff-tool)

## License

This package is a mix between CC and MIT License. Give me some time to sort it out.

---
[Back to top](#laravel-diff-tool)
