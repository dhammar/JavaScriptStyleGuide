JavaScript Style Guide
====================

*An approach to JavaScript from the perspective of a battle-hardened .NET shop.*

## <a name='TOC'> Table of Contents</a>

  1. General Formatting
  	1. [Spacing](#spacing)
  	2. [Semicolons](#semicolons)
  	3. [Commas](#commas)
  	4. [Braces](#braces)
  	5. [Strings](#strings)
  	6. [Line length](#linelength)
  	7. [Comments](#comments)
  2. Style
  	1. [Declarations](#declarations)
  	2. [Naming Conventions](#naming)
  	3. [Literals](#literals)
  	4. [Functions](#functions)
  	5. [Comparisons](#comparisons)
  	6. [Type Checking](#types)
  	6. [Namespacing](#namespacing)
  	7. [Global](#global)
  3. Implementation
  	1. [Prototypes](#prototypes)
  	2. [Async](#async)
  	3. [Eval, With, Object.freeze, Object.seal, Object.preventExtensions ...](#nonono)
  	4. [Performance](#performance)
  	5. [Unit Testing](#unittesting)

----

> ### <a name='spacing'>Spacing</a>

  - Use soft tabs of four spaces

	```javascript
	// Bad
	function sample() {
	var x = 2;
	}

	// Bad
	function sample() {
	∙∙var x = 2;
	}

	// Bad
	function sample() {
	→   var x = 2;
	}

	// Good
	function sample() {
	∙∙∙∙var x = 2;
	}
	```

  - Place one space before leading braces and after commas

	```javascript
	// Bad
	function sample(){
		// ... implementation ...
	}

	// Good
	function sample()∙{
		// ... implementation ...
	}

	// Bad
	update('contact',{
		name: 'Reptar'
	});

	// Good
	update('contact',∙{
		name: 'Reptar'
	});
	```

  - Use indentation when chaining

	```javascript
	// Bad
	$element.on().off().remove();

	// Bad
	$element.on()
	.off()
	.remove();

	// Good
	$element.on()
		.off()
		.remove();
	```


----

> ### <a name='semicolons'>Semicolons</a>

There are those out there who do not believe in the semicolon, but alas, we do! Semicolons aid in **readability** and **minification**. Two things that are very important, so just remember to use them.


----
> ### <a name='commas'>Commas</a>

  - **Leading? Nope.** This style has it's benefits for sure in troubleshooting visually, but really we should all be linting our code anyways, right? If you find this is an issue, make sure you've got lint running and you should be good to go.
    
	```javascript
	// This is bad
	var x = 2
	  , y = 3;
	```

  - **Trailing? Yep.** Much cleaner looking and not as hard to type.
    
	```javascript
	// This is good
	var x = 2,
	    y = 3;
	```


----
> ### <a name='braces'>Braces</a>

  - **Functions:** Always use braces. This just helps with readability in general. Awkward multiple line statements are bound to occur that may not make sense immediately to another developer who is  skimming over code. Braces help ensure blocks are well defined with a good visual weight.

	```javascript
	// Bad
	if (true)
		return false;

	// Bad
	if (true) return false;

	// Good
	if (true) {
		return false;
	}

	// Good
	if (true) { return false; }
	```


----
> ### <a name='strings'>Strings</a>

  - Use single quotes `''` for strings. This helps alleviate the pain of having to escape quotes in normal copy as well as in XML.

	```javascript
	// Bad
	var name = 'Reptar';

	// Good
	var name = 'Reptar';
	```

  - Use commonsense with string length before wrapping it across multiple lines.
  - Build strings using array concatenation (mainly for performance benefits in Internet Explorer).

	```javascript
	// Bad
	var message = 'This message' +
		'goes across several' +
		'lines.';

	// Good
	var message = [
			'This message',
			'goes across several',
			'lines.'
		].join('');
	```


----
> ### <a name='linelength'>Line Length</a>

A good rule of thumb is somewhere between 80 and 120 lines of code. While we don't have an explicit standard, just try and be conscious of long lines.

Really this has two benefits:

  1. General readability in that you don't have to scroll horizontally to see the end of some lines.
  2. Side-by-side views are more useful when you're code doesn't cover the whole width of your 20" widescreen monitor.


----
> ### <a name='comments'>Comments</a>

  - **Placement:** Comments should be placed according to your commonsense. If you think that you won't remember why you did something after a month of vacation, then make a note. Don't explain every nook and cranny though.
  - **Format:**
    * Single line comments should use the double forward slash with a space after the slashes.
    
	```javascript
	//Bad comment

	// Good comment
	```

    * Multiple line comments should use the block comment style.

	```javascript
	/*
		Comments that span multiple lines.
		Are better off in a simple, unadorned block.
	*/
	```

  - Avoid interrupting cow goes moo. Interrupting comments do not have a place in our world. They can go usually go elsewhere really easily and be just as effective.

	```javascript
	function sample(param1, param2, /* OPTIONAL */ param3) {
		// ... implementation ...
	}
	```

  - Regions are OK to use.


----
> ### <a name='declarations'>Declarations</a>

  - **Variables:** Should be declared at the start of a block and should be declared once. Each block should only have one `var` statement.

	```javascript
	// Bad
	var x = 2;
	var y = 2;

	// Good
	var x = 2,
		y = 2;

	// Bad
	var x = 2;

	x = x * 5;

	var y = 2;

	// Good
	var x = 2,
		y = 2;

	x = x * 5;
	```

  - **Hoisting:** Be aware that variable declarations get hoisted to the top of their scope. Function *declarations* (not function *expressions*) are hoisted to the top of their scope as well. Function expressions have their host variable name hoisted to the top of their scope, but not their function body or function name.
    * *Function Declaration:*

	```javascript
	function sample() {
		// ... implementation ...
	}
	```

    * *Function Expression:*
    
	```javascript
	var x = function x() { 
		// ... implementation ...
	};

	(function () {
		// ... implementation ...
	});
	```


----
> ### <a name='naming'>Naming Conventions</a>

  - **General Guidelines:**
    * *Name Choices:* Avoid using abbreviations (use `getWindow` instead of `getWin`). Don't use hungarian notation `strName` to note the type of the variable. Only use the underscore character to prefix names of private members.
    * *Reserved Words:* Be aware of and do not use [reserved words](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Reserved_Words) as keys. 
  - **Variables:** Use camel casing. Example: `backgroundColor`.
  - **Properties:** Use camel casing. Example: `element.backgroudColor`.
  - **Classes/Constructors:** Use pascal casing. Example: `function Dog() { }`.
  - **Constants:** Use pascal casing. Example: `var DOMElementId = 'firstName';`.
  - **File Names:** Use camel casing. Example: `contactRibbon.js`.


----
> ### <a name='literals'>Literals</a>

  - Objects should use object literal. This style is just plain cleaner and simpler

	```javascript
	// Bad
	var coords = new Object();
	coords.x = 0;
	coords.y = 0;

	// Good
	var coords = {
		x = 0,
		y = 0
	};
	```

  - Arrays should use array literal as well.

	```javascript
	// Bad
	var x = new Array();
	x.push(2);
	x.push(3);

	// Good
	var x = [2, 3];

  - [Namespaces should not be defined as literals. They are messy.](#namespaces)


----
> ### <a name='functions'>Functions</a>

  - **Length:** Use commonsense, if your function is starting to look really, really long then chunk it up into pieces. General rule of thumb is you should start to get scared of the length if it is about a screen-height's worth of code.
  - **Anonymous:** Anonymous functions (such as with inline callbacks) simply put should almost never be anonymous. Functions always serve a purpose and thus should always deserve a name. This will help greatly with stack traces. If a client sends you a list of anonymous -> anonymous -> anonymous, that really won't help you troubleshoot a problem, will it?
  - **Closures:** Closures are very, very handy but be wary of circular references and the memory leaks they can bring about in IE.
  - **Callbacks:** If you have a lot of asynchronous calls to make and have a bunch of inline callbacks, you may start to notice a sort of pyramid shape to your code. Try to avoid this and split out your inline callbacks out.

	```javascript
	// Bad
	retrieveDinosaur(function retrievedDinosaur(dino) {
		if (dino.name === 'Reptar') {
			retrieveChildren(function retrievedChildren(children) {
				// ... and the pyramid gets taller and taller from here ...
			});
		}
	});

	// Good
	function _retrievedDinosaur(dino) {
		if (dino.name !== 'Reptar') { return; }

		retrieveChildren(_retrievedChildren);
	}

	// ...

	retrieveDinosaur(_retrievedDinsoaur);
	```

----
> ### <a name='comparisons'>Comparisons</a>

  - **Equality:** Use strict comparisons (`===` and `!==`) always as opposed to Type-converting (abstract) comparisons. The only exception to this would be for checking if something is null *or* undefined.

	```javascript
	// Bad
	if (name == 'Reptar') { }

	// Good
	if (name === 'Reptar') { }
	```

  - **Conditions:** Non-trivial conditions should be assigned to a descriptive variable.

	```javascript
	// Bad
	if (name === 'Reptar' && type === 'dinosaur') {
		// ... implementation ...
	}

	// Good
	var isMatch = (name === 'Reptar' && type === 'dinosaur');
	if (isMatch) {
		// ... implementation ...
	}
	```


----
> ### <a name='types'>Type Checking</a>

  - **String:** `typeof variable === 'string'`
  - **Number:** `typeof variable === 'number'`
  - **Boolean:** `typeof variable === 'boolean'`
  - **Object:** `typeof variable === 'object'`
  - **Array:** `Array.isArray(arrayLikeObject)`
  - **Null:** `variable === null`
  - **Null or Undefined:** `variable == null`
  - **Undefined:** `typeof variable === 'undefined'`
  - **Instance of an Object:** `classInstance.Type === 'className'`
    * *Note:* We are purposefully avoiding the usage of `instanceof` in this case because it is unsafe across dialogs/iframes. If the class definition is reloaded in another context (or frame/window) and objects from one context are sent to another context, the `instanceof` check may fail. This does require some extra plumbing, but it is minimal.
  - **Type Conversion:** When converting a string to an integer using `parseInt()`, always pass in the radix. Therefore instead of `parseInt('2');` use `parseInt('2', 10);`.
  - **Type Coercion:** Coercion is OK to use when it makes sense, and if it looks like it might be confusing, change your implementation or wrap it in parenthesis.

	```javascript
	// Bad: could be misconstrued as using the '++' operator
	var x = 0;
	x = 2 + +document.getElementById('countInput').value;

	// Good
	var x = 0;
	x = 2 + (+document.getElementById('countInput').value);
	```


----
> ### <a name='namespacing'>Namespacing</a>

Namespacing should be used to group functions together and to help avoid pollution of the global namespace. There are several different ways to namespace your code, but it is preferable to create our namespaces and scopes using an Immediately Invoked Function Expressions (IIFE). This is the cleaner way of organizing your code. If you use object literals to define a namespace, you have to name all your functions twice. With the IIFE pattern you have better control of private vs public members. Also, as part of good styling keep the invocation of your IIFE inside the parenthesis that contain it.

	```javascript
	// Bad
	var Container = [
		_isOpen: false,
		
		open: function open() {
			this._isOpen = true;
		}
	};


	// Good
	var Container = (function createNamespace() {

		var _isOpen = false;

		function open() {
			isOpen = true;
		}

		// Expose public members below
		return {
			open: open
		};

	}());
	```


----
> ### <a name='global'>Global</a>

  - **Pollution:** You too can prevent global namespace pollution. Only add objects/variables to the global namespace if necessary, otherwise keep it in the normal scope. In general wrap all of your code in an IIFE block that is in strict mode (`'use strict';` is set) and pass in a reference to the global object to more vividly declare your exports.

	```javascript
	// Bad
	var x = 2;

	function addToX(y) {
		return x + y;
	}

	addToX(1);


	// Good
	(function (global) {
		'use strict';
		global.x = 2;

		function addToX(y) {
			return x + y;
		}

		addToX(1);	

	}(this));
	```

  - **Performance:** JavaScript searches up the scope chain for variables; globals take the longest to find. Therefore if you must define a global, if you use it more than once in a block, assign a reference to it in a local variable.


----
> ### <a name='prototypes'>Prototypes</a>

Do not extend native object prototypes as it adversely affects re-factoring code down the line. The prime example of this I always run into is with Date.js. If you include it, find out it has a problem, then need to swap it out for something like Moment.js, you are going to have the lease fun experience of your life trying to hunt down all the places it is used.


----
> ### <a name='async'>Async</a>

If you have the option between asynchronous and synchronous. Always try to start the asynchronous route. If you end up going synchronous, you better have a very good explanation of why. Locking up the User Interface is no good for anyone.


----
> ### <a name='nonono'>Eval, With, Object.freeze, Object.seal, Object.preventExtensions ...</a>

There is about a one in a million chance that you will need to use any of this stuff. Stay clear unless you know for sure what you're doing with them, and even then, probably still stay clear of them.


----
> ### <a name='performance'>Performance</a>

  - **Loops:** There are several ways to optimize loops but most of the time nowadays we can shoot for readability unless we really need to ensure our loops are going to be performant. In general we should start with the below and then if we need to be faster, evaluate other options such as decrementing while loops.

	```javascript
	// Example
	var i,
		len;

	for (i = 0, len = arrayLikeObject.length; i < len; i++) {

	}
	```

  - **Copying arrays:** Use `Array.slice`.

	```javascript
	// Bad
	var i,
		len,
		itemsCopy = [];

	for (i = 0, len = items.length; i < len; i++) {
		itemsCopy[i] = items[i];
	}

	// Good
	itemsCopy = items.slice();
	```
	
  - Follow all the other rules already laid out in this document. Things like using type-converting comparison operators can be slower.


----
> ### <a name='unittesting'>Unit Testing</a>

Do it and don't let it fall by the wayside, give a good fight for extra time to make sure your code is tested. We prefer to use QUnit and PhantomJS.