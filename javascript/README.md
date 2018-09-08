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