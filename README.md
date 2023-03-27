<details><summary> # example of interface / types / functions / enums / generics / namespaces / modules</summary>
<p> 


## interface
```
interface SomePerson {
    name: string;
    age: number;
    greet(phrase: string): void;
}

let user1: SomePerson;

user1 = {
    name: 'Max',
    age: 30,
    greet(phrase: string) {
        phrase = phrase + ' ' + this.name;
    }
};

```
## type
```
type AddFn = (a: number, b: number) => number;  // type alias for function type (function signature)  
let add: AddFn;                                  
add = (n1: number, n2: number) => {
    return n1 + n2;
};
```

## simple types 
```
let name2: string = 'Max';
let age: number = 30;
let hasHobbies: boolean = true;
```
## array types
```
let hobbies: string[] = ['Sports', 'Cooking'];
let hobbies2: any[] = ['Sports', 1, true];
```
## tuples
```
let address: [string, number] = ['Superstreet', 99];
```
## enums
```
enum Color {
    Gray,   // 0
    Green,  // 1
    Blue    // 2
}

let myColor: Color = Color.Green;
console.log(myColor);   // 1
```
</p>
</details>

<details><summary> Classes </summary>
<p> 

# classes
```
class Person {
    name: string;  // public
    private type: string;   // private 
    protected TheAge: number = 30; // protected

    constructor(name: string, public username: string) { // public username: string is a shortcut for this.username = username; 
        this.name = name;
    }

    printAge() {
        console.log(this.TheAge);
        this.setType('Old Guy'); // can access private method
    }

    private setType(type: string) {
        this.type = type;
        console.log(this.type);
    }
}

const person = new Person('Max', 'max');
console.log(person.name, person.username);
```
## inheritance 
```
class Max extends Person {
    // name = 'Max'; // override name property
    constructor(username: string) {
        super('Max', username);
        this.TheAge = 31;
    }
}

const max = new Max('max');
console.log(max);
```
## getters & setters
```
class Plant {
    private _species: string = 'Default';

    get species() {
        return this._species;
    }

    set species(value: string) {
        if (value.length > 3) {
            this._species = value;
        } else {
            this._species = 'Default';
        }
    }
}

let plant = new Plant();
console.log(plant.species);

plant.species = 'AB';
console.log(plant.species);

plant.species = 'Green Plant';
console.log(plant.species);
```
## static properties & methods
 static properties & methods are attached to the class itself, not to the instances of the class
```
class Helpers {
    static PI: number = 3.14;       
    static calcCircumference(diameter: number): number {
        return this.PI * diameter;
    }
}

console.log(2 * Helpers.PI);
console.log(Helpers.calcCircumference(8));

```
## abstract classes
 abstract classes are base classes from which other classes may be derived. They may not be instantiated directly.
 abstract classes may contain implementation details for its members. The abstract keyword is used to define abstract classes as well as abstract methods within an abstract class.
```
abstract class Project {
    projectName: string = 'Default';
    budget: number = 1000;

    abstract changeName(name: string): void;

    calcBudget() {
        return this.budget * 2;
    }
}

class ITProject extends Project {
    changeName(name: string): void {
        this.projectName = name;
    }
}

let newProject = new ITProject();
console.log(newProject);
newProject.changeName('Super IT Project');
console.log(newProject);
```
## private constructors
 private constructors are used to prevent the class from being instantiated
```
class OnlyOne {
    private static instance: OnlyOne;

    private constructor(public name: string) {}

    static getInstance() {
        if (!OnlyOne.instance) {
            OnlyOne.instance = new OnlyOne('The Only One');
        }
        return OnlyOne.instance;
    }
}

// let wrong = new OnlyOne('The Only One'); // error
let right = OnlyOne.getInstance();
console.log(right.name);
// right.name = 'Something else'; // error
```
## namespaces
 namespaces are used to organize code into logical groups and to provide a way to handle name collisions
