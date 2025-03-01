# Coding conventions 

Before commencing implementation make sure the requirement is well defined and even documents if sufficiently complex.  

## [Clean Code Principles](https://www.freecodecamp.org/news/clean-coding-for-beginners/) (courtesy of Robert C. "Uncle Bob" Martin) 

1. Magic numbers - all values (numbers and strings) should be used via a variable with a name that describes its purpose.  

1. Comments: should be kept to an absolute minimum and to describe why the code is as it is not what it is doing. 

1. Naming convention - general rule - descriptive over brevity: 

    1. Absolute constants such as days in a week should use capitalised snake case. 

        * e.g., const DAYS_IN_A_WEEK = 7; 

    1. Constants and variable should use camel case which is a series of words joined together all in lower case except the first letter of second (and subsequent) words. 

    1. Boolean variables and properties should be named to make then more readable when used in a condition, such as an if statement. 

        * i.e., prefixed with 'is' or 'has', etc. e.g., if (blar.hasChildren) ... 

    1. Function/Method names should ideally start with a verb as calling them will usually involve some action being performed. The verb should be followed but one or more nouns, the object on which the function will be executed. If required a qualifying word can be used to disambiguate but this should be used rarely. Try to use a consistent set of verbs. 

    1. Classes and (functional) components should use Pascal case (like camel case but with the first letter also capitalised.) 

1. Keep functions small and dedicated to a single purpose. Functions have two primary purposes; to provide reuse and to decompose larger functions doing too many things and making them difficult to comprehend. 

1. Avoid nested loops as deeply nested loops are difficult to comprehend. Flattening the dataset or using recursion can be an alternative. 

1. Avoid using single letter variable names including in for loops. Arrays should use a plural name with the individual elements (and objects) using the singular form. 

## Tooling 

