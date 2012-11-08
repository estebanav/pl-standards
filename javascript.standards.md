# Pl-standards - Presentation Layer Standards for PLDs

#{Js Basic Styles}
=====================================

The aim of this repository is to provide a common set of guidelines to stablish  a standard way of coding to Presentation Layers Developers and good practices.



**Javascript: Style Guide and Good Practices - (Work in progress)**

## Introduction
We'd like to build a set of recommendations to write better javascript. It is a good space to think, discuss, search and learn. We're inspired in several sources, which are at the bottom of this page.

As Douglas Crockford says:
> The long-term value of software to an organization is in direct proportion to the quality of the codebase. Over its lifetime, a program will be handled by many pairs of hands and eyes. If a program is able to clearly communicate its structure and characteristics, it is less likely that it will break when modified in the never-too-distant future.

> Code conventions can help in reducing the brittleness of programs.

> All of our JavaScript code is sent directly to the public. It should always be of publication quality.

[http://javascript.crockford.com/code.html](http://javascript.crockford.com/code.html)   

Let's start.


###Indentation
Each level 4 spaces. Don't use Tabs.

###Line Length
No longer than 80 characters. 
If there's more characters, wrap it after an operator (, +) and next line must be indented two levels.

###Strings
Use double quotes, never singles ones. Never use an slash to create a new line when the string is to long.

###Null
Use only with objects. 
•	To initialize a variable that later be assigned to an object
•	Like a parameter for a function that waits an object or to return from a function where an object is expected
Not a good idea:
```javascript
if (person != null){
    doSomething();
}
```

###Undefined
// Good
```javascript
if (typeof variable == "undefined") {
    // do something
}
```

// Bad: Using undefined literal
```javascript
if (variable == undefined) {
    // do something
}
```



###Operator Spacing
// Good
```javascript
var found = (values[i] === item);       Space before and after it when it has two operands.
```

// Bad: Missing spaces
```javascript
var found = (values[i]===item);
```

###Parenthesis Spacing
Not space after the opening paren or before the closing paren.

###Object Literals
// Good
```javascript
var object = {
      
      key1: value1,
      key2: value2,
      
      func: function() {
             // do something
      },

      key3: value3

};
```

###Comments
Use comments frequently.

Single line: 
	Separate line (to describe code below it). Use same indentation that commented code.
	End of a line (to describe the code before it). Use one indentation level between the code and the comment.

Multi line: 
```javascript
if (condition){
    //1 empty line
    /*
     * if you made it here,
     * then all security checks passed
     */
```     

###Comment Annotations

```javascript
//TODO: lorem ipsum

/*
* HACK: Have to do this for IE. I plan on revisiting in
*/
//REVIEW: How make it better?
//FIXME: remember, it should be fixed because ...!
```

###Variables
Declare variables before use it.
Declare at the beginning of the functions.
Use 1 single var for a group of declarations.
// Good
```javascript
var count = 10,
      name = "Nicholas",  
      found = false,
      empty;
```

###Function Declaration
Declare before use it.
Use function declaration format, not  function expression (except in methods, function which are object members)
// Good
```javascript
function doSomething(arg1, arg2) {
    return arg1 + arg2;
}
```
See space before opening brace, after the comma (on arguments) but not before it. Don't use space between the name and opening paren.

###Immediate functions
// Good
```javascript
var value = (function() {
    
    // function body

    return {
        message: "Hi"
    }
}());
```
Notice the following structure: ( function() {   }() );

###Naming
Use lower camel case for variable names, and use nouns: var addressNumber;
Use lower camel case for function names, and choose verbs: getAddressNumber();
Function used to create objects, using new, should be named using non verbs, with upper camel case: MyObject();
Variables  with constant values should use every letter on uppercase, and words separated by underscores: INTERVAL_TIME;

###Strict Mode
Use it only into a function, not on global scope. 
It change the way javascript is proccesed, and sometimes, it can avoid errors.
```javascript
function Name() {
    "use strict";
```

###Assignment
// Good
```javascript
var flag = (i < count);
```
Use parenthesis on the value side, only when it contains a comparison.

###Equality Operatos
Use !== / === instead of != / ==.
It can avoid errors caused by type coersion: when JS change the type of some variable to get a comparison.

###Ternary operator
Use only to assign a value 
// Good
```javascript
var value = condition ? value1 : value2;
```

###Statements
Simple statements ends with ;
Only 1 statement per line: Bad > count++; a = b;

IF
```javascript
if (condition) {
    statements
} else if (condition) {
    statements
} else {
    statements
}
```
Never omit braces even if there's only a single statement. 

FOR
Use only for arrays:
```javascript
for (initialization; condition; update) {
    statements
}
```

Use only for objects:
```javascript
for (variable in object) {
    statements
}
```

Use hasOwnProperty() method into an IF to get only the properties of the instance.

```javascript
for (prop in object) {
    if (object.hasOwnProperty(prop)) {
        console.log("Property name is " + prop);
        console.log("Property value is " + object[prop]);
    }
}
```

While
```javascript
while (condition) {
    statements
}
```


Do
```javascript
do {
    statements
} while (condition);
```
Notice the ; at the end of DO statement.

Switch
```javascript
switch (value) {
    case 1:
             /* falls through */
    
    case 2:
           doSomething();
           break;

    case 3:
            return true;

    default:
              throw new Error("This shouldn\'t happen.");
}
```


Try
```javascript
try {
    statements
} catch (variable) {
    statements
} finally { 
    statements
}
```



###Good Practices in JavaScript


###Loose Coupling between JS, CSS & HTML

Get a low level of dependency between JS , CSS and HTML layers. 
	
	>Don't use css expression() into the CSS.
	>Try to keep  out the css properties from the javascript code. 
	>To change css properties from javascript, prefer  to assign or remove CSS classes, defined into CSS files.
	>Don't  embed javascript into HTML tags. 


###Avoid Globals

1) Pass external variables required for a function, like arguments. So its value won't depends of global assignments but it'll depends on the value assigned to the parameter.

