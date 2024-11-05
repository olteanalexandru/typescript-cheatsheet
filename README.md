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

## union types
```
function combine(input1: number | string, input2: number | string) {
    let result;
    if (typeof input1 === 'number' && typeof input2 === 'number') {
        result = input1 + input2;
    } else {
        result = input1.toString() + input2.toString();
    }
    return result;
}

const combinedAges = combine(30, 26);
const combinedNames = combine('Max', 'Anna');
```

## literal types
```
function printText(s: string, alignment: 'left' | 'right' | 'center') {
    console.log(s, alignment);
}

printText('Hello, world', 'left');
```

## type guards
```
type Admin = {
    name: string;
    privileges: string[];
};

type Employee = {
    name: string;
    startDate: Date;
};

type ElevatedEmployee = Admin & Employee;

function printEmployeeInformation(emp: ElevatedEmployee) {
    console.log('Name: ' + emp.name);
    if ('privileges' in emp) {
        console.log('Privileges: ' + emp.privileges);
    }
    if ('startDate' in emp) {
        console.log('Start Date: ' + emp.startDate);
    }
}
```

## intersection types
```
type Combinable = string | number;
type Numeric = number | boolean;

type Universal = Combinable & Numeric;
```

## function overloads
```
function add(a: number, b: number): number;
function add(a: string, b: string): string;
function add(a: Combinable, b: Combinable) {
    if (typeof a === 'string' || typeof b === 'string') {
        return a.toString() + b.toString();
    }
    return a + b;
}

const result = add('Max', ' Schwarz');
result.split(' ');
```

## optional chaining
```
const fetchedUserData = {
    id: 'u1',
    name: 'Max',
    job: { title: 'CEO', description: 'My own company' }
};

console.log(fetchedUserData?.job?.title);
```

## nullish coalescing
```
const userInput = null;

const storedData = userInput ?? 'DEFAULT';

console.log(storedData);
```

## type assertions
```
let someValue: unknown = 'this is a string';

let strLength: number = (someValue as string).length;
```

## index types
```
interface ErrorContainer {
    [prop: string]: string;
}

const errorBag: ErrorContainer = {
    email: 'Not a valid email!',
    username: 'Must start with a capital character!'
};
```

## keyof type operator
```
type Person = {
    name: string;
    age: number;
};

function getProperty<T, K extends keyof T>(obj: T, key: K) {
    return obj[key];
}

const person: Person = { name: 'Max', age: 30 };
const personName = getProperty(person, 'name');
```

## mapped types
```
type ReadonlyPerson = {
    readonly [K in keyof Person]: Person[K];
};

const readonlyPerson: ReadonlyPerson = { name: 'Max', age: 30 };
// readonlyPerson.name = 'Anna'; // Error: Cannot assign to 'name' because it is a read-only property.
```

## conditional types
```
type NonNullable<T> = T extends null | undefined ? never : T;

type Example = NonNullable<string | number | undefined>; // string | number
```

## utility types
```
type PartialPerson = Partial<Person>;
const partialPerson: PartialPerson = { name: 'Max' };

type RequiredPerson = Required<Person>;
const requiredPerson: RequiredPerson = { name: 'Max', age: 30 };

type ReadonlyPerson = Readonly<Person>;
const readonlyPerson: ReadonlyPerson = { name: 'Max', age: 30 };

type Record<K extends keyof any, T> = {
    [P in K]: T;
};
const nameAgeMap: Record<string, number> = {
    Max: 30,
    Anna: 28
};
```

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
        super('Max', username);  // call parent constructor
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
 SOLID</summary>
<p>

SOLID is a set of principles for object-oriented design and programming.

# S - Single responsibility principle
 A class should have one and only one reason to change, meaning that a class should have only one job.
# O - Open/closed principle
 Objects or entities should be open for extension, but closed for modification.
 --think of (if elses are ussualy a sign of violation of this principle and can be replaced with polymorphism )
