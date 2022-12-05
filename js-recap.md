# JS Recap

- Don’t use `var` anymore (since version ES6)
- single equals `=` is an assignment operator
- double equals `==` is a comparison operator
  - double equals `==` compares value
  - triple equals `===` compares value and type
- primitive types (data that is not an `Object` and has no methods or properties:
  - String
  - Number
  - BigInt
  - Boolean
  - Undefined
  - Symbol
  - Null
- Arrays are Objects (if you declare an array with `const` you can still mutate them (what’s inside) but not re-declare them)
- Block scope: variables declare in a scope `{ ... }` are not available outside that scope. However `var` is Hoisted out to global scope, but its value will probably be `undefined`
- `typeof()` can be used to check the type of a variable
- `Object`'s are non-primitive, they can contain:

  - other `Objects` or variables
  - key-value pairs
  - properties
  - methods (functions)
  - can be created with:

    - Template Literal syntax `let obj = { key: "value" }`
    - Blueprints / Factories to make new objects with the properties:

    ```jsx
    function Person(name, age) {
      this.name = name;
      this.age = age;
    }

    const myPerson = new Person('george', 12);
    ```

- Loops
  - For `for (let i = 1; i < 10; i++) { ... }`
  - For in `for (let key in objects) { ... }`
  - For of `for (let object of objects) { ... }`
  - While `while (condition) { ... }`
  - Do While `do { ... } while (condition)`
- Refactoring - Just write code that is functional first then refactor
  - DRY (Don’t Repeat Yourself)
  - KISS (Keep It Simple Stupid) - except you are not stupid!
- Handling `Date()`'s are tricky, it seems to get and set a current date as soon as you call `new Date()`

  - You can then format a date e.g. to display `YYYY-MM-DD` you can use `Date().toISOSTring().substring(0, 10);` (converts to ISOString format then takes the only the first 10 characters, leaving out the time portion)
  - When using this date to try and set another date e.g. max-date 1 month from now, you can't seem to just use the same date and set the month: `today.setMonth(today.getMonth() + 1);` - don't know why this doesn't work, it's like it doesn't treat `today` as a date object anymore as you can't set it to ISOString afterwards
  - However wrapping it in a new date did work - it probably doesn't matter but might not be strictly correct if it is creating a new date (the time will be slightly different) `const oneMonthFromNow = new Date(today.setSetMonth(today.getMonth() + 1 ));`