```
namespace MyMath {
    const PI = 3.14;

    export function calcCircumference(diameter: number) {
        return diameter * PI;
    }

    export function calcRectangle(width: number, length: number) {
        return width * length;
    }
}

console.log(MyMath.calcCircumference(8));
console.log(MyMath.calcRectangle(8, 20));
```
## modules -
 modules are used to organize code into logical groups and to provide a way to handle name collisions
 modules are executed within their own scope, not in the global scope; this means that variables, functions, classes, etc. declared in a module are not visible outside the module unless they are explicitly exported using one of the export forms.  
```
// module.ts
export class SomeClass {
    public someProperty: string = 'someProperty';
}

// app.ts
 import { SomeClass } from './module';

 let someClass = new SomeClass();
 console.log(someClass.someProperty);
```
## decorators -

 decorators are functions that can be attached to classes, methods, accessors, properties, or parameters. Decorators use the form @expression, where expression must evaluate to a function that will be called at runtime with information about the decorated declaration.
 decorators are a stage 2 proposal for JavaScript and are available as an experimental feature of TypeScript.
 decorators are a TypeScript feature that allow you to add both annotations and a meta-programming syntax for class declarations and members. Decorators are a stage 2 proposal for JavaScript and are available as an experimental feature of TypeScript.
 ```
let logged = function(target: any, propertyName: string | Symbol) {
    console.log(target);
    console.log(propertyName);
}

class Person {
    @logged
    name: string;

    constructor() {
        console.log('Hi!');
    }
}
```
## factory
```
function logging(value: boolean) {
    return value ? logged : null;
}

class Car {
    
        @logging(true)
        name: string;
    
        constructor() {}
    }
```
## advanced
```
function printable(constructorFn: Function) {
    constructorFn.prototype.print = function() {
        console.log(this);
    }
}

@printable
class Plant {
    name = 'Green Plant';
}

const plant = new Plant();
(<any>plant).print();
```
## method decorator
 a method decorator is declared just before a method declaration. The method decorator is applied to the Property Descriptor for the method, and can be used to observe, modify, or replace a method definition.
 a method decorator cannot be used in a declaration file, or in any other ambient context (such as in the body of an ambient function expression).
 a method decorator is applied when the class containing the decorated method is declared. The decorator is called as a function at runtime, with the following three arguments:
 1. For a static member, the constructor function of the class. For an instance member, the prototype of the class.
 2. The name of the member.
 3. The Property Descriptor for the member.
```
function editable(value: boolean) {
    return function(target: any, propName: string, descriptor: PropertyDescriptor) {
        descriptor.writable = value;
    }
}

function overwritable(value: boolean) {
    return function(target: any, propName: string): any {
        const newDescriptor: PropertyDescriptor = {
            writable: value
        };
        return newDescriptor;
    }
}

class Project {
    @overwritable(false)
    projectName: string;

    constructor(name: string) {
        this.projectName = name;
    }

    @editable(false)
    calcBudget() {
        console.log(1000);
    }
}

const project = new Project('Super Project');
project.calcBudget();
project.calcBudget = function() {
    console.log(2000);
}
project.calcBudget();
```
## parameter decorator
 a parameter decorator is declared just before a parameter declaration. A parameter decorator is applied to the constructor function of the class for a static member, or the prototype of the class for an instance member.
 a parameter decorator cannot be used in a declaration file, or in any other ambient context (such as in the body of an ambient function expression).
```
function printInfo(target: any, methodName: string, paramIndex: number) {
    console.log('Target: ', target);
    console.log('methodName: ', methodName);
    console.log('paramIndex: ', paramIndex);
}

class Course {
    name: string;

    constructor(name: string) {
        this.name = name;
    }

    printStudentNumbers(mode: string, @printInfo printAll: boolean) {
        if (printAll) {
            console.log(10000);
        } else {
            console.log(2000);
        }
    }
}

const course = new Course('Super Course');
course.printStudentNumbers('anything', true);
```
</p>
</details>