-- multiple classes could be created that implement the same interface and then the correct class is chosen at runtime or 
-- make use of switches instead of if else statements
# L - Liskov substitution principle
 This principle states that "objects in a program should be replaceable with instances of their subtypes without altering the correctness of that program."
 --objects of a superclass shall be replaceable with objects of its subclasses without affecting the functionality of the program
--subclasses must implement all the methods of the superclass and not overwrite logic
--subclasses should not throw exceptions that are not thrown by the superclass 


-- in such cases the superclass should be refactored  or multiple interfaces/classes should be created to handle the different cases
 # I - Interface segregation principle
 This principle states that "many client-specific interfaces are better than one general-purpose interface."
 --a client should never be forced to implement an interface that it doesn't use completely 
--interfaces should be broken down into smaller interfaces that are specific to the client
 # D - Dependency inversion principle
 This principle states that "one should "depend upon abstractions, [not] concretions."
--high level modules should not depend on low level modules
--both should depend on abstractions ( think of middleMans that handle the communication between the two )


## Single responsibility principle
```
class User {
  constructor(name, email) {
    this.name = name;
    this.email = email;
  }

  changeEmail(newEmail) {
    this.email = newEmail;
  }
}
```
# Open/closed principle
```
class Shape {
  constructor(type) {
    this.type = type;
  }
}

class Circle extends Shape {
  constructor() {
    super('circle');
  }
}

class Square extends Shape {
  constructor() {
    super('square');
  }
}

class AreaCalculator {
  constructor(shapes = []) {
    this.shapes = shapes;
  }

  sum() {
    return this.shapes.reduce((acc, shape) => {
      if (shape.type === 'circle') {
        acc += (shape.radius ** 2) * Math.PI;
      }

      if (shape.type === 'square') {
        acc += shape.side ** 2;
      }

      return acc;
    }, 0);
  }
}

const calc = new AreaCalculator([
  new Circle(2),
  new Square(5),
  new Square(6),
]);

console.log(calc.sum()); // 113.09733552923255
```
## Liskov substitution principle
```
class Person {
  constructor(name) {
    this.name = name;
  }

  walk() {
    return `${this.name} is walking`;
  }
}

class Employee extends Person {
  constructor(name, title) {
    super(name);
    this.title = title;
  }

  walk() {
    return `${this.name}, ${this.title}, is walking`;
  }
}

const p = new Person('John');

console.log(p.walk()); // John is walking


```

# Interface segregation principle
```
class Animal {
  constructor(name) {
    this.name = name;
  }

  eat() {
    return `${this.name} is eating`;
  }

  sleep() {
    return `${this.name} is sleeping`;
  }
}


```

# Dependency inversion principle
```
class Fetch {
  request(url) {
    // return fetch(url).then(r => r.json());
  }
}

class LocalStorage {
  get() {
    const dataFromLocalStorage = 'data from local storage';

    return dataFromLocalStorage;
  }
}

class FetchClient {

  constructor() {
    this.fetch = new Fetch();
  }

  clientGet() {
    return this.fetch.request('vk.com');
  }
}

class LocalStorageClient {

  constructor() {
    this.localStorage = new LocalStorage();
  }

  clientGet() {
    return this.localStorage.get();
  }
}

class Database {

  constructor(client) {
    this.client = client;
  }

  getData(key) {
    return this.client.clientGet(key);
  }
}

const db = new Database(new FetchClient());

console.log(db.getData('rand')); // data from fetch

const db2 = new Database(new LocalStorageClient());

console.log(db2.getData('rand')); // data from local storage
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

let [a, b, c, d, e] = array;  // a = 1, b = 2, c = 3, d = 4, e = 5

```

