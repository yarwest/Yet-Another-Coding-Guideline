# Yet Another Coding Guideline
Hey hello

# Coding Style Guide/Best Practices

This guide serves as a set of guidelines for writing maintainable and readable code troughout the entire stack.
Small note: this guide (especially the General Topics section) is not limited to just code but also general steps that can be taken to assure the quality of a software product/project.

This guide will cover:

- [General Topics](#general)
- [Object Oriented Programming](#oop)
- [Functional Programming](#fp)
- [HTML](#html)
- [CSS (SCSS)](#css)
- [PHP](#php)
- [Java](#java)
- [Python](#python)
- [JavaScript (jQuery)](#js)

### Why
The point of maintaining code standards is to maintain a general sense of structure and quality within a project group to better allow expansion, understanding of the code, and resource management. A text document with examples is one of the best ways (if not the best one) to convey and collect these standards and because I have failed to find any other documents that suit my style and projects I have decided to create my own.

Do not consider this guide final, additions are always welcome and I will make them myself whenever I see fit.

I do however strongly recommend following these guidlines if you want to prevent your team members from going insane before the end of the project.

For the love of god, please make sure to configure the indentation settings of your editor/IDE to a single tab character with a width of 4 spaces.

<a name="general"></a>
## General

### Project Structure
A project should at all points be based around a method of version control in one form or another. My preference goes out to Git. Whenever I use Git in a project, I try to utilize a branch based workflow. This boils down to something very simple: the main project is kept on the master branch, this is the presentable branch. Which is updated at certain intervals, this could for example be after every sprint in a SCRUM-based project or at every release of your product. Next up is the development branch, this contains the most recent version of the project with all completed features. Lastly there is a collection of branches refered to as feature branches. These branches are where the developers will actually work. Whenever a project consists of multiple seperate teams working on the same product, I suggest making multiple development branches (one for each team) based on the main development branch and use those to merge the features made by the team after which they get merged into de main development branch.

Every seperate feature should get a seperate branch and the dependency from one feature branch to another should be kept as small as possible. All functionalities should be accompagnied by (unit) tests that will validate the actual functionality. The developer will work according to the discussed standards.
Whenever a commit is made, the developer should ensure that the commit message is a short, clear, description of the changes made in the commit.
It is key for the developer to make a commit for every independent modification, so that commits can be easily reverted. A thing to keep in mind with this is: if you feel like using the words "and I also did" (or something of that nature) in your commit message, you should probably split this commit into multiple ones.

Whenever a feature is done (in otherwords functional), there shall be a pull request created from said feature branch to the development branch. This feature will have to be reviewed by the person that is responsible for the product quality, or someone appointed for this task by said quality manager. During the review process the reviewer will check whether the produced code fits the standards and if it functiones the way it should (which is determined by running the unit tests). If the conditions are met and there are no merge conflicts, the code can be merged into the development branch.
If the code is not ready for merging, the original author of the pull request has to amend his code to allow for merging.

### Coding
Use descriptive function/method/class/variable/file names. I don't want none of that ```int d = 1;``` bs. Exceptions being when the variable is used as an iterator or something along those lines. But you should have a long, hard, internal discussion before even thinking of doing something like that. Use camelCase if the language allows that.

Limit the amount of variables, operations and lines used as much as possible. Naturally, this will benefit the application in every way since less memory and processing power will be used.

Something that is very important to keep in mind is the global scope. Avoid using global variables as they can lead to an application wide state which should be avoided whenever possible. This basically leads to code that is hard to test, hard to debug and very fragile when used in a multithreaded setting. An example of this is is when a function returns different outputs while receiving the same input.

#### General Formatting
All variables and function names should be written in camel casing if the language allows this.

When composing a code block, keep the following conventions in mind when applicable:

- Do not use a line break before the opening brace
- Use a line break after the opening brace
- Use a line break before the closing brace
- Use a line break after the closing brace, only if that brace terminates a statement or terminates the body of a method, constructor, or named class. For example, there is no line break after the brace if it is followed by an ```else``` or a comma

#### Switch Statements
A switch block should always contain a ```default``` case. Whenever, a fall-trough is used (omission of a ```break``` statement), this should be made clear in a comment.

<!--- algorithm complexity --->
<!--- method/function length --->

### Testing
All functionality should be tested via unit tests. Personally I always strive for 100% method/function coverage.
A test should always only test one method/function. A test can test for various scenarious as long as the test output differentiates between the various cases.

<a name="oop"></a>
## Object Oriented Programming
Classes should be set up based on responsibility and a class should aim to have only one concern in order to limit the access to methods or attributes that should not be accessible from a specific use case.

When naming a class it is obvious that a descriptive name should be used. To ease mutual understanding of class names, keep the following few conventions in mind:

- When the class creates objects, use the ```Factory``` suffix
- When the class is responsible for coordination and communication between other business classes, use the ```Facade``` suffix
- When the class controls the use of a resource class, use the ```Proxy``` suffix
- When the class wraps another class in order to adjust its use for a consumer class, use the ```Adapter``` suffix

When the name of a parameter is/should be the same as an attribute of a class, the ```this``` keyword should be used rather than changing the name of the parameter.
Example:
```java
public class Class {
	private String name;

	public void setName(String name) {
		this.name = name;
	}
}
```

Static classes are something that should be avoided since, just like global variables, they provide global state throughout the application. Besides that, static classes also result in global coupling which makes understanding and maintaining code harder than it needs to be, and it results in having to jump through a few hoops to be able to use isolated unit tests.

On the topic of isolated unit tests, whenever an object is instantiated inside the business logic of another class, it will create a dependency between the two objects which in turn makes it impossible to create an isolated unit test for said business logic. The only way to actually test code that has been set up this way is by testing both classes at the same time since they are directly dependent and mocking is impossible. Naturally, this can be avoided by using a factory instead of having the object instantiated inside the business logic.

Avoid having business logic inside the constructor of an object since it makes it harder to seperate the creation of the object from specific business actions.

<a name="fp"></a>
## Functional Programming
Treat files as you would classes and split them up based on functionality.

Prevent the use of mutable variables since they provide state like global variables do and this can severely hinder concurency. Any state should be passed as an input value to the function that has to be executed.

<a name="html"></a>
## HTML

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
I will be assuming the use of SCSS for 90% of the time, it will be specified when this is not the case.

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

### General
A file that consists of purely PHP should not end with a PHP closing tag ( ```?>``` ), this is done to prevent any unintended white space after that closing tag.

All PHP logic shall be written using an Object Orientated Approach. This means that there are no functions, only classes and methods. Functional PHP scripts belong to scriptkiddies and will harm testing, extensibility and clarity of the code in the long run.
The code is to be indented with a single tab charachter with a width of 4 spaces. The conventions surrounding code block shall be followed regarding the position of braces. All variables and function names should be written in camel casing.
Example:
```php
function exampleFunction() {
	echo “I am indented”;
}
```

When initializing variables, try to do this close to their first usage. Variables should be initialized on declaration or almost immediately afterwards
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

### General
A Java file should contain the following (in that order):

- license or copyright statements (if they exist)
- package statement
- import statements
- one top level class

This obviously means that every top level class has its own filr. This provides a clearer and a more easy to understand structure of classes.

The aforementioned sections should be clearly separated, which is usually done using a seperating blank line.

Whenever importing classes from a package, do not use wildcard imports since more often than not they will lead to classes being imported while they are never used.

The contents of a class should have a certain ordering amongst them, this can't just be a chronological order of creation but there should be some thought put into it as to improve readability.

When initializing variables, try to do this close to their first usage. Variables should be initialized on declaration or almost immediately afterwards

### Formatting
Optional braces, like with an ```if```, ```else```, ```for``` or ```ẁhile``` statements, should always be present to improve readability. The same goes for empty blocks, in this case it is expected to follow the code block conventions surrounding braces.

Each statement should be on a seperate line.



<!--- todo --->

<a name="python"></a>
## Python

### General
When you are trying to store multiple instances of the same type, use a list or array. When trying to store multiple pieces of data that are not of the same type but are still part of the same concept, use a tuple.
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
The code is to be indented with a single tab charachter with a width of 4 spaces. The opening bracket of a code block is supposed to be on the same line as the signature.  All variables and function names should be written in camel casing.
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

When initializing multiple variables, try to do this close to their first usage. Variables should be initialized on declaration or almost immediately afterwards. It is possible to chain these variables but always make sure to declare base values seprately (so don’t do let me = you = 2) because this can lead to problems with the global namespace.
Example:
```javascript
let	i = 5,
	e = 5,
	c = 3;
let	m = 5;
let	d = 4;
```