<details><summary>  OOP - Object Oriented Programming core concepts brief overview</summary>
<p>


## Inheritance -
 is a mechanism in which one object acquires all the properties and behaviors of a parent object. It is an important part of object-oriented programming (OOP) in which one class acquires the properties (methods and fields) of another. With the use of inheritance the information is made manageable in a hierarchical order.
## encapsulation ( get / set) -
 is the mechanism of wrapping the data (variables) and code acting on the data (methods) together as a single unit. In encapsulation, the variables of a class will be hidden from other classes, and can be accessed only through the methods of their current class. Therefore, it is also known as data hiding.
```

class Person {
    private name: string;
    private type: string;
    private age: number = 27;

    constructor(name: string, public username: string) {
        this.name = name;
    }

    printAge() {
        console.log(this.age);
        this.setType("Old Guy");
    }

    private setType(type: string) {
        this.type = type;
        console.log(this.type);
    }
}
```
## PolyMorphism -
 is the ability of a variable, function, or object to take on many forms. The most common use of polymorphism in OOP occurs when a parent class reference is used to refer to a child class object.
 Polymorphism reffering to interfaces and abstract classes - is a design principle that allows a class to be defined by its behavior and not by its attributes. Polymorphism is achieved by using abstract classes and interfaces.
 Polymorphism reffering to inheritance - is a design principle that allows a class to be defined by its behavior and not by its attributes. Polymorphism is achieved by using inheritance.
```
class Car {
    protected name: string;

    constructor(name: string) {
        this.name = name;
    }

    printName() {
        console.log(this.name);
    }
}
```
## Abstraction -
 is the process of hiding the implementation details from the user, only the functionality will be provided to the user. In other words, the user will have the information on what the object does instead of how it does it.
```

class Car {
    protected name: string;

    constructor(name: string) {
        this.name = name;
    }

    printName() {
        console.log(this.name);
    }
}
```
# Interfaces -

 An interface is a syntactical contract that an entity should conform to. An interface defines the syntax that any entity must adhere to. Interfaces are used to achieve abstraction and also to support the concept of loose coupling in software design.
 Interfaces are similar to abstract classes. Both define abstract members that are implemented in derived classes. However, interfaces define only abstract members, whereas abstract classes can define both abstract and non-abstract members. In addition, interfaces cannot contain implementation for their members, whereas abstract classes can. Members of an interface are public by default.
```

interface NamedPerson {
    firstName: string;
    age?: number;
    [propName: string]: any;
    greet(lastName: string): void;
}

function greet(person: NamedPerson) {
    console.log("Hello, " + person.firstName);
}

function changeName(person: NamedPerson) {
    person.firstName = "Anna";
}

const person: NamedPerson = {
    firstName: "Max",
    hobbies: ["Cooking", "Sports"],
    greet(lastName: string) {
        console.log("Hi, I am " + this.firstName + " " + lastName);
    }

}

greet(person);
```
</p>
</details>

<details><summary> 
 GRASP - General Responsibility Assignment Software Patterns</summary>
<p>

 GRASP oop concepts:
        -G -  Generalization 
        -R -  Reusability
        -A -  Abstraction
        -S -  Specialization
        -P -  Polymorphism
## Creator -
 is a class that creates other objects. It is responsible for knowing which classes need to be instantiated. It is also responsible for knowing how the instances of these classes will be created and used.
```

class Person {
    private name: string;
    private age: number;

    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }
}

class PersonFactory {
    static createPerson(name: string, age: number) {
        return new Person(name, age);
    }
}

const person = PersonFactory.createPerson('Max', 27);
```
## Controller - 
is a class that controls the flow of data between the view and the model. It is responsible for knowing which data needs to be displayed and when. It is also responsible for knowing which model objects need to be updated and when.