## spread operator
```
let array = [1, 2, 3, 4, 5];  

let array2 = [...array, 6, 7, 8, 9, 10];  // array2 = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

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

# Array / Object methods 

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
# flatMap
flatMap first maps each element using a mapping function, then flattens the result into a new array. It is identical to a map followed by a flat of depth 1, but flatMap is often quite useful, as merging both into one method is slightly more efficient.
```
let array2 = array.flatMap((value) => [value, value * 2]);
let items2 = items.flatMap((value) => [value.price, value.price * 2]);
```



# filter
filter creates a new array with all elements that pass the test implemented by the provided function.

```
let array2 = array.filter((value) => value > 3);
let items2 = items.filter((value) => value.price > 10);
```

# 

# reduce
reduce applies a function against an accumulator and each element in the array (from left to right) to reduce it to a single value.
```
let array2 = array.reduce((accumulator, currentValue) => accumulator + currentValue);
let items2 = items.reduce((accumulator, currentValue) => accumulator + currentValue.price);
```

# findIndex
findIndex returns the index of the first element in the array that satisfies the provided testing function. Otherwise, it returns -1, indicating that no element passed the test.
```
let value = array.findIndex((value) => value > 3);
let item = items.findIndex((value) => value.price > 10);
```

# find
find returns the value of the first element in the array that satisfies the provided testing function.
```
let value = array.find((value) => value > 3);
let item = items.find((value) => value.price > 10);
```
# some
some tests whether at least one element in the array passes the test implemented by the provided function.
```
let value = array.some((value) => value > 3);
let item = items.some((value) => value.price > 10);
```
# every
every tests whether all elements in the array pass the test implemented by the provided function.
```
let value = array.every((value) => value > 3);
let item = items.every((value) => value.price > 10);
```
# includes
includes determines whether an array includes a certain value among its entries, returning true or false as appropriate.
```
let value = array.includes(3);
let item = items.includes(10);
```

# indexOf
indexOf returns the first index at which a given element can be found in the array, or -1 if it is not present.
```
let value = array.indexOf(3);
let item = items.indexOf(10);
```
# push
push adds one or more elements to the end of an array and returns the new length of the array.
```
array.push(4);
array.push(5, 6);
```
# pop
pop removes the last element from an array and returns that element.
```
let value = array.pop();
```
# shift
shift removes the first element from an array and returns that element.
```
let value = array.shift();
```
# unshift
unshift adds one or more elements to the beginning of an array and returns the new length of the array.
```
array.unshift(0);
array.unshift(-1, -2);
```
# concat
concat merges two or more arrays and returns a new array.
```
let array2 = array.concat([6, 7, 8, 9, 10]);
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
  String functional methods and other useful methods </summary>
<p>

# String methods
# charAt
charAt returns the character at the specified index in a string.
```
let string = 'hello';

let char = string.charAt(0);
```
# charCodeAt
charCodeAt returns the Unicode of the character at the specified index in a string.
```
let string = 'hello';

let charCode = string.charCodeAt(0);
```
# concat
concat joins two or more strings and returns a new string.
```
let string2 = string.concat(' world');
```
# includes
includes determines whether one string may be found within another string, returning true or false as appropriate.
```
let value = string.includes('ell');
```
# indexOf
indexOf returns the index within the calling String object of the first occurrence of the specified value, starting the search at fromIndex. Returns -1 if the value is not found.
```
let value = string.indexOf('l');
```
# lastIndexOf
lastIndexOf returns the index within the calling String object of the last occurrence of the specified value, searching backwards from fromIndex. Returns -1 if the value is not found.
```
let value = string.lastIndexOf('l');
```
# match
match retrieves the result of matching a string against a regular expression.
```
let value = string.match(/l/g);
```
# replace
replace searches a string for a specified value, or a regular expression, and returns a new string where the specified values are replaced.
```
let string2 = string.replace('l', 'L');
```
# search
search searches a string for a specified value, or regular expression, and returns the position of the match.
```
let value = string.search('l');
```
# slice
slice extracts a section of a string and returns it as a new string, without modifying the original string.
```
let string2 = string.slice(2);
```
# split
split splits a String object into an array of strings by separating the string into substrings.
```
let value = string.split('l');
```
# substr
substr extracts parts of a string, beginning at the character at the specified position, and returns the specified number of characters.
```
let value = string.substr(2, 3);
```
# substring
substring extracts parts of a string, between the start and end indexes, and returns the specified number of characters.
```
let value = string.substring(2, 4);
```
# toLowerCase
toLowerCase converts a string to lowercase letters.
```
let string2 = string.toLowerCase();
```
# toUpperCase
toUpperCase converts a string to uppercase letters.
```
let string2 = string.toUpperCase();
```
# trim
trim removes whitespace from both ends of a string.
```
let string2 = ' hello ';

let string3 = string2.trim();
```
# padStart
padStart pads the current string with another string until the resulting string reaches the given length.
```
let string2 = string.padStart(10, '0');
```
# padEnd
padEnd pads the current string with another string until the resulting string reaches the given length.
```
let string2 = string.padEnd(10, '0');
```
# repeat
repeat returns a new string with a specified number of copies of the string it was called on.
```
let string2 = string.repeat(3);
```
# startsWith
startsWith determines whether a string begins with the characters of a specified string, returning true or false as appropriate.
```
let value = string.startsWith('he');
```
# endsWith
endsWith determines whether a string ends with the characters of a specified string, returning true or false as appropriate.
```
let value = string.endsWith('lo');
```
# trimStart
trimStart removes whitespace from the beginning of a string.
```
let string2 = ' hello ';

let string3 = string2.trimStart();
```
# trimEnd
trimEnd removes whitespace from the end of a string.
```
let string2 = ' hello ';

let string3 = string2.trimEnd();
```
# String.fromCharCode
fromCharCode converts Unicode values to characters.
```
let value = String.fromCharCode(104, 101, 108, 108, 111);
```
# String.fromCodePoint
fromCodePoint returns a string created by using the specified sequence of code points.
```
let value = String.fromCodePoint(104, 101, 108, 108, 111);
```
# String.raw
raw returns a string created by using the raw string and template literal.
```
let value = String.raw`Hello\nWorld`;
```


