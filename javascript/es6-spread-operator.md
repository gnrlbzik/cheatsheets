# ES6 - Spread Operator

## links

- ARTICLE SOURCE: http://www.snappyjs.com/2018/03/28/cheatsheet-object-rest-spread-in-javascript/
- MOZ DOCS: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax
- MICROSOFT DOCS: https://docs.microsoft.com/en-us/scripting/javascript/reference/spread-operator-decrement-dot-dot-dot-javascript
- COMPATABILITY: http://kangax.github.io/compat-table/es6/#test-spread_(...)_operator
- ECMA: https://github.com/tc39/proposal-object-rest-spread / http://www.ecma-international.org/ecma-262/6.0/#sec-argument-lists-runtime-semantics-argumentlistevaluation

## compatibility

Currently requires javascript transpiling, es6 feature.


``` javascript
npm install --save-dev babel-plugin-transform-object-rest-spread

// And then in your .babelrc
{
  "plugins": ["transform-object-rest-spread"]
}
```

## cheatsheet

### spreading arrays

``` javascript
const lowNumbers = [ 1, 2, 3];
const highNumbers = [4, 5, 6];
const [ one, ...restOfNumbers] = lowNumbers;
one; // 1
restOfNumbers; // [2, 3]
```

### copying arrays

``` javascript
const lowNumbers = [ 1, 2, 3];
const cpy = [...lowNumbers]
cpy; // [1, 2, 3]

// Caveats -> The arrays are not "deep copied"
const deepArray = [[1], [2], [3]];
const notDeepCopy = [...deepArray];
notDeepCopy[0][0] = 9;
notDeepCopy; // [[9], [2], [3]]
deepArray; // WARNING: [[9], [2], [3]]
```

### merging arrays

``` javascript
const lowNumbers = [ 1, 2, 3];
const highNumbers = [4, 5, 6];
const merged = [ ...lowNumbers, ...highNumbers];
merged; // [1, 2, 3, 4, 5, 6];
```

### spreading over function

``` javascript
const lowNumbers = [ 1, 2, 3];
function myFunction(x, y, z) { console.log(`${x}, ${y}, ${z}`); };
myFunction(...lowNumbers); // 1, 2, 3
```

Keep an extra eye out on that caveat, we’re not deep copying arrays when spreading.

### object spread

``` javascript
const volvo = {
    make: 'Volvo',
    model: 'XC90',
    mileage: 2500,
    color: 'green'
};

const { make, model, ...restOfvolvo } = volvo;
make; // Volvo
model; // XC90
restOfvolvo; // { mileage: 2500, color: 'green' }
//const { ...restOfvolvoStart, make, model } = volvo; // Not allowed

// New variable names when spreading
const { make : newMakeName, model : newModelName } = volvo;
newMakeName; // Volvo
newModelName; // XC90
```

### copying objects

``` javascript
const volvo = {
    make: 'Volvo',
    model: 'XC90',
    mileage: 2500,
    color: 'green'
};
const volvoCopy = { ... volvo };
volvoCopy; // { make: 'Volvo', model: 'XC90', mileage: 2500, color: 'green' }

// Caveats -> They objects are not "deep copied".
const audi = {
    make: 'Audi',
    engine: {
        type: 'diesel'
    },
    color: 'navy'
};
const notDeepCopyObject = { ...volvo, ...audi };
audi.engine.type = 'petrol'; // WARNING: No deep copy
audi.color = 'brown'; // OK
notDeepCopyObject; // {make: 'Audi', model: 'XC90', mileage: 2500, color: 'navy', engine: { type: 'petrol' }}
```

### merging objects

``` javascript
const volvo = {
    make: 'Volvo',
    model: 'XC90',
    mileage: 2500,
    color: 'green'
};
const bmw = {
    make: 'bmw',
    color: 'blue'
};
const hybrid = { ...volvo, ...bmw};
hybrid; //{ make: 'bmw', model: 'XC90', mileage: 2500, color: 'blue'}
```

### spreading args in function

``` javascript
// Spreading args in function
function moreArgs(a, b, ...multiple) {
    console.log(multiple.map(arg => arg));
}
moreArgs('a', 'b', 'c', 'd', 'e', 'f'); // ['c', 'd', 'e', 'f']
```