```
class Person {
    private name: string;
    private age: number;

    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }
}

class PersonFactory {
    static createPerson(name: string, age: number) {
        return new Person(name, age);
    }
}

class PersonController {
    private persons: Person[] = [];

    addPerson(name: string, age: number) {
        const person = PersonFactory.createPerson(name, age);
        this.persons.push(person);
    }
}

const personController = new PersonController();

personController.addPerson('Max', 27);
```
## High Cohesion - 
is a measure of how strongly related the responsibilities of a class are. A class with high cohesion is focused on a single responsibility and has a small number of instance variables. A class with low cohesion has many responsibilities and many instance variables.
```
class Person {
    private name: string;
    private age: number;

    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }
}

class PersonFactory {
    static createPerson(name: string, age: number) {
        return new Person(name, age);
    }
}

class PersonController {
    private persons: Person[] = [];

    addPerson(name: string, age: number) {
        const person = PersonFactory.createPerson(name, age);
        this.persons.push(person);
    }
}

const personController = new PersonController();

personController.addPerson('Max', 27);
```
## Low Coupling -
 is a measure of how dependent one class is on another. A class with low coupling depends on as few other classes as possible. A class with high coupling depends on many other classes.
```
class Person {
    private name: string;
    private age: number;

    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }
}

class PersonFactory {
    static createPerson(name: string, age: number) {
        return new Person(name, age);
    }
}

class PersonController {
    private persons: Person[] = [];

    addPerson(name: string, age: number) {
        const person = PersonFactory.createPerson(name, age);
        this.persons.push(person);
    }
}

const personController = new PersonController();

personController.addPerson('Max', 27);
```
## Inversion of Control -
 is a design principle that allows the control flow of a program to be inverted. Inversion of control is achieved by using a framework that takes control of the flow of a program and delegates the execution of tasks to other objects.
```

class Car {
    drive() {
        console.log('Driving...');
    }
}

class CarFactory {
    static createCar() {
        return new Car();
    }
}

class CarController {
    private car: Car;

    constructor() {
        this.car = CarFactory.createCar();
    }

    drive() {
        this.car.drive();
    }
}

const carController = new CarController();

carController.drive();
```
## Dependency Injection -
 is a design pattern that allows the removal of hard-coded dependencies and makes it possible to change them, whether at runtime or compile time.
```
class cat {
    meow() {
        console.log('Meow!');
    }
}

class CatFactory {
    static createCat() {
        return new Cat();
    }
}

class CatController {
    private cat: Cat;

    constructor(cat: Cat) {
        this.cat = cat;
    }

    meow() {
        this.cat.meow();
    }
}

const cat = CatFactory.createCat();
const catController = new CatController(cat);

catController.meow();
```
</p>
</details>



<details><summary> Functional Programing / Async - await</summary>
<p>

## destructuring

```
let array = [1, 2, 3, 4, 5];

let [a, b, c, d, e] = array;

```

## spread operator
```
let array = [1, 2, 3, 4, 5];

let array2 = [...array, 6, 7, 8, 9, 10];

```
## rest operator
```
function sum(...args: number[]): number {
    let sum = 0;
    for (let arg of args) {
        sum += arg;
    }
    return sum;
    }

```

## default parameters
```
function sum(a: number, b: number = 0): number {
    return a + b  ;
    }
```


## arrow functions
```
let sum = (a: number, b: number): number => a + b;
```

# map / filter / reduce / sort / forEach / split / join / slice / splice / toString 