# Other useful methods 

# isNaN
isNaN determines whether a value is NaN or not.
```
let value = isNaN('hello');
```
# isFinite
isFinite determines whether a value is a finite number.
```
let value = isFinite(Infinity);
```
# parseFloat
parseFloat parses a string and returns a floating-point number.
```
let value = parseFloat('3.14');
```
# parseInt
parseInt parses a string and returns an integer.
```
let value = parseInt('3.14');
```
# setTimeout
setTimeout calls a function or evaluates an expression after a specified number of milliseconds.
```
setTimeout(() => console.log('Hello'), 1000);
```
# setInterval
setInterval calls a function or evaluates an expression at specified intervals (in milliseconds).
```
setInterval(() => console.log('Hello'), 1000);
```
# clearInterval
clearInterval stops the intervals set by setInterval.
```
let interval = setInterval(() => console.log('Hello'), 1000);

clearInterval(interval);
```
# clearTimeout
clearTimeout stops the timeouts set by setTimeout.
```
let timeout = setTimeout(() => console.log('Hello'), 1000);

clearTimeout(timeout);
```
# Math.random
random returns a random number between 0 (inclusive) and 1 (exclusive).
```
let value = Math.random();
```
# Math.floor
floor returns the largest integer less than or equal to a given number.
```
let value = Math.floor(3.14);
```
# Math.ceil
ceil returns the smallest integer greater than or equal to a given number.
```
let value = Math.ceil(3.14);
```
# Math.round
round returns the value of a number rounded to the nearest integer.
```
let value = Math.round(3.14);
```
# Math.min
min returns the smallest of zero or more numbers.
```
let value = Math.min(1, 2, 3, 4, 5);
```
# Math.max
max returns the largest of zero or more numbers.
```
let value = Math.max(1, 2, 3, 4, 5);
```
# Math.abs
abs returns the absolute value of a number.
```
let value = Math.abs(-3.14);
```
# Math.pow
pow returns the base to the exponent power.
```
let value = Math.pow(2, 3);
```
# Math.sqrt
sqrt returns the square root of a number.
```
let value = Math.sqrt(9);
```










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

# map

```
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

</p>
</details>


<details><summary> 
OOP - Func   Mixin pattern
</summary>



## Mixin pattern



1. Mixin Classes
Two mixin classes are defined:

CanSayHi: A class that provides a sayHi method.
HasSuperPower: A class that provides a superpower method.

```
class CanSayHi {
name ;
sayHi() {
   return `Hi, I am ${this.name}`;
}
}

