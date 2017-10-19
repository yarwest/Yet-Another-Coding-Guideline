# Yet Another Coding Guideline
Hey hello

# Coding Style Guide/Best Practices

This guide serves as a set of guidelines for writing maintainable and readable code troughout the entire stack.
Small note: this guide (especially the General Topics section) is not limited to just code but also general steps that can be taken to assure the quality of a software product/project.

This guide will cover:

- [General Topics](#general)
- [Object Orientated Programming](#oop)
- [HTML](#html)
- [CSS (SCSS)](#css)
- [PHP](#php)
- [Java](#java)
- [Python](#python)
- [JavaScript (jQuery)](#js)


Do not consider this guide final, additions are always welcome.

I do however strongly recommend following these guidlines if you want to prevent your team members from going insane before the end of the project.

For the love of god, please make sure to configure the indentation settings of your editor/IDE to a single tab character with a width of 4 spaces.

<a name="general"></a>
## General
Use descriptive function/method/class/variable/file names. I don't want none of that ```int d = 1;``` bs. Exception being when the variable is used as an iterator. But you should have a long, hard, internal discussion before even thinking of doing that.

<a name="oop"></a>
## Object Orientated Programming
This ain't hard, just make some classes.

<a name="html"></a>
## HTML
There isn’t much I can think up for HTML right now. todo.

### General
Children elements are supposed to be indented with a single tab charachter with a width of 4 spaces.
Example:
```html
<div class=”parentElement”>
	<p class=”childElement”>This is the first child</p>
	<p class=”childElement”>This is the second child</p>
</div>
```

Classnames and ids of elements are supposed to be written in camelcasing. This is done to make sure there is no interference with Bootstrap styling (since Bootstrap uses snakecase).
Example:
```html
<p class=”redText”>This is a red text</p>
```

Prevent using extra classes or ids in your HTML where a modified CSS selector would suffice.

<a name="css"></a>
## CSS/SCSS
Again, not much to say right now. I will be assuming the use of SCSS for 90% of the time.

### General
Constants that are to be used in multiple stylesheets should be defined in the ```variables.scss``` file. This file should contain no actual style rules, just variables. Try to initalize file specific variables at the beginning of the file.

The style rules are to be indented with a single tab charachter with a width of 4 spaces. The opening bracket of a code block is supposed to be on the same line as the selector.
Example:
```css
.redText {
	color: red;
}
```

Nest your code blocks whenever possible to prevent unwanted behaviour.
Example:
```css
.text {
	line-height: 5px;
	.red {
		color: red;
	}
}
```

Limit the use of ```!important``` to situations where there is no other option because of overlapping style rules.

<a name="php"></a>
## PHP
General
A file that consists of purely PHP should not end with a PHP closing tag ( ```?>``` ), this is done to prevent any unintended white space after that closing tag.

All PHP logic shall be written using an Object Orientated Approach. This means that there are no functions, only classes and methods. Functional PHP scripts belong to scriptkiddies and will harm testing, extensibility and clarity of the code in the long run.
The code is to be indented with a single tab charachter with a width of 4 spaces. The opening bracket of a code block is supposed to be on the same line as the signature. All variables and function names should be written in camel casing.
Example:
```php
function exampleFunction() {
	echo “I am indented”;
}
```

Try to initialize class/method specific variables at the beginning of that class/method.
Make sure to write a comment before a function or code block. Describe the functionality, the parameters and return values. This has to be done using the [phpDocumenter](https://docs.phpdoc.org/) syntax, which works very similar to Javadoc.
Example:
```php
<?php
/**
 * This document will show you how you are supposed to document a PHP file.
 */
/**
 * This class contains method(s) that will help you document.
 */
class documenter {
	/**
 	 * This method is responsible for showing you how to document.
 	 * @param text, a string that has to be printed.
 	 * @return the printed string
 	 */
	function exampleFunction($text) {
		echo $text;
		return $text
	}
}
```

<a name="java"></a>
## Java
Just don't do it. jk todo.

<a name="python"></a>
## Python
When you are trying to store multiple instances of the same type, use a list or array. When trying to store multiple pieces of data that are not of the same type but are still part of the same thing, use a tuple.
Example:
```python
// Storing a list of song titles
titles = ["Never Gonna Give You Up", "Ding Dang", "Shooting Stars"]

// Storing a coordinate
location = (12.3, 20.2)

// This also allows you to easily unpack the earlier defined collection into seperate variables
x, y = location
```

<a name="js"></a>
## JavaScript/jQuery
There are a lot of things that can be said about JavaScript, I’ll try to keep it limited.

### General
The code is to be indented with a single tab charachter with a width of 4 spaces. The opening bracket of a code block is supposed to be on the same line as the signature. All variables and function names should be written in camel casing.
Example:
```javascript
function exampleFunction() {
	alert(“I am indented”);
}
```

Make sure to write a comment before a function or code block. Describe the functionality, the parameters and return values. This has to be done using the [JSDoc](http://usejsdoc.org/) syntax, which works very similar to Javadoc.
Example:
```javascript
/**
 * This function is responsible for showing you how to document.
 * @param text, a string that has to be printed.
 * @returns the printed string
 */
function exampleFunction(text) {
	alert(text);
	return text
}
```

When making a jQuery function, always end the function by returning ```this```, this allows the function to be chained with other functions.
Example:
```javascript
jQuery.fn.extend({
    exampleFunction: function () {
        alert(this.text);
        return this;
    }
});
// Because ‘this’ is returned at the end of the exampleFunction
// hide can be called in the same line
$(“p”).exampleFunction().hide();
```

### Variables
A variable should be declared with ```let``` rather than ```var```, this is done amongst others to constrict the scope of the variable to the current block, which will prevent unexpected behaviour. More information and examples on that can be found in the accepted answer of [this StrackOverflow question](https://stackoverflow.com/questions/762011/whats-the-difference-between-using-let-and-var-to-declare-a-variable).
The downside of this is that you can not redeclare this variable (no clue why you would want this to be fair), but you are able to overwrite it. 
Example:
```javascript
// This works
var i = 0;
var i = 1;

// This works too
let i = 0;
i = 1;

// This throws a syntax error
let i = 0;
let i = 1;

// This also throws a syntax error
let i = 0;
var i = 1;
```

Never use ```var``` inside a block if it may negatively effect the function of which it is a part.

Prevent using for-loops when a foreach-loop is possible. Whenever there are multiple for-loops, initialize the index variable before the loop. Any variables that are to be used inside a loop should be initialized outside of the loop when possible. This will speed up the application by reducing the number of system interactions.
Example:
```javascript
function exampleFunction() {
	var i = 0,
	    e = 0;
	for(i = 0; i < 5; i++){
		e = i + 1;
		alert(e);
	}
	for(i = 0; i < 7; i++){
		alert(i);
	}
}
```

Naturally, the downside of this is that certain variables are available outside of the loop that they are used in. Make sure to always  Be aware of such situations. Whenever you suspect it may lead to unexpected behaviour it is your primary concern to restrict the variables scope to the appropriate block.

When initializing multiple variables, try to do this at the beginning of the appropriate block. It is possible to chain these variables but always make sure to declare base values seprately (so don’t do let me = you = 2) because this can lead to problems with the global namespace.
Example:
```javascript
let	i = 5,
	e = 5,
	c = 3;
let	m = 5;
let	d = 4;
```