# map
map creates a new array with the results of calling a provided function on every element in the calling array.
```
let array = [1, 2, 3, 4, 5];
let items = {
    name: 'alex',price: 10,
    name: 'alex2',price: 20,
    name: 'alex3',price: 30,
}
```
```
let array2 = array.map((value) => value * 2); 
let items2 = items.map((value) => value.price * 2);
```
# filter
filter creates a new array with all elements that pass the test implemented by the provided function.
```
let array2 = array.filter((value) => value > 3);
let items2 = items.filter((value) => value.price > 10);
```
# reduce
reduce applies a function against an accumulator and each element in the array (from left to right) to reduce it to a single value.
```
let array2 = array.reduce((accumulator, currentValue) => accumulator + currentValue);
let items2 = items.reduce((accumulator, currentValue) => accumulator + currentValue.price);
```
# sort
sort sorts the elements of an array in place and returns the sorted array.
```
let array2 = array.sort((a, b) => a - b);
let items2 = items.sort((a, b) => a.price - b.price); //sort by price
```
# forEach
forEach executes a provided function once for each array element.
```
array.forEach((value) => console.log(value));
```
# split
split splits a String object into an array of strings by separating the string into substrings.
```
let string = '12345';

let array = string.split('');
```

# join
join joins all elements of an array into a string.
```
let string = array.join('');
```

# slice
slice extracts a section of a string and returns it as a new string, without modifying the original string.
```
let string2 = string.slice(2);
```

# splice
splice changes the contents of an array by removing or replacing existing elements and/or adding new elements in place.
```
let array2 = array.splice(2, 1);
```
toString
toString returns a string representing the specified array and its elements.
```
let string = array.toString();
```
# async / await
async / await is a way to write asynchronous code that looks synchronous.
async / await is built on top of promises.
asyncronous code is code that is not executed in order and is executed at a later time.
it is superior to synchronous code because it does not block the execution of other code.

```

let asyncFunc = async () => {
    try {
        let MapFilter = await MapFilter();
        return MapFilter;
    } catch (error) {
        console.log(error);
    }
    }

let MapFilter = () => {
    let array = [1, 2, 3, 4, 5];
    let array2 = array.map((value) => value * 2).filter((value) => value > 3);
    return array2;
    }

asyncFunc().then((result) => console.log(result));
```

</p>
</details>




<details><summary> 
 Functional programing concepts</summary>
<p>
 1. Pure functions ,
 2. Immutability
 3. First class functions
 4. Higher order functio
 5. Currying
 6. Composition
 7. Point free style
 8. Lazy evaluation
 9. Recursion
 10. Referential transparency
 11. Algebraic data types
 12. Pattern matching
 13. Type classes
 14. Monads
 15. Functors
 16. Applicatives
 17. Monoids


# 1. Pure functions
 A pure function is a function that has no side effects and always returns the same result given the same arguments.
 Pure functions are idempotent, meaning that they can be called multiple times with the same arguments without changing the result or state of the program.
 Pure functions are also referentially transparent, meaning that they can be replaced with their return value without changing the behavior of the program.
 Pure functions are easier to test, compose, and reason about than impure functions.

# 2. Immutability
 Immutability is a state in which an object cannot be modified after it is created.
 Immutability is a core concept in functional programming.
 Immutability makes it easier to reason about your code because you know that an object will never change.
 Immutability also makes it easier to test your code because you don't have to worry about the state of an object changing during a test.
 Immutability is also a performance optimization because it allows JavaScript engines to make certain assumptions about your code that they would not be able to make if your code were mutable.

# 3. First class functions
 A first class function is a function that can be assigned to a variable, passed as an argument to another function, or returned from another function.
 First class functions are a core concept in functional programming.
 First class functions allow you to abstract over actions, not just values.
 First class functions allow you to treat functions as values and pass functions as arguments to other functions, which is called higher order functions.

# 4. Higher order functions
 A higher order function is a function that takes a function as an argument, returns a function, or both.
 Higher order functions are a core concept in functional programming.
 Higher order functions allow you to abstract over actions, not just values.
 Higher order functions allow you to treat functions as values and pass functions as arguments to other functions, which is called higher order functions.

# 5. Currying
 Currying is the process of transforming a function that takes multiple arguments into a function that takes them one at a time.
 Currying is a core concept in functional programming.
 Currying is useful for partial application.
 Currying is useful for creating reusable, composable functions.