class HasSuperPower {
heroName ;

superpower() {
   return `${this.heroName} can fly`;
}

}

```



2. Target Class
The superHero class is the target class that will incorporate the mixins. It implements both CanSayHi and HasSuperPower.

```

class superHero implements CanSayHi, HasSuperPower {
heroName 

constructor(public name: string) {
   this.heroName = name;
}

sayHi: () => string;
superpower: () => string;

}
```



3. Applying Mixins
The applyMixins function is defined to apply mixins to the target class. It copies the methods from mixin classes to the target class prototype.
 ```



function applyMixins(derivedCtor: any, baseCtors: any[]) {
baseCtors.forEach(baseCtor => {
   Object.getOwnPropertyNames(baseCtor.prototype).forEach(name => {
       derivedCtor.prototype[name] = baseCtor.prototype[name];
   });
});
}

 ```



4. Usage
Mixins are applied to the superHero class using applyMixins. An instance of superHero is then created, and both mixin methods are called.
```

 applyMixins(superHero, [CanSayHi, HasSuperPower]);

let hero = new superHero('Superman');

console.log(hero.sayHi());
console.log(hero.superpower());

```

</p>
</details>

<details>
<summary>Ultimate LeetCode Problem-Solving Cheatsheet</summary>

### 1. Data Structure Fundamentals

#### Arrays

```typescript
// Initialize
const arr: number[] = [];
const fixed: number[] = new Array(5).fill(0);  // [0,0,0,0,0]
const matrix: number[][] = Array(3).fill(0).map(() => Array(4).fill(0));

// Key Methods
arr.push(1);       // Add to end: O(1)
arr.pop();         // Remove from end: O(1)
arr.unshift(1);    // Add to start: O(n)
arr.shift();       // Remove from start: O(n)
arr.splice(2,1);   // Remove at index: O(n)

// Slice without modifying original
const subArray = arr.slice(startIdx, endIdx);  // O(n)

// Common Array Patterns
const sum = arr.reduce((a, b) => a + b, 0);
const max = Math.max(...arr);
const min = Math.min(...arr);
```

#### Maps & Sets

```typescript
// Map for key-value pairs
const map = new Map<string, number>();
map.set("key", 1);
map.get("key");
map.has("key");
map.delete("key");

// Set for unique values
const set = new Set<number>();
set.add(1);
set.has(1);
set.delete(1);
set.size;

// Frequency Counter Pattern
function createFrequencyMap(arr: number[]): Map<number, number> {
    const freq = new Map();
    for (const num of arr) {
        freq.set(num, (freq.get(num) || 0) + 1);
    }
    return freq;
}
```

### 2. Common Problem-Solving Patterns

#### Two Pointers Pattern

```typescript
// Two pointers from ends (e.g., for sorted arrays)
function twoSum(nums: number[], target: number): number[] {
    let left = 0, right = nums.length - 1;
    
    while (left < right) {
        const sum = nums[left] + nums[right];
        if (sum === target) return [left, right];
        if (sum < target) left++;
        else right--;
    }
    return [];
}

// Fast & Slow Pointers (e.g., for linked lists)
function hasCycle(head: ListNode | null): boolean {
    let slow = head, fast = head;
    
    while (fast && fast.next) {
        slow = slow!.next;
        fast = fast.next.next;
        if (slow === fast) return true;
    }
    return false;
}
```

#### Sliding Window Pattern

```typescript
// Fixed Window
function findMaxAverage(nums: number[], k: number): number {
    let sum = nums.slice(0, k).reduce((a, b) => a + b, 0);
    let max = sum;
    
    for (let i = k; i < nums.length; i++) {
        sum = sum - nums[i - k] + nums[i];
        max = Math.max(max, sum);
    }
    return max / k;
}

