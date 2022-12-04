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