# 6. Composition
 Composition is the process of combining two or more functions to produce a new function.
 Composition is a core concept in functional programming.
 Composition is useful for creating reusable, composable functions.

```
const compose = (f, g) => x => f(g(x));
const toUpperCase = x => x.toUpperCase();
const exclaim = x => x + '!';
const shout = compose(exclaim, toUpperCase);
shout('send in the clowns');
```
# 7. Point free style
 Point free style is the process of composing functions without explicitly mentioning the arguments to the composed functions.
 Point free style is a core concept in functional programming.
 Point free style is useful for creating reusable, composable functions.

# 8. Lazy evaluation
 Lazy evaluation is the process of deferring the evaluation of an expression until its value is needed.
 Lazy evaluation is a core concept in functional programming.
 Lazy evaluation is useful for creating reusable, composable functions.

```
const repeat = (str, times) => {
  let result = '';
  for (let i = 0; i < times; i++) {
    result += str;
  }
  return result;
}
```

# 9. Recursion
 Recursion is the process of defining something in terms of itself.
 Recursion is a core concept in functional programming.
 Recursion is useful for creating reusable, composable functions.
```
const repeat2 = (str, times, result = '') => {
    if (times <= 0) {
        return result;
    }
    return repeat(str, times - 1, result + str);
    }
const repeat3 = (str, times) => times <= 0 ? '' : repeat(str, times - 1, str + str);
```

# 10. Referential transparency
 Referential transparency is the property of an expression that can be replaced with its value without changing the behavior of the program.

# 11. Algebraic data types
 An algebraic data type is a type that is defined by its values.
 Algebraic data types are a core concept in functional programming.

# 12. Pattern matching
 Pattern matching is the process of checking a value against a pattern.

# 13. Type classes
 A type class is a set of types that share certain common behaviors.

# 14. Monads
 A monad is a type that implements the monad interface by providing a flatMap method.

# 15. Functors
 A functor is a type that implements the functor interface by providing a map method.

# 16. Applicatives
 An applicative is a type that implements the applicative interface by providing an ap method.

# 17. Monoids
 A monoid is a type that implements the monoid interface by providing an empty method and a concat method.





# call by reference 
 means that the object is passed by reference, not by value.
 The reference is passed to the function, so if the function changes the object's properties, that change is visible outside the function, as shown in the following example:
 ```
const one = {
  name: 'one',
}

const two = one;

two.name = 'two';

console.log(one.name); // two
```
# call by value
 means that the object is passed by value, not by reference.
 The value is passed to the function, so if the function changes the object's properties, that change is not visible outside the function, as shown in the following example:
```
const one2 = {
  name: 'one',
}

const two2 = {
  ...one2,
};

two2.name = 'two';

console.log(one2.name); // one
```
## map / filter / reduce prototype methods

#map
v
let myMap = [1, 2, 3, 4, 5].map((item) => {
  return item * 2;
}

Array.prototype.myMap  = function (callback ) {
  let result = [];
  for (let i = 0; i < this.length; i++) {
    result.push(callback(this[i], i, this));  // callback(item, index, array)
  }
  return result ;
}

```
#filter
```
let myFilter = [1, 2, 3, 4, 5].filter((item) => {
  return item > 2;
}

Array.prototype.myFilter = function (callback) {
  let result = [];
  for (let i = 0; i < this.length; i++) {
    if (callback(this[i], i, this)) {  // callback(item, index, array)
      result.push(this[i]);
    }
```
#reduce
```
let myReduce = [1, 2, 3, 4, 5].reduce((acc, item) => {
  return acc + item;
}

Array.prototype.myReduce = function (callback, initialValue) {
  let acc = initialValue;
  let i = 0;
  if (initialValue === undefined) {
    acc = this[0];
    i = 1;
  }
  for (i; i < this.length; i++) {
    acc = callback(acc, this[i], i, this);  // callback(acc, item, index, array)
  }
  return acc;
}
```