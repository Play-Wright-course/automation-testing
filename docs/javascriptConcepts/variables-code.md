# JavaScript: var, let, const – Code Snippets with Output

## 1. var Scope
```javascript
function testVarScope() {
  if (true) {
    var x = 10;
  }
  console.log("var x =", x);
}
testVarScope();
```

Output:
```
var x = 10
```

## 2. let Scope
```javascript
function testLetScope() {
  if (true) {
    let y = 20;
    console.log("Inside block y =", y);
  }
}
testLetScope();
```

Output:
```
Inside block y = 20
```

## 3. Hoisting
```javascript
console.log(a);
var a = 5;
```

Output:
```
undefined
```

## 4. let TDZ
```javascript
let b = 10;
```

## 5. Redeclaration
```javascript
var name = "Nitin";
var name = "Patil";
let city = "Pune";
city = "Mumbai";
```

## 6. Global Behavior
```javascript
var aVar = 100;
let aLet = 200;
```

## 7. Shadowing
```javascript
var x = 1;
function demo() {
  var x = 2;
  console.log("Inside function x =", x);
}
demo();
console.log("Outside x =", x);
```

## 8. const Example
```javascript
const user = { name: "Nitin", city: "Pune" };
user.city = "Mumbai";
console.log(user);
```

## 9. Closure (var)
```javascript
for (var i = 1; i <= 3; i++) {
  setTimeout(() => console.log("var i =", i), 100);
}
```

## 10. Closure (let)
```javascript
for (let i = 1; i <= 3; i++) {
  setTimeout(() => console.log("let i =", i), 100);
}
```

## 11. Final Example
```javascript
var v = 1;
let l = 2;
const c = 3;
function show() {
  if (true) {
    var v = 10;
    let l = 20;
    const c2 = 30;
    console.log(v, l, c2);
  }
  console.log(v);
}
show();
```