// Dynamic Window
function longestSubstringWithoutRepeats(s: string): number {
    const seen = new Set();
    let left = 0, max = 0;
    
    for (let right = 0; right < s.length; right++) {
        while (seen.has(s[right])) {
            seen.delete(s[left]);
            left++;
        }
        seen.add(s[right]);
        max = Math.max(max, right - left + 1);
    }
    return max;
}
```

#### Binary Search Pattern

```typescript
function binarySearch(nums: number[], target: number): number {
    let left = 0, right = nums.length - 1;
    
    while (left <= right) {
        const mid = left + Math.floor((right - left) / 2);
        if (nums[mid] === target) return mid;
        if (nums[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return -1;
}

// Binary Search on Answer Space
function findMinimumTime(tasks: number[]): number {
    let left = 1, right = 10**9;
    
    while (left < right) {
        const mid = left + Math.floor((right - left) / 2);
        if (canComplete(tasks, mid)) right = mid;
        else left = mid + 1;
    }
    return left;
}
```

### 3. Tree Traversal Patterns

#### DFS (Depth-First Search)

```typescript
// Recursive DFS
function dfs(root: TreeNode | null): void {
    if (!root) return;
    
    // Pre-order
    console.log(root.val);
    dfs(root.left);
    dfs(root.right);
    
    // In-order
    // dfs(root.left);
    // console.log(root.val);
    // dfs(root.right);
    
    // Post-order
    // dfs(root.left);
    // dfs(root.right);
    // console.log(root.val);
}

// Iterative DFS using Stack
function dfsIterative(root: TreeNode | null): number[] {
    if (!root) return [];
    const result: number[] = [];
    const stack = [root];
    
    while (stack.length) {
        const node = stack.pop()!;
        result.push(node.val);
        if (node.right) stack.push(node.right);
        if (node.left) stack.push(node.left);
    }
    return result;
}
```

#### BFS (Breadth-First Search)

```typescript
function bfs(root: TreeNode | null): number[] {
    if (!root) return [];
    const result: number[] = [];
    const queue = [root];
    
    while (queue.length) {
        const levelSize = queue.length;
        
        for (let i = 0; i < levelSize; i++) {
            const node = queue.shift()!;
            result.push(node.val);
            if (node.left) queue.push(node.left);
            if (node.right) queue.push(node.right);
        }
    }
    return result;
}
```

### 4. Dynamic Programming Patterns

#### Memoization Template

```typescript
function memoize<T, R>(fn: (...args: T[]) => R): (...args: T[]) => R {
    const cache = new Map<string, R>();
    
    return (...args: T[]): R => {
        const key = JSON.stringify(args);
        if (cache.has(key)) return cache.get(key)!;
        const result = fn(...args);
        cache.set(key, result);
        return result;
    };
}

// Example Usage
const fib = memoize((n: number): number => {
    if (n <= 1) return n;
    return fib(n - 1) + fib(n - 2);
});
```

#### Tabulation Template

```typescript
function fibTabulation(n: number): number {
    if (n <= 1) return n;
    const dp = new Array(n + 1).fill(0);
    dp[1] = 1;
    
    for (let i = 2; i <= n; i++) {
        dp[i] = dp[i-1] + dp[i-2];
    }
    return dp[n];
}
```

### 5. Graph Algorithms

#### DFS for Graphs

```typescript
function dfsGraph(graph: Map<number, number[]>, start: number): Set<number> {
    const visited = new Set<number>();
    
    function dfs(node: number): void {
        visited.add(node);
        for (const neighbor of graph.get(node) || []) {
            if (!visited.has(neighbor)) {
                dfs(neighbor);
            }
        }
    }
    
    dfs(start);
    return visited;
}
```

#### BFS for Graphs

```typescript
function bfsGraph(graph: Map<number, number[]>, start: number): number[] {
    const visited = new Set<number>();
    const result: number[] = [];
    const queue = [start];
    visited.add(start);
    
    while (queue.length) {
        const node = queue.shift()!;
        result.push(node);
        
        for (const neighbor of graph.get(node) || []) {
            if (!visited.has(neighbor)) {
                visited.add(neighbor);
                queue.push(neighbor);
            }
        }
    }
    return result;
}
```

### 6. Useful Utility Functions

#### Number Operations

```typescript
// GCD (Greatest Common Divisor)
function gcd(a: number, b: number): number {
    return b === 0 ? a : gcd(b, a % b);
}

// LCM (Least Common Multiple)
function lcm(a: number, b: number): number {
    return (a * b) / gcd(a, b);
}

// Check if number is prime
function isPrime(n: number): boolean {
    if (n <= 1) return false;
    for (let i = 2; i <= Math.sqrt(n); i++) {
        if (n % i === 0) return false;
    }
    return true;
}
```

#### String Operations

```typescript
// Check if string is palindrome
function isPalindrome(s: string): boolean {
    return s === s.split('').reverse().join('');
}

// Count character frequency
function charFrequency(s: string): Map<string, number> {
    return s.split('').reduce((map, char) => {
        map.set(char, (map.get(char) || 0) + 1);
        return map;
    }, new Map<string, number>());
}
```

#### Array Operations

```typescript
// Custom sorting
const customSort = arr.sort((a, b) => {
    // Return negative if a should come before b
    // Return positive if b should come before a
    // Return 0 if order doesn't matter
    return a - b;
});

// Find all permutations
function permutations<T>(arr: T[]): T[][] {
    if (arr.length <= 1) return [arr];
    const result: T[][] = [];
    
    for (let i = 0; i < arr.length; i++) {
        const current = arr[i];
        const remaining = [...arr.slice(0, i), ...arr.slice(i + 1)];
        const perms = permutations(remaining);
        
        for (const perm of perms) {
            result.push([current, ...perm]);
        }
    }
    return result;
}
### 7. HashMap Problem-Solving Pattern

#### Basic HashMap Usage

```typescript
// Two Sum using HashMap
function twoSum(nums: number[], target: number): number[] {
    const map = new Map<number, number>();
    
    for (let i = 0; i < nums.length; i++) {
        const complement = target - nums[i];
        if (map.has(complement)) {
            return [map.get(complement)!, i];
        }
        map.set(nums[i], i);
    }
    return [];
}

// Group Anagrams
function groupAnagrams(strs: string[]): string[][] {
    const map = new Map<string, string[]>();
    
    for (const str of strs) {
        const key = str.split('').sort().join('');
        if (!map.has(key)) map.set(key, []);
        map.get(key)!.push(str);
    }
    
    return Array.from(map.values());
}

// First Non-Repeating Character
function firstUniqChar(s: string): number {
    const freq = new Map<string, number>();
    
    // Count frequencies
    for (const char of s) {
        freq.set(char, (freq.get(char) || 0) + 1);
    }
    
    // Find first unique
    for (let i = 0; i < s.length; i++) {
        if (freq.get(s[i]) === 1) return i;
    }
    return -1;
}
```

#### Advanced HashMap Techniques

```typescript
// Using composite keys
function pairsBySum(nums: number[]): Map<string, [number, number][]> {
    const pairMap = new Map<string, [number, number][]>();
    
    for (let i = 0; i < nums.length; i++) {
        for (let j = i + 1; j < nums.length; j++) {
            const sum = nums[i] + nums[j];
            const key = `sum:${sum}`;
            if (!pairMap.has(key)) pairMap.set(key, []);
            pairMap.get(key)!.push([nums[i], nums[j]]);
        }
    }
    return pairMap;
}

// Using HashMap for caching/memoization
function memoizedFunction<T, R>(fn: (arg: T) => R): (arg: T) => R {
    const cache = new Map<string, R>();
    
    return (arg: T): R => {
        const key = JSON.stringify(arg);
        if (!cache.has(key)) {
            cache.set(key, fn(arg));
        }
        return cache.get(key)!;
    };
}
```

### 8. QuickSort Pattern

#### Basic QuickSort Implementation

```typescript
function quickSort(arr: number[]): number[] {
    if (arr.length <= 1) return arr;
    
    const pivot = arr[Math.floor(arr.length / 2)];
    const left: number[] = [];
    const middle: number[] = [];
    const right: number[] = [];
    
    for (const num of arr) {
        if (num < pivot) left.push(num);
        else if (num > pivot) right.push(num);
        else middle.push(num);
    }
    
    return [...quickSort(left), ...middle, ...quickSort(right)];
}

// In-place QuickSort
function quickSortInPlace(arr: number[], low: number = 0, high: number = arr.length - 1): void {
    if (low < high) {
        const pivotIndex = partition(arr, low, high);
        quickSortInPlace(arr, low, pivotIndex - 1);
        quickSortInPlace(arr, pivotIndex + 1, high);
    }
}

function partition(arr: number[], low: number, high: number): number {
    const pivot = arr[high];
    let i = low - 1;
    
    for (let j = low; j < high; j++) {
        if (arr[j] <= pivot) {
            i++;
            [arr[i], arr[j]] = [arr[j], arr[i]];
        }
    }
    
    [arr[i + 1], arr[high]] = [arr[high], arr[i + 1]];
    return i + 1;
}
```

#### QuickSelect Pattern (Finding Kth Element)

```typescript
function quickSelect(arr: number[], k: number): number {
    function select(left: number, right: number, k: number): number {
        if (left === right) return arr[left];
        
        const pivotIndex = partition(arr, left, right);
        
        if (k === pivotIndex) return arr[k];
        if (k < pivotIndex) return select(left, pivotIndex - 1, k);
        return select(pivotIndex + 1, right, k);
    }
    
    return select(0, arr.length - 1, k - 1);
}
```

### 9. Pass-by-Value vs Pass-by-Reference Pattern

#### Understanding the Difference

```typescript
// Pass by Value (Primitives)
function modifyPrimitive(x: number): number {
    x = x + 1;
    return x;
}

let num = 5;
console.log(modifyPrimitive(num)); // 6
console.log(num); // Still 5

// Pass by Reference (Objects, Arrays)
function modifyObject(obj: {value: number}): void {
    obj.value = obj.value + 1;
}

let myObj = {value: 5};
modifyObject(myObj);
console.log(myObj.value); // 6
```

#### Common Patterns for Handling References

```typescript
// Cloning Objects
function safeObjectModification<T extends object>(obj: T): T {
    // Shallow clone
    const shallowCopy = {...obj};
    
    // Deep clone
    const deepCopy = JSON.parse(JSON.stringify(obj));
    
    return deepCopy;
}

// Immutable Array Operations
function immutableArrayOperations(arr: number[]): number[] {
    // Instead of arr.push(1)
    const addedElement = [...arr, 1];
    
    // Instead of arr.pop()
    const removedLast = arr.slice(0, -1);
    
    // Instead of arr.unshift(1)
    const addedFirst = [1, ...arr];
    
    // Instead of arr.shift()
    const removedFirst = arr.slice(1);
    
    return addedElement;
}

// Handling Nested Objects
function handleNestedObjects(obj: any): any {
    if (obj === null || typeof obj !== 'object') {
        return obj;
    }
    
    if (Array.isArray(obj)) {
        return obj.map(item => handleNestedObjects(item));
    }
    
    const newObj: any = {};
    for (const key in obj) {
        newObj[key] = handleNestedObjects(obj[key]);
    }
    return newObj;
}
```

#### Practical Applications

```typescript
// Tree Node Cloning
class TreeNode {
    val: number;
    left: TreeNode | null;
    right: TreeNode | null;
    
    constructor(val: number) {
        this.val = val;
        this.left = null;
        this.right = null;
    }
}

function cloneTree(root: TreeNode | null): TreeNode | null {
    if (!root) return null;
    
    const newNode = new TreeNode(root.val);
    newNode.left = cloneTree(root.left);
    newNode.right = cloneTree(root.right);
    
    return newNode;
}

// Graph Clone with HashMap
function cloneGraph(node: Node | null): Node | null {
    if (!node) return null;
    
    const visited = new Map<Node, Node>();
    
    function dfs(node: Node): Node {
        if (visited.has(node)) return visited.get(node)!;
        
        const clone = new Node(node.val);
        visited.set(node, clone);
        
        for (const neighbor of node.neighbors) {
            clone.neighbors.push(dfs(neighbor));
        }
        
        return clone;
    }
    
    return dfs(node);
}
```
