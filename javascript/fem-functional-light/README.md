# Functional-light JS

[Course link](https://frontendmasters.com/courses/functional-javascript-v2)

[Book link](https://github.com/getify/Functional-Light-JS/tree/master/manuscript)

To do:

Something on composition
Something on partial application
Something on currying

## partial application

Some now, some later

A partial utility taken from [getify](https://github.com/getify/Functional-Light-JS/blob/master/manuscript/ch3.md/#user-content-curry)

```js
function partial(fn,...presetArgs) {
    return function partiallyApplied(...laterArgs){
        return fn( ...presetArgs, ...laterArgs );
    };
}

// or the ES6 => arrow form
var partial =
    (fn,...presetArgs) =>
        (...laterArgs) =>
            fn( ...presetArgs, ...laterArgs );
```

`partial` takes a function and n number of arguments (gathered together in `presentArgs`), then it returns a function with the `presentArgs` already applied. This returned function will then take a further n arguments and will run the originally supplied function with both the original args and the new args.

Usage of partial:

```js
var getPerson = partial( ajax, "http://some.api/person" );
```

Returns a function with the arg `"http://some.api/person"` already applied. When called it will run the already supplied `ajax` function with the already applied arg (`"http://some.api/person"`), and any extra arguments supplied.

And now the tricky bit.
Imagine you in an edge case you want to provide the data arg ahead of time, for example in a getCurrentUser function. Compare these two:

```js
function getPerson(data,cb) {
    ajax( "http://some.api/person", data, cb );
}

function getCurrentUser(cb) {
    getPerson( { user: CURRENT_USER_ID }, cb );
}
```

the `getCurrentUser` function calls `getPerson` and passes pre-set data and the callback. We could use a partial to do this:

```js
// version 1
var getCurrentUser = partial(
    ajax,
    "http://some.api/person",
    { user: CURRENT_USER_ID }
);

// version 2
var getCurrentUser = partial( getPerson, { user: CURRENT_USER_ID } );
```