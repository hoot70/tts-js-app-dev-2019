# ES6 Lesson

## Interpolation

Don't need to use line breaks in ES6 when using back ticks
```javascript
console.log(`Hello! I'm a string
continues on this line`);
```

Old way of doing line breaks
```javascript
console.log('string text 1\n' + 'string text 2')
```

This is the old way of concatination
```javascript
console.log('Hello ' + name +' I hope you have a great ' + day);
```
This is the new way in ES6 to do interpolation

```javascript
console.log(`Hello ${name} I hope you have a great ${day}`);
```
Example of interpolation inside of an object
```javascript
const name = 'Jimmy'
const day = 'Wednesday'
const instructor = {
    name: 'Chris',
    lesson: 'ES6',
    greet: function(){
        return `Hello ${this.name} I hope your lesson on ${this.lesson} goes well on ${day}`
    }
}
```
## Let and Const

This would be undefined because you are allowing let to be reassigned

```javascript
function foo() {
    let x = true;
    if (x) {
        let usingVar = 'im using let';
    }
    console.log(usingVar);
}

foo() //this would be undefined
```
Once you assign const it cannot be reassigned
```javascript
const instructors = ['Jim', 'Chris']
instructors = ['Jimm', 'Christ']
```
If you tried to do this you would get an error because it would say that instructors is already assigned

You can modify an array if it is a const
```javascript
instructors.push('Jack', 'Jill');
```
Would add Jack and Kill to the end of the array

## Default Parameters
Default parameters allow you to pass default items into your function.

This would be the old way of doing this
```javascript
function hello(name){
    name = name || 'Mystery Person'
    console.log('Hello ' + name + '!');
}

hello('Bobby'); //returns 'Hello Bobby!'
hello();//returns 'Hello Mystery Person!'
```
This would be the way to do this in ES6
```javascript
function hello(name = 'Mystery Person'){
    console.log(`Hello ${name}!`);
}

hello('Bobby'); //returns 'Hello Bobby!'
hello();//returns 'Hello Mystery Person!'
```
## Arrow Functions

Arrow functions allow you to streamline the way you write functions.

This is the old way of doing it
```javascript
const teacher = {
    name: 'Jim',
    speak: function(){
        //bind a funciton to a specific context
        let boundFunction = function(){
        console.log('later my name is ' + this.name)
    }.bind(this);//add this to make sure that it binds to the object
    //bound function will always run in a bound context
    setTimeout(boundFunction, 1000);
    }
}

teacher.speak();
```
This is the way to write this function with arrow functions
```javascript
const teacher = {
    name: 'Jim',
    speak: function(){
        let boundFunction = () => {
        console.log('later my name is ' + this.name)
    };
    setTimeout(boundFunction, 1000);
    }
}
//arrow functions have lexical binding. They are bound to the scope of where they are defined and not where they are used
teacher.speak();
```
Arrow functions do not need a return if the function is all on the same line
```javascript
let students = [
    {name: 'Hugo'},
    {name: 'Candace'},
    {name: 'Taylor'},
    {name: 'Dimitri'}
];

let names = students.map((pizza) => pizza.name);

console.log(names);
```
This would return the same thing as
```javascript
let students = [
    {name: 'Hugo'},
    {name: 'Candace'},
    {name: 'Taylor'},
    {name: 'Dimitri'}
];

let names = students.map((pizza) => {
    return pizza.name
});

console.log(names);
```

## Rest Operators
Rest operator allows you to put the parameters to take any number of objects and pass them into an array