2)Declare variables into body function, and using always the "var" statement .

3) Into new code,  is better use strict mode to avoid global variables and other programming errors.

4) Set only 1 single global using Namespaces:

```javascript
var JS = {};

JS.some = function(title) {
    this.title = title;
    this.page = 1;
};

JS.some.prototype.myMethod = function(param) {
    this.attribute += param;
};
JS.some.otherThing = new JS.some("bla bla bla");
```

###Cache length in loops

Store the length's array in a variable before the loop.

Good:
```javascript
var l = array.length;
for(var i=0; i<=l; i++){
    //do something
}
```
Bad:
```javascript
for(var i=0; i<=array.length; i++){

}
```

###Append new elements outside of a loop

Adding elements to the DOM has a cost. Do it once, not once at each iteration.

Bad:

```javascript
$.each(array, function(){
    //do something and...
    $('.list').append(newElement);
})
```

##Jquery Good Practices

Good:
```javascript
$.each(array, function(){
    //do something and...
   html += '<li>' + value + '</li>';
})
$('.list').html(html);
```

###Optimize selectors

Good:
```javascript
$('#some div.class')  //starting with ID. It's faster.
```

Best:
```javascript
$('#some ').find(' div.class')
```

 Good:
```javascript
$('-specifity > +specificity')  Example: $('.titles td.first')  -> $([tag or class] [tag.class])
```

Bad:
```javascript
$('.data table tr td.red .income') //too much specificity!
```

Bad:
```javascript
$('.buttons > *')  //no universal selector!
```

###Use delegate and live

```javascript
$(context-holder).delegate('elements', 'event', callback);

$(element).live('event', callback);
```

They work faster and allow add new elements without re bind event handlers.