1. Employ an active linter like [ESLint](https://eslint.org/).  

1. Use a [prettifier](https://prettier.io/) configured to revise on save to ensure common rules are applied consistently.  

1. Consider using [TypeScript](https://www.typescriptlang.org/) especially on larger development teams.  

1. Consider using CSS pre-processor like [SCSS](https://sass-lang.com/)/[LESS](https://lesscss.org/)/[Stylus](https://stylus-lang.com/) to maintain your CSS.  

    * Also employ a naming methodology such as [BEM](https://getbem.com/), [BEVM](https://www.slideshare.net/Jyaasa/bevm-blockelementvariation-modifier) or [CUBE](https://cube.fyi/). 

## General guidance 

1. Semicolons should always be used to terminate all statements, usually enforced through prettier/lint rules. 

1. One statement per line. Single statements following a conditional (if/else) should appear on the same line as the conditional. 

1. Use of the following keywords is not permitted: eval, with and Function. 

1. Use of the following keywords should be avoided (especially with labels): continue, break. 

1. Consider using TDD and Pair-programming whenever practicable. 

1. Variable declaration: Use Const in preference to Let and Let in preference to Var, but there will be valid use cases for using Var. 

1. Equality: Use triple equals `===` in preference to double equals `==` to avoid errors resulting from type cohesion, except when evaluating null/undefined. 

1. Use Object dictionaries in preference to switch statements. 

1. Only use ternary operators to return a single value directly or as a result from function call.

1. Use arrow functions only when the value of 'this' needs to be preserved. 

1. Always use semicolons to terminate statements. 

1. String delimiters: Use template literals (``) over quotes (single or double). 

1. Only use single quotes in JS and double quotes in HTML. 

1. Do not include 'console' method calls in production code. When reporting an error either throw and 'Error' to report an exception or better still call a logging service to maintain an error log. Use log points to debug code in the browser. 

1. Try to avoid mutating state and side-effects by using pure functions as much as possible. 

1. Only use the style attribute in HTML to revise the value of a custom property. 

1. Regular Expression (RegExp) patterns should not be used directly but assigned to a constant with a name that defines exactly what the pattern is expressing.  

    1. Whenever possible "top and/or tail" RegExp patterns using the `^` and `$` symbols. 

    1. Whenever possible bound repetitions.  

        - Instead of using `+` (one or more) or `*` (any number),
        - use `{ 1, UL }`  or `{ 0, UL }`
        - where UL is a reasonable Upper Limit. 

    1. Test, test and test some more. Not just the positive cases but more importantly the negative and edge cases.  

        * Test positive cases 
        * Test negative cases 
        * Test edge cases 


## Observed Don'ts and Does 

The following list are a set of recommendations to improve current practice and make the current code base more consistent with other frontend projects. Links to relevant [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript) pages have been provided. 

| #    | Don't   | Do     |
| :--: | :----- | :----- |
| 1    | Evaluate the length of an array or size of map/set for truth/false. | Use the [truthy](https://developer.mozilla.org/en-US/docs/Glossary/Truthy)/[falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy) nature of the numeric coercion, 0 = false, non-zero = true. |
|| `if (array.length === 0)` | `if (!array.length)` |
|| `if (array.length >= 1)` | `if (array.length)` |
|| `if (string.length < 1)` | `if (!string.length)` |
|| | If you actually need a Boolean value invert (or even double-invert) the result using '!'. |
|| | This also applies when the conditional expression is used in a ternary operation. |
| 2 | Evaluate of a Boolean variable against a Boolean literal | Use the Boolean value directly. This also applies when the conditional expression is using in a ternary operation. |
|| `if (booleanValue === true)` | `if (booleanValue)` |
|| `if (booleanValue !== true)` | `if (!booleanValue)` |
| 3 | Concatenate strings using the plus operator | Use [Template Literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals) (back-tick delimiters with interpolation) |
|| `let fullString = variableOne + ' ' + variableTwo;` | `let fullString = \`${variableOne} ${variableTwo}\`;` |
| 4 | Append items on an array individually when they can be done in a batch. | [See MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/push) |
|| `destinationArray.push(itemOne);` | `destinationArray.push(itemOne, itemTwo, itemThree);` |
|| `destinationArray.push(itemTwo);` ||
|| `destinationArray.push(itemThree);` ||
| 5 | Use a ternary operator to return literal true/false. | Just use the condition, even if it needs inverting. |
|| `let variable = (condition) ? true : false;` | `let variable = condition;` |
|| `return (condition) ? false : true;` | `return !condition;` |
| 6 | Check for the existence of a property in an object using the in operator. | Often using [optional-chaining](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining) will simplify things. |
|| `'time' in props.filters && 'key' in props.filters.time` | `'key' in props.filters?.time` |
|| | Care has to be taken when dealing with properties holding primitive values as the falsy value can provide the same feedback as a null or undefined property. In the example above, if the property 'key' is expected to hold a complex value like an object or array, the following can be used to check the property is valid. |
|| | `props.filters?.time?.key` |
|| | This mechanism can be used to check methods exist before executing them or array elements exist. |
| 7 | Use arrow functions properties in place of methods. This does not include calling methods from within arrow-functions used as event handlers. | Use standards methods. |
|| `class ExampleClass {` | `class ExampleClass { ` |
||  `property = () => {` | ` method() { ` |
|| `    // do some action context of THIS` |  `  // do some action context of THIS ` |
|| ` }` | ` }`| 
|| `}` | `}` |
| 8 | Use the ternary operator for simple conditionals such as: | Use the [logical shortcut &&](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_AND). |
|| `(condition) ? doSomething() : null;  /*Do nothing */` |  `(condition) && doSomething(); `|
|| | Especially in the case of conditional rendering of JSX. |
| 9 | Use the ternary operator to avoid (truthy) value override. | Use the [logical shortcut \|\|](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_OR_assignment). |
|| `let x = (x !== \'\') ? x : y; // keep x if not an empty string, otherwise set to y` | `let x \|\|= y;` |
|10 | **Use the ternary operator to avoid value (non-nullish) override. | Use [nullish assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_nullish_assignment). |
|| `let x = (x === null || x === undefined) ? y : x;` | `let x ??= y;` // only assigns y to x when x is null or undefined |
| 12 | Include presentation logic directly in the style or className attributes. | Declare a function/method to perform the logic and reference it in the attribute. |
|| `<element style={{ fontSize: isBigText ? '2em' : '1em' }} />` | `<element className={getTextSize(isBigText)} />` |
|| | `function getTextSize(isBigText) {`
|| |   `return isBigText ? 'largeTextSize' : 'defaultTextSize';
|| | `}` |

 