Old way of doing this
```javascript
console.log(names);

function add(){
    console.log('arguments object', arguments);

    var numbers = Array.prototype.slice.call(arguments);

    var sum = 0;

    numbers.forEach(function (number){
        sum += number;
     
    });
    return sum;
}

console.log(add(1,2,3,4,5,6,7,8));
```
This is doing it with Rest operators
```javascript
let add = (...numbers) => {
    console.log('rest parameters', numbers);

    let sum = 0;
       numbers.forEach(function (number){
        sum += number;
       });
       return sum 
}

console.log(add(1,2,3,4,5,6,7,8));
```
This is doing this with Rest operators all on the same line
```javascript
let add = (...numbers) => numbers.reduce((sum, number) => sum += number, 0);

console.log(add(1,2,3,4,5,6,7,8));
```
This is combining Rest parameters with multiple arguements
```javascript
function addStuff(x, y, ...z){
    return (x+y) * z.length;
}

console.log(addStuff(1, 2, "hello", 'world', true, 99));
```
This is an example using the spread operator
```javascript
let random = ['Hello', 'World', true, 99]
let newArray = [1, 2, ...random, 3]

console.log(newArray);
// returns [ 1, 2, 'Hello', 'World', true, 99, 3 ]
```
Another Example
```javascript
let spreadEx = (item) => {
    let spreadArray = [...item]
    console.log(spreadArray);
    return spreadArray;
}

spreadEx('Hello World');
// returns [ 'H', 'e', 'l', 'l', 'o', ' ', 'W', 'o', 'r', 'l', 'd' ]
```
A different example
```javascript
let restEx = (...z) => {
    console.log(z)
    return z
}

restEx('hello', 'world');
// returns [ 'hello', 'world' ]
```
Below is not a not very DRY way of pulling items out of an array
```javascript
var students = ['Julian', 'AJ', 'Matt']
var x = students[0];
var y = students[1];
var z = students[2];

console.log(x, y, z);
```
This is how you destructure an array using ES6
```javascript
let students = ['Julian', 'AJ', 'Matt'];
let[x, y, z] = students;

console.log(x, y, z);//returns Julian AJ Matt
console.log(y, z);//returns AJ Matt
```
This is a way of doing it through a function
```javascript
let completedHomework = () => {
    return ['Julian', 'AJ', 'Matt'];
}

let [x,y,z] = completedHomework();

console.log(x,y,z);
```
This also works with objects
```javascript
let instructor = {
    name: 'Jimmy',
    email: 'no@no.com'
}

let { name: x, email: y} = instructor;

console.log(x)//returns 'Jimmy'
```
Here is an example with default parameters
```javascript
let person = {
    name: 'Bert',
}

function something({name, email = 'no@no.com'}){
    console.log(name, email);
};

something(person);
```

## Constructor Functions
These will allow you to set things in your app to allow you to call them multiple times throughout your page
```javascript
//Constructors are capitalized
function Person(name, job){
    this.name = name;
    this.job = job;

}

Person.prototype.getName = function getName(){
    return this.name;
}

var goodGuy = new Person ('Aang', 'Airbender');

console.log(goodGuy.getName());//returns 'Aang'
```
This is a more ES6 version of doing this
```javascript
class Person {
    constructor (name, job) {
        this.name = name;
        this.job = job;
    }
    getName(){
        return this.name;
    }
    getJob(){
        return this.job;
    }
}

let goodGuy = new Person('Neo', 'the One');

console.log(goodGuy.getName());//returns 'Neo'
```
This is an example that allows you to update contents
```javascript
class Person {
    constructor (name) {
        this.name = name;
    }
    set name (name) {
        this._name = name;
    }
    get name() {
        return this._name
    }
}

let goodGuy = new Person('Jim Gordon');
console.log(goodGuy.name);
//returns Jim Gordon
goodGuy.name = 'James Gordon';
console.log(goodGuy.name);
//returns James Gordon
```
This allows you to map through and add to the object
```javascript
let student = {name: 'Aaron'};
let status = new Map();

status.set(student.name, 'Denise');
status.set('feeling', 'churlish')
console.log(status.get(student.name));
console.log(status.get('feeling'));
```
## Encapsulation
This is an example of encapsulation
```javascript
const Guy = (function(){
    const _name = new WeakMap();

class Guy {
    constructor(name) {
        this[_name] = name;
    }
    set name(name) {
        this[_name] = name;
    }
    get name() {
        return this[_name];
    }
}

return Guy;
}());

let guy = new Guy('Fieri');
console.log(guy.name);
```







