- a prototype is another object that is used as a fallback source of properties
    - when an object gets a request for a property it does not have, its prototype will be searched for the property
    - ex: Object.prototype is the top level prototype of objects in JS
        - contains methods like toString
    - you can use Object.create to create an object with a specific prototype
    ```js
    let protoRabbit = {
        speak(line) {
            console.log(`The ${this.type} rabbit says '${line}'`);
        }
    };
    let killerRabbit = Object.create(protoRabbit);
    killerRabbit.type = "killer";
    killerRabbit.speak("SKREEEE!");
    // → The killer rabbit says 'SKREEEE!'
    ```
- a class defines the shape of a type of object - what methods and properties it has, where an object created from a class is an instance of the class
    - to create an instance of a class, you have to make an object that derives from the proper prototype
        - in addition you need to ensure that the object has properties that instances of the class are supposed to have
            - this is what a *constructor* function does
    - constructors automatically get a property names *prototype* that by default holds a plain, empty object that derives from Object.prototype.
    - names of constructors are capitalized
    ```js
    class Rabbit {
        constructor(type) {
            this.type = type;
        }
        speak(line) {
            console.log(`The ${this.type} rabbit says '${line}'`);
            }
        }

        let killerRabbit = new Rabbit("killer");
        let blackRabbit = new Rabbit("black");
    ```
    - the method named *constructor* will be bound to the name of the class as the constructor function
        - the rest of the methods are packages into that constructor's prototype
- overriding derived prototypes:
    ```js
    Rabbit.prototype.teeth = "small";
    console.log(killerRabbit.teeth);
    // → small
    killerRabbit.teeth = "long, sharp, and bloody";
    console.log(killerRabbit.teeth);
    // → long, sharp, and bloody
    console.log(blackRabbit.teeth);
    // → small
    console.log(Rabbit.prototype.teeth);
    // → small
    ```
    - you can override properties in instances of a more generic class while letting nonexceptional objects take a standard value from their prototype

- object property names must be strings
    - if you need a map whose keys can't easily be converted to streings - such as objects - you cannot use an object as a map
    - javascript comes with a class called Map that is written for this purpose though:
    ```js
    let ages = new Map();
    ages.set("Boris", 39);
    ages.set("Liang", 22);
    ages.set("Júlia", 62);

    console.log(`Júlia is ${ages.get("Júlia")}`);
    // → Júlia is 62
    console.log("Is Jack's age known?", ages.has("Jack"));
    // → Is Jack's age known? false
    console.log(ages.has("toString"));
    // → false
    ```
- object property names can also be symbols
    - symbols are values created with the Symbol function
    - newly created symbols are unique, you cannot create the same symbol twice
    - the string you pass to Sybol is included when you convert it to a string and can make it easier to recognize a symbol when showing it in the console
    ```js
    const toStringSymbol = Symbol("toString");
    Array.prototype[toStringSymbol] = function() {
    return `${this.length} cm of blue yarn`;
    };

    console.log([1, 2].toString());
    // → 1,2
    console.log([1, 2][toStringSymbol]());
    // → 2 cm of blue yarn
    ```
    ```js
    let stringObject = {
        [toStringSymbol]() { return "a jute rope"; }
    };
    console.log(stringObject[toStringSymbol]());
    // → a jute rope
    ```
- the object given to a for/of loop is expected to be *iterable*
    - this means it has a method named with the *Symbol.iterator* symbol
    - when called, that method should return an object that provides a second interface, *iterator*
        - this is the actual thing that iterates
        - it has a *next* method that returns the next result
        - that result should be an object with a *value* property that provides the next value if there is one, and a *done* property which should be true when there are no more results and false otherwise
    - note that the *next, value*, and *done* property names are plain strings, not symbols
    - only *Symbol.iterator* which is likely to be added to a *lot* of different objects, is an actual symbol
    ```js
    let okIterator = "OK"[Symbol.iterator]();
    console.log(okIterator.next());
    // → {value: "O", done: false}
    console.log(okIterator.next());
    // → {value: "K", done: false}
    console.log(okIterator.next());
    // → {value: undefined, done: true}
    ```
    
