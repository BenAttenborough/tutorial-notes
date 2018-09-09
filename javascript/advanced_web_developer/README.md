# Advanced Web Developer
[Advanced Web Developer](https://www.udemy.com/the-advanced-web-developer-bootcamp/)

## Arrays

<details>
<summary>array.forEach()</summary>

The forEach() method executes a provided function once for each array element.
Basic usage:

```js
  /*
 Write a function called doubleValues which accepts an array and returns a new array with all the values in the array passed to the function doubled

 Examples:
 doubleValues([1,2,3]) // [2,4,6]
 doubleValues([5,1,2,3,10]) // [10,2,4,9,20]

 */
function doubleValues(arr){
    var newArr = [];
    arr.forEach(function(val) {
        newArr.push(val * 2);
    });
    return newArr;
}

// Alternatively using ES2015

let double = arr => {
    var newArr = [];
    arr.forEach( val => newArr.push(val * 2) );
    return newArr;
};

/*
 Write a function called onlyEvenValues which accepts an array and returns a new array with only the even values in the array passed to the function

 Examples:
 onlyEvenValues([1,2,3]) // [2]
 onlyEvenValues([5,1,2,3,10]) // [2,10]

 */
function onlyEvenValues(arr){
    var newArr = [];
    arr.forEach(function(val){
        if(val % 2 === 0){
            newArr.push(val)
        }
    })
    return newArr;
}

/*
 Write a function called showFirstAndLast which accepts an array of strings and returns a new array with only the first and last character of each string.

 Examples:
 showFirstAndLast(['colt','matt', 'tim', 'udemy']) // ["ct", "mt", "tm", "uy"]
 showFirstAndLast(['hi', 'goodbye', 'smile']) // ['hi', 'ge', 'se']

 */
function showFirstAndLast(arr){
    var newArr = [];
    arr.forEach(function(val){
        newArr.push(val[0] + val[val.length-1])
    });
    return newArr;
}

/*
 Write a function called addKeyAndValue which accepts an array, a key, and a value and returns a the array passed to the function with the new key and value added for each variable

 Examples:
 addKeyAndValue([{name: 'Elie'}, {name: 'Tim'}, {name: 'Matt'}, {name: 'Colt'}], 'title', 'instructor')

 // [{name: 'Elie', title:'instructor'}, {name: 'Tim', title:'instructor'}, {name: 'Matt', title:'instructor'}, {name: 'Colt', title:'instructor'}]

 */
function addKeyAndValue(arr,key,value){
    arr.forEach(function(val){
        val[key] = value;
    });
    return arr;
}

/*
 Write a function called vowelCount which accepts a string and returns an object with the keys as the vowel and the values as the number of times the vowel appears in the string. This function should be case insensitive so a lowercase letter and uppercase letter should count

 Examples:
 vowelCount('Elie') // {e:2,i:1};
 vowelCount('Tim') // {i:1};
 vowelCount('Matt') // {a:1})
 vowelCount('hmmm') // {};
 vowelCount('I Am awesome and so are you') // {i: 1, a: 4, e: 3, o: 3, u: 1};
 */
function vowelCount(str){
    var splitArr = str.toLowerCase().split("");
    var obj = {};
    var vowels = "aeiou";

    splitArr.forEach(function(letter){
        if(vowels.indexOf(letter) !== -1){
            if(obj[letter]){
                obj[letter]++;
            } else{
                obj[letter] = 1;
            }
        }
    });
    return obj;
}
```
</details>

<details>
<summary>array.map()</summary>

The map() method creates a new array with the results of calling a provided function on every element in the calling array. See MDN

Basic usage:

```js
function doubleValues(arr) {
    return arr.map(function (val) {
        return val * 2
    });
}

//ES2015
let doubleValuesES2015 = arr => arr.map(val => val * 2);

function valTimesIndex(arr) {
    return arr.map(function (val, idx) {
        return val * idx;
    })
}

function extractValue(arr, key) {
    return arr.map(function (val) {
        return val[key];
    });
}

function extractFullName(arr) {
    return arr.map(function (val) {
        return val.first + " " + val.last;
    });
}
```
</details>

<details>
<summary>array.filter()</summary>
The filter() method creates a new array with all elements that pass the test implemented by the provided function. See MDN

Basic usage:
```js
/*
 Write a function called filterByValue which accepts an array of objects and a key and returns a new array with all the objects that contain that key.

 Examples:
 filterByValue([{first: 'Elie', last:"Schoppik"}, {first: 'Tim', last:"Garcia", isCatOwner: true}, {first: 'Matt', last:"Lane"}, {first: 'Colt', last:"Steele", isCatOwner: true}], 'isCatOwner') // [{first: 'Tim', last:"Garcia", isCatOwner: true}, {first: 'Colt', last:"Steele", isCatOwner: true}]
 */

function filterByValue(arr, key){
    return arr.filter(function(val){
        return val[key];
    });
}

/*
 Write a function called find which accepts an array and a value and returns the first element in the array that has the same value as the second parameter or undefined if the value is not found in the array.

 Examples:
 find([1,2,3,4,5], 3) // 3
 find([1,2,3,4,5], 10) // undefined
 */

function find(arr, searchValue){
    var value = "";
    arr.forEach(function(val) {
        if (val === searchValue)
            value = val;
    });
    return value || undefined;
}

/*
 Write a function called findInObj which accepts an array of objects, a key, and some value to search for and returns the first found value in the arrayt.

 Examples:
 findInObj([{first: 'Elie', last:"Schoppik"}, {first: 'Tim', last:"Garcia", isCatOwner: true}, {first: 'Matt', last:"Lane"}, {first: 'Colt', last:"Steele", isCatOwner: true}], 'isCatOwner',true) // {first: 'Tim', last:"Garcia", isCatOwner: true}
 */

function findInObj(arr, key, searchValue){
    for (var i = 0; i < arr.length; i++) {
        if (arr[i][key] === searchValue)
            return arr[i];
    }
    return undefined;
}

/*
 Write a function called removeVowels which accepts a string and returns a new string with all of the vowels (both uppercased and lowercased) removed. Every character in the new string should be lowercased.

 Examples:
 removeVowels('Elie') // ('l')
 removeVowels('TIM') // ('tm')
 removeVowels('ZZZZZZ') // ('zzzzzz')
 */

function removeVowels(str){
    str = str.toLowerCase();
    var strArray = str.split('');
    var vowels = 'aeiou';
    var newStr = '';
    return strArray.filter(function(val) {
        return vowels.indexOf( val ) === -1;
    }).join('');
}

/*
 Write a function called doubleOddNumbers which accepts an array and returns a new array with all of the odd numbers doubled (HINT - you can use map and fitler to double and then filter the odd numbers).

 Examples:
 doubleOddNumbers([1,2,3,4,5]) // [2,6,10]
 doubleOddNumbers([4,4,4,4,4]) // []
 */

function doubleOddNumbers(arr){
    return arr.filter(function(val) {
        return val % 2 !== 0;
    }).map(function(val){
        return val * 2;
    });
}
```
</details>

<details>
<summary>array.some()</summary>

The some() method tests whether at least one element in the array passes the test implemented by the provided function. See MDN

* Iterates through an array
* Runs a callback on each value in the array
* If the callbak returns true for at least one single value, return true
* Otherwise, return false
* The result will be a boolean

Basic usage:

```js
// How does some work?

function some(array, callback) {
    for (var i = 0; i < array.length; i++) {
        if (callback(array[i], i, array)) {
            return true;
        }
    }
    return false;
}

// Example callback for our hand built function above

function isEvenNumber(num) {
    return num % 2 === 0;
}

some([1, 2, 3], isEvenNumber); // True
some([1, 3, 5], isEvenNumber); // False

// Using built in array.some instead:

function hasEvenNumber(arr) {
    return arr.some(function (value) {
        return value % 2 === 0;
    });
}

hasEvenNumber([1,2,3,4]); // true
hasEvenNumber([1,3,5]); // false

// Example 2:

function hasComma(str) {
    return str.split('').some(function(value) {
        return value === ',';
    })
}

hasComma('This is wonderful'); // false
hasComma('This, is wonderful'); // true
```
</details>

<details>
<summary>array.every()</summary>

The every() method tests whether all elements in the array pass the test implemented by the provided function. See MDN

Basically an inverse of some - every element must pass a test

* Iterates through an array
* Runs a callback on each value in the array
* If the callbak returns false for at least one single value, return false
* Otherwise, return true
* The result will be a boolean
</details>

<details>
<summary>array.reduce()</summary>

The reduce() method applies a function against an accumulator and each element in the array (from left to right) to reduce it to a single value. See MDN

Basic usage:
```js
/*
 Write a function called extractValue which accepts an array of objects and a key and returns a new array with the value of each object at the key.

 Examples:
 var arr = [{name: 'Elie'}, {name: 'Tim'}, {name: 'Matt'}, {name: 'Colt'}]
 extractValue(arr,'name') // ['Elie', 'Tim', 'Matt', 'Colt']
 */

function extractValue(arr, key){
    var newArray = [];
    return arr.reduce(function(accumulator, nextValue){
        accumulator.push(nextValue[key]);
        return accumulator;
    },newArray);
}


/*
 Write a function called vowelCount which accepts a string and returns an object with the keys as the vowel and the values as the number of times the vowel appears in the string. This function should be case insensitive so a lowercase letter and uppercase letter should count

 Examples:
 vowelCount('Elie') // {e:2,i:1};
 vowelCount('Tim') // {i:1};
 vowelCount('Matt') // {a:1})
 vowelCount('hmmm') // {};
 vowelCount('I Am awesome and so are you') // {i: 1, a: 4, e: 3, o: 3, u: 1};
 */

function vowelCount(str){
    var vowels = 'aeiou';
    return str.toLowerCase().split('').reduce(function(accumulator, nextValue, i, array) {
        if(vowels.indexOf(nextValue) !== -1) {
            if (nextValue in accumulator) {
                accumulator[nextValue]++;
            } else {
                accumulator[nextValue] = 1;
            }
        }
        return accumulator;
    },{});
}

/*
 Write a function called addKeyAndValue which accepts an array of objects and returns the array of objects passed to it with each object now including the key and value passed to the function.

 Examples:
 var arr = [{name: 'Elie'}, {name: 'Tim'}, {name: 'Matt'}, {name: 'Colt'}];

 addKeyAndValue(arr, 'title', 'Instructor') //
 [
 {title: 'Instructor', name: 'Elie'},
 {title: 'Instructor', name: 'Tim'},
 {title: 'Instructor', name: 'Matt'},
 {title: 'Instructor', name: 'Colt'}
 ]
 */

function addKeyAndValue(arr, key, value){
    var obj = {};
    return arr.reduce(function(accumulator, nextValue) {
        // Take next value and add key value pair to it
        //accumulator.push(nextValue);
        //accumulator.push(nextValue[key] = value);
        obj = nextValue;
        obj[key] = value;
        accumulator.push(obj);
        return accumulator;
    }, []);
}


/*
 Write a function called partition which accepts an array and a callback and returns an array with two arrays inside of it. The partition function should run the callback function on each value in the array and if the result of the callback function at that specific value is true, the value should be placed in the first subarray. If the result of the callback function at that specific value is false, the value should be placed in the second subarray.

 Examples:

 function isEven(val){
 return val % 2 === 0;
 }

 var arr = [1,2,3,4,5,6,7,8];

 partition(arr, isEven) // [[2,4,6,8], [1,3,5,7]];

 function isLongerThanThreeCharacters(val){
 return val.length > 3;
 }

 var names = ['Elie', 'Colt', 'Tim', 'Matt'];

 partition(names, isLongerThanThreeCharacters) // [['Elie', 'Colt', 'Matt'], ['Tim']]
 */

function partition(arr, callback){
    return arr.reduce(function(accumulator, nextValue) {
        if (callback(nextValue))
            accumulator[0].push(nextValue);
        else
            accumulator[1].push(nextValue);
        return accumulator;
    },[[],[]]);
}
```
</details>

## Closures

<details>
<summary>
Basics
</summary>
A closure is the combination of a function and the lexical environment within which that function was declared. See MDN

Basic usage:

```js
// Basic closure
// Inner functions can see outer function variables

function outer() {
    var start = "Closures are";
    return function inner() {
        return start + " " + "awesome"
    }
}

outer(); // returns inner function definition
outer()(); // returns "Closures are awesome"

function outer(a){
    return function inner(b) {
        // the inner function is making use of the variable "a"
        // which was defined in an outer function called "outer"
        // and by the time inner is called, that outer function has returned
        // this function called "inner" is a closure
        return a+b;
    }
}

outer(5)(5); // 10
var storeOuter = outer(5);
storeOuter(10); //15

/*
 Write a function called specialMultiply which accepts two parameters. If the function is passed both parameters, it should return the product of the two. If the function is only passed one parameter - it should return a function which can later be passed another parameter to return the product. You will have to use closure and arguments to solve this.

 Examples:

 specialMultiply(3,4); // 12
 specialMultiply(3)(4); // 12
 specialMultiply(3); // function(){}....
 */

function specialMultiply(a,b){
    if (arguments.length === 2)
        return a*b;
    if(arguments.length === 1){
        return function(b){
            return a*b;
        }
    }
    return false;
}

/*
 Write a function called guessingGame which takes in one parameter amount. The function should return another function that takes in a parameter called guess. In the outer function, you should create a variable called answer which is the result of a random number between 0 and 10 as well as a variable called guesses which should be set to 0.

 In the inner function, if the guess passed in is the same as the random number (defined in the outer function) - you should return the string "You got it!". If the guess is too high return "Your guess is too high!" and if it is too low, return "Your guess is too low!". You should stop the user from guessing if the amount of guesses they have made is greater than the initial amount passed to the outer function.

 You will have to make use of closure to solve this problem.

 Examples (yours might not be like this, since the answer is random every time):

 var game = guessingGame(5)
 game(1) // "You're too low!"
 game(8) // "You're too high!"
 game(5) // "You're too low!"
 game(7) // "You got it!"
 game(1) // "You are all done playing!"

 var game2 = guessingGame(3)
 game2(5) // "You're too low!"
 game2(3) // "You're too low!"
 game2(1) // "No more guesses the answer was 0"
 game2(1) // "You are all done playing!"
 */

function guessingGame(amount){
    var answer = Math.floor(Math.random() * 11),
        guesses = 0;
    return function guess(guess) {
        guesses++;
        if (guesses > amount)
            return "You are all done playing!";
        if (guess === answer)
            return "You got it!";
        if (guess > answer)
            return "Your guess is too high!";
        return "Your guess is too low!"
    }
}
```
</details>

<details>
<summary>
Private variables
</summary>

```js
// Private variables

function counter(){
    var count = 0;
    return function inner(){
        count++;
        return count;
    }
}

var counter1 = counter();

counter1; // function definition

counter1(); // 1

counter1(); // 2

var counter2 = counter();

counter2(); // 1

// Demonstrates private variable;

count; // Reference error

// More privacy

function classRoom(){
    var instructors = ["Elie", "Colt"]
    return {
        getInstructors: function(){
            return instructors;
        },
        addInstructor: function(instructor){
            instructors.push(instructor);
            return instructors;
        }
    }
}

var first = classRoom();

first.getInstructors(); // ["Elie", "Colt"]

first.addInstructor("Matt"); // ["Elie", "Colt", "Matt"]

var second = classRoom();

second.addInstructor("Bob"); // ["Elie", "Colt", "Bob"]

first.getInstructors(); // ["Elie", "Colt", "Matt"]

// Gotcha - can use pop to remove instructors from private variable!


first.getInstructors().pop(); // "Matt"

// Correct implementation

function classRoom(){
    var instructors = ["Elie", "Colt"]
    return {
        getInstructors: function(){
            return instructors.slice();
        },
        addInstructor: function(instructor){
            instructors.push(instructor);
            return instructors.slice();
        }
    }
}

var course1 = classRoom();
course1.getInstructors().pop(); // ["Colt"]
course1.getInstructors().pop(); // ["Colt"]
course1.getInstructors(); // ["Colt", "Elie"]

// now the instructors variable is truly private!
```
</details>

## Call, apply and bind

<details>
<summary>
.call()
</summary>
The call() method calls a function with a given this value and arguments provided individually.

Basic usage:

```js
/*
 Write a function called arrayFrom which converts an array-like-object into an array.

 Examples:
 var divs = document.getElementsByTagName('divs');
 divs.reduce // undefined
 var converted = arrayFrom(divs);
 converted.reduce // function(){}....
 */

function arrayFrom(arrayLikeObject){
    return [].slice.call(arrayLikeObject)
}

/*
 // Write a function called sumEvenArguments which takes all of the arguments
 passed to a function and returns the sum of the even ones.

 Examples:
 sumEvenArguments(1,2,3,4) // 6
 sumEvenArguments(1,2,6) // 8
 sumEvenArguments(1,2) // 2
 */

function sumEvenArguments(){
    var args = [].slice.call(arguments);
    return args.reduce(function(acc, nextVal) {
        if (nextVal % 2 === 0) {
            acc += nextVal;
        }
        return acc;
    },0)
}
```
</details>

<details>
<summary>
.apply()
</summary>
The apply() method calls a function with a given this value, and arguments provided as an array (or an array-like object). See MDN

Basic usage:

```js
/*
 Write a function called invokeMax which accepts a function and a maximum amount. invokeMax should return a function that when called increments a counter. If the counter is greater than the maximum amount, the inner function should return "Maxed Out"

 Examples:

 function add(a,b){
 return a+b
 }

 var addOnlyThreeTimes = invokeMax(add,3);
 addOnlyThreeTimes(1,2) // 3
 addOnlyThreeTimes(2,2) // 4
 addOnlyThreeTimes(1,2) // 3
 addOnlyThreeTimes(1,2) // "Maxed Out!"

 */

function invokeMax(fn, num){
    var max = 0;
    return function(){
        if(max >= num) return "Maxed Out!";
        max++;
        return fn.apply(this,arguments);
    }
}

/*
 Write a function called once which accepts two parameters, a function and a value for the keyword 'this'. Once should return a new function that can only be invoked once, with the value of the keyword this in the function set to be the second parameter.

 Examples:

 function add(a,b){
 return a+b
 }

 var addOnce = once(add, this);
 addOnce(2,2) // 4
 addOnce(2,2) // undefined
 addOnce(2,2) // undefined

 function doMath(a,b,c){
 return this.firstName + " adds " + (a+b+c)
 }

 var instructor = {firstName: "Elie"}
 var doMathOnce = once(doMath, instructor);
 doMathOnce(1,2,3) // "Elie adds 6"
 doMathOnce(1,2,3) // undefined


 */

function once(fn, thisArg){
    var hasBeenCalled = false;
    return function(){
        if(!hasBeenCalled){
            hasBeenCalled = true;
            return fn.apply(thisArg, arguments)
        }
    }
}
```
</details>

<details>
<summary>
.bind()
</summary>
The filter() method creates a new array with all elements that pass the test implemented by the provided function. See MDN

Basic usage:
</details>

<details>
<summary>
.reduce()
</summary>
The reduce() method applies a function against an accumulator and each element in the array (from left to right) to reduce it to a single value. See MDN

Basic usage:
</details>

## ES2015

<details>
<summary>
const
</summary>
Constants are block-scoped, much like variables defined using the let statement. The value of a constant cannot change through re-assignment, and it can't be redeclared. See MDN

Basic usage:

```js
var firstInstructor = "Colt";

firstInstructor = "Elie";

const anotherInstructor = "Tim";

anotherInstructor = "Elie"; // TypeError

const anotherInstructor = "Bob"; // SyntaxError

// We can NEVER redeclare a const
// However if const is an object or array their values can change
// This is because const only makes the binding imutable, not the values.
// Primitives are the same as their bindings so cannot change
// But object and array VALUES can be changed

const numbers = [1,2,3,4];
numbers.push(10);
numbers; // (5) [1,2,3,4,10]
numbers = "No!"; // TypeError
```
</details>

<details>
<summary>
let
</summary>
The let statement declares a block scope local variable, optionally initializing it to a value. See MDN

Basic usage:

```js
// Let creates block scope

var instructor = "Elie";

if (instructor === "Elie") {
    let funFact = "Plays Cello!";
}

funFact; // Reference error

// Hoisting with let

function helloInstructor() {
    return elie;
    var elie = "ME!";
}
helloInstructor(); // undefined - notice that the variable is created, but not assigned a value

// Variable is hoisted to the top of the function

// So the above becomes:

function helloInstructor() {
    var elie;
    return elie;
    elie = "ME!";
}

// Everything below the return statement is unreachable.

// Let has hoisting as well but we cannot access the value
// It occupies a Temporal Dead Zone (TDZ)

function helloSecondInstructor() {
    return colt;
    let colt = "Him!";
}
helloSecondInstructor(); // ReferenceError

// Use cases for let

for (var i = 0; i < 5; i++) {
    setTimeout(function () {
        console.log(i);
    }, 1000)
}

// 5 (five times)
// Because by the time the setTimeout completes the for loop has completed and i = the last value (5)

// Pre ES2015 solution:

for (var i = 0; i < 5; i++) {
    (function (j) {
        setTimeout(function () {
            console.log(j);
        }, 1000);
    })(i)
}

// ES2015

for (let i = 0; i < 5; i++) {
    setTimeout(function () {
        console.log(i);
    }, 1000)
}
```
</details>

<details>
<summary>
Template strings
</summary>
Template literals are string literals allowing embedded expressions. You can use multi-line strings and string interpolation features with them. They were called "template strings" in prior editions of the ES2015 specification. MDN

Basic usage:

```js
//ES5

var firstName = "Elie";

var lastName = "Schoppik";

console.log("Hello" + firstName + " " + lastName); // error prone!

//ES2015

console.log(`Hello ${firstName} ${lastName}`);

//Multiline strings

`
Hello
How
Nice
This
Is!
`
```
</details>

<details>
<summary>
Arrow functions
</summary>
An arrow function expression has a shorter syntax than a function expression and does not have its own this, arguments, super, or new.target. These function expressions are best suited for non-method functions, and they cannot be used as constructors. See MDN

* Arrow functions are not exatly the same as regular functions!
* Arrow functions do not get their own 'this' keyword
Inside of an arrow function, the keyword this has its original meaning from the enclosing context
* The fact that arrow functions do not have their own this keyword can be quite helpful - you just need to understand when you might NOT want that!
* Arrow functions do not get arguments
* Arrow functions should not be used for object methods
Basic usage:

```js
// ES5
var add = function(a,b){
    return a+b;
};

// Replace the keyword 'function' with =>

let add = (a,b) => {
    return a+b;
};

// One line arrow functions
// # You can put arrow functions on one line
// # But you must omit the return keyword as well as curly braces

let add = (a,b) => {
    return a+b;
};

// Becomes

let add = (a,b) => a+b;

// Refactoring with arrow functions

// ES5
[1,2,3].map(function(value){
    return value * 2;
}) // [2,4,6]

// Becomes

[1,2,3].map(value => value * 2);

// ES5

function doubleAndFilter(arr){
    return arr.map(function(value){
        return value * 2;
    }).filter(function(value){
        return value % 3 === 0;
    })
}

doubleAndFilter([5,10,15,20]); // [30]

var doubleAndFilter = arr => arr.map(val => val * 2).filter(num => num % 3 === 0);

doubleAndFilter([5,10,15,20]); // [30]

// A familiar situation:

var instructor = {
    firstName: "Elie",
    saysHi: function(){
        setTimeout(function(){
            console.log("Hello " + this.firstName);
        }, 1000);
    }
}

instructor.saysHi(); // "Hello undefined"
// this.firstName is undefined because the 'this' context has changed to the setTimeout context, NOT the instructor object
// In ES5 we can solve this by binding the this context to the setTimeout function:

// ES15 solution:

var instructor = {
    firstName: "Elie",
    saysHi: function(){
        setTimeout(function(){
            console.log("Hello " + this.firstName);
        }.bind(this), 1000);
    }
}

instructor.saysHi(); // "Hello Elie"

// ES2015 solution

var instructor = {
    firstName: "Elie",
    saysHi: function(){
        setTimeout(() => {
            console.log("Hello " + this.firstName);
        }, 1000);
    }
}

// Because arrow functions do not have a 'this' value the this value takes its context from the outer closure - the instructor object
// But we still need to use the function keyword for the saysHi method, since that needs a this value

// Arrow functions also don't get an arguments value either.

/* 1 - Refactor the following code to use ES2015 arrow functions - make sure your function is also called tripleAndFilter

 function tripleAndFilter(arr){
 return arr.map(function(value){
 return value * 3;
 }).filter(function(value){
 return value % 5 === 0;
 })
 }

 */

let tripleAndFilter = arr => arr.map(val => val * 3).filter(val => val % 5 === 0);


/* 2 - Refactor the following code to use ES2015 arrow functions. Make sure your function is also called doubleOddNumbers

 function doubleOddNumbers(arr){
 return arr.filter(function(val){
 return val % 2 !== 0;
 }).map(function(val){
 return val *2;
 })
 }

 */

let doubleOddNumbers = arr => arr.filter(val => val % 2 !== 0).map(val => val * 2 );



/* 3 - Refactor the following code to use ES2015 arrow functions. Make sure your function is also called mapFilterAndReduce.

 function mapFilterAndReduce(arr){
 return arr.map(function(val){
 return val.firstName
 }).filter(function(val){
 return val.length < 5;
 }).reduce(function(acc,next){
 acc[next] = next.length
 return acc;
 }, {})
 }
 */

let mapFilterAndReduce = (arr) => arr.map(val => val.firstName).filter(val => val.length < 5)
    .reduce((acc,next) => {
        acc[next] = next.length
        return acc;
    }, {})

/* 4 - Write a function called createStudentObj which accepts two parameters, firstName and lastName and returns an object with the keys of firstName and lastName with the values as the parameters passed to the function.

 Example:
 createStudentObj('Elie', 'Schoppik') // {firstName: 'Elie', lastName: 'Schoppik'}
 */

let createStudentObj = (firstName, lastName) => ({firstName:firstName, lastName:lastName})


/* 5 - Given the following code:


 Refactor this code to use arrow functions to make sure that in 1000 milliseconds you console.log 'Hello Colt'

 var instructor = {
 firstName: "Colt",
 sayHi: function(){
 setTimeout(function(){
 console.log('Hello ' + this.firstName)
 },1000)
 }
 }

 */

var instructor = {
    firstName: "Colt",
    sayHi: function(){
        setTimeout(() =>{
            console.log('Hello ' + this.firstName)
        }, 1000)
    }
}
```
</details>

<details>
<summary>
Default parameters
</summary>
Default function parameters allow formal parameters to be initialized with default values if no value or undefined is passed. See MDN

```js
// ES5
function add(a, b){
    return a+b;
}

add(); // NaN because a is undefined and b is undefined

// ES5 solutions
function add(a, b){
    if(a == undefined) {
        a = 2;
    }
    if(b == undefined) {
        b = 5;
    }
    return a+b;
}

// ES2015 solution
function add(a=10, b=20){
    return a+b;
}

add(); // 30
add(20); // 40
```
</details>

<details>
<summary>
for...of
</summary>
The for...of statement creates a loop iterating over iterable objects (including the built-in String, Array, e.g. the Array-like arguments or NodeList objects, TypedArray, Map and Set, and user-defined iterables), invoking a custom iteration hook with statements to be executed for the value of each distinct property of the object. See MDN

Basic usage:

```js
var arr = [1,2,3,4,5];

for(let val of arr){
    console.log(val);
}

// 1
// 2
// 3
// 4
// 5

// Cannot be used on objects
```
</details>

<details>
<summary>
rest
</summary>
The rest parameter syntax allows us to represent an indefinite number of arguments as an array. See MDN

* The rest operator always returns an array
* Is called the rest operator "only" when it is a parameter to a function
* Is accessed without the ... in a function
* A better alternative to using the arguments array-like-object
Basic usage:

```js
function printRest(a, b, ...c) {
    console.log(a);
    console.log(b);
    console.log(c);
}

printRest(1, 2, 3, 4, 5, 6);

// 1
// 2
// [3,4,5,6]

//ES5
function sumArguments() {
    var total = 0;
    for (var i = 0; i < arguments.length; i++) {
        total += arguments[i];
    }
    return total;
}

//Fancier ES5
function sumArguments() {
    var argumentsArray = [].slice.call(arguments);
    return argumentsArray.reduce(function(acc,next){
        return acc + next;
    });
}

// ES2015
var sumArguments = (...args) => args.reduce((acc, next) => acc + next);
```
</details>

<details>
<summary>
spread
</summary>
Spread syntax allows an iterable such as an array expression or string to be expanded in places where zero or more arguments (for function calls) or elements (for array literals) are expected, or an object expression to be expanded in places where zero or more key-value pairs (for object literals) are expected. See MDN

* Used on arrays to spread each value out (as a comma seperated value)
* Useful when you have an array, but what you are working with expects comma separated values

Basic usage:

```js
// ES5
var arr1 = [1,2,3];
var arr1 = [4,5,6];
var arr1 = [7,8,9];
var combined = arr1.concat(arr2).concat(arr3);

// ES2015
var combined = [...arr1,...arr2,...arr3];

// Spread instead of apply

// ES5
var arr = [3,2,4,1,5];

Math.max(arr); // NaN

Math.max.apply(this, arr); // 5

// ES2015
Math.max(...arr);

function sumValues(a,b,c){
    return a+b+c;
}

var nums = [12,15,20];

// ES5
sumValues.apply(this, nums); // 47

// ES2015
sumValues(...nums);
```
</details>

<details>
<summary>
Object enchancements
</summary>
Basic usage:

```js
// Object Shorthand Notation

var firstName = "Elie";
var lastName = "Schoppik";

// ES5
let instructor = {
    firstName: firstName,
    lastName: lastName
}

// ES2015
var instructor = {
    firstName,
    lastName
}

// Object Methods

// ES5
var instructor = {
    sayHello: function() {
        return "Hello";
    }
}

// ES2015
var instructor = {
    sayHello(){
        return "Hello"''
    }
}

// Computed Property Names

// ES5
var firstName = "Elie";
var instructor = {};
instructor[firstName] = "That's me!";

instructor.Elie; // "That's me!"

// ES2015
var firstName = "Elie";
var instructor = {
    [firstName]: "That's me!"
};

instructor.Elie; // "That's me!"
```
</details>

<details>
<summary>
Destructuring
</summary>
The destructuring assignment syntax is a JavaScript expression that makes it possible to unpack values from arrays, or properties from objects, into distinct variables. See MDN

Extracting values from data stored in objects and arrays

```js
// ES5

var instructor = {
    firstName: "Elie",
    lastName: "Schoppik"
}

var firstName = instructor.firstName;
var lastName = instructor.lastName;

firstName; // "Elie"
lastName; // "Schoppik"

// Gets worse more elements we have

// ES2015

var instructor = {
    firstName: "Elie",
    lastName: "Schoppik"
}

var {firstName, lastName} = instructor;

firstName; // "Elie"
lastName; // "Schoppik"

// MUST use same variable names

// If you want to use different variable names:

var instructor = {
    firstName: "Elie",
    lastName: "Schoppik"
}

var {firstName:first, lastName:last} = instructor;

first; // "Elie"
last; // "Schoppik"

// ES5 Default Values with an object

function createInstructor(options) {
    var options = options || {};
    var name = options.name || {first: "Matt", last: "Lane"}
    var isFunny = options.isFunny || false;
    return [name.first, name.last, isFunny];
}

createInstructor(); // ["Matt", "Lane", false]
createInstructor({isFunny: true}); // ["Matt", "Lane", true]
createInstructor({name: {first: "Tim", last: "Garcia"}}); // ["Tim", "Garcia", false]

// Lots of work!

// ES2015 Destructuring

function createInstructor({name = {first: "Matt", last: "Lane"}, isFunny=false} = {}) {
    return [name.first, name.last, isFunny];
}

// # We're passing in a destructured object as a default parameter!
// # We assign as a default value an empty object so ES2015 knows we are destructuring
// # If nothing is passwed in, we default to the destructured object as the parameter

// Object fields as parameters ES5

function displayInfo(obj) {
    return [obj.name, obj.favColor];
}

var instructor = {
    name: "Elie",
    favColor: "Purple"
}

displayInfo(instructor); // ["Elie", "Purple"]

// Object fields as parameters ES2015

function displayInfo({name,favColor}) {
    return [name, favColor];
}

var instructor = {
    name: "Elie",
    favColor: "Purple"
}

displayInfo(instructor); // ["Elie", "Purple"]

// Arrays

var arr = [1, 2, 3];

// ES5
var a = arr[0];
var b = arr[1];
var c = arr[2];

a; //1
b; //2
c; //3

// ES2015

var [a,b,c] = arr;

a; //1
b; //2
c; //3

// ES5 vx ES2015

function returnNumbers(a, b) {
    return [a, b];
}

var first = returnNumbers(5, 10)[0];
var second = returnNumbers(5, 10)[1];

first; // 5
second; // 10

// ES2015

[first, second] = returnNumbers(5, 10);

first; // 5
second; // 10

// Swapping values

// ES5
function swap(a, b) {
    var temp = a;
    a = b;
    b = temp;
    return [a, b];
}

swap(10,5); // [5,10]

// ES2015
function swap(a,b) {
    return [a,b] = [b,a];
}

swap(10,5); // [5,10]

// Exercises

function displayStudentInfo(obj){
    var {first, last} = obj;
    return `Your full name is ${first} ${last}`
}

function printFullName({first,last}){
    return `Your full name is ${first} ${last}`
}

function createStudent({likesJavaScript = true, likesES2015 = true} = {}){
    var start = 'The student';
    if(likesJavaScript && likesES2015){
        start += ' likes JavaScript and ES2015'
    } else if(likesJavaScript){
        start += ' likes JavaScript!'
    } else if(likesES2015){
        start += ' likes ES2015!'
    } else {
        start += ' does not like much...'
    }
    return start;
}

function reverseArray(arr){
    for(var i = 0; i < arr.length/2; i++){
        [arr[i], arr[arr.length - 1 - i]] = [arr[arr.length - 1 - i], arr[i]]
    }
    return arr;
}
```
</details>

<details>
<summary>
find
</summary>
The find() method returns the value of the first element in the array that satisfies the provided testing function. Otherwise undefined is returned. See MDN

* Invoked on arrays
* Accepts a callback with value, index and array (just like forEach, map, filter, etc.)
* Returns the value found or undefined if not found

```js
/**
 * Created by ben on 20/01/2018.
 */

var instructors = [{name: "elie"}, {name: "Matt"}, {name: "Tim"}, {name: "Colt"}];

instructors.find(function(val){
    return val.name == "Tim"
}); // {name: "Tim"}

// Using arrow functions

instructors.find((val) => val.name == "Tim");

// findIndex

// Similar to find, but returns an index or -1 if the value is not found

var instructors = [{name: "elie"}, {name: "Matt"}, {name: "Tim"}, {name: "Colt"}];

instructors.findIndex(function(val){
    return val.name == "Tim"
}); // 2

instructors.findIndex(function(val){
    return val.name == "Bob"
}); // -1
```
</details>

<details>
<summary>
exercises
</summary>

```js
/*
 Write a function called copyObject, which accepts one parameter, an object. The function should return a shallow copy of the object.

 var o = {name: 'Elie'}
 var o2 = copyObject({}, o)
 o2.name = "Tim"
 o2.name // 'Tim'
 o.name // 'Elie'
 */

function copyObject(obj){
    return Object.assign({},obj);
}

/*

 Write a function called checkIfFinite which accepts one parameter and returns true if that parameter is a finite number.

 checkIfFinite(4) // true
 checkIfFinite(-3) // true
 checkIfFinite(4. // .toEqual(true
 checkIfFinite(NaN) // false
 checkIfFinite(Infinity) // false
 */

function checkIfFinite(number){
    return Number.isFinite(number);
}

/*

 Write a function called areAllNumbersFinite which accepts an array and returns true if every single value in the array is a finite number, otherwise return false.

 var finiteNums = [4,-3,2.2]
 var finiteNumsExceptOne = [4,-3,2.2,NaN]
 areAllNumbersFinite(finiteNums) // true
 areAllNumbersFinite(finiteNumsExceptOne) // false
 */

function areAllNumbersFinite(arr){
    return arr.every((val) => Number.isFinite(val))
}

/*

 Write a function called convertArrayLikeObject which accepts a single parameter, an array like object. The function should return the array like object converted to an array.

 var divs = document.getElementsByTagName('div')
 divs.reduce // undefined

 var converted = convertArrayLikeObject(divs)
 converted.reduce // funciton(){}...
 */

function convertArrayLikeObject(obj){
    return Array.from(obj);
}

/*

 Write a function called displayEvenArguments which accepts a variable number of arguments and returns a new array with all of the arguments that are even numbers.

 displayEvenArguments(1,2,3,4,5,6) // [2,4,6]
 displayEvenArguments(7,8,9) // [8]
 displayEvenArguments(1,3,7) // []
 */

function displayEvenArguments(...args){
    return args.filter((val) => val % 2 == 0);
}
```
</details>


