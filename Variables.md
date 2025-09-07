# 2. Variables (var, let, const) – Deep Dive

JavaScript provides three ways to declare variables: `var`, `let`, and `const`.  
While all can store values, they differ in **scope**, **re-declaration rules**, **hoisting behavior**, and **mutability**.  

---

## 🔹 var
- **Function-scoped**: A `var` declared inside a function is available throughout the function.  
- **Ignores block scope**: Declaring inside `if`, `for`, or `{}` does not limit its scope.  
- **Hoisted**: Moved to the top of the scope during compilation, initialized with `undefined`.  
- **Allows re-declaration**: You can declare the same variable again in the same scope (not recommended).  

### Example – var inside block
```js
if (true) {
  var x = "Hello";
}
console.log(x); // ✅ Accessible outside block
Example – var inside function
js
Copy code
function testVar() {
  if (true) {
    var inside = "Function scope";
  }
  console.log(inside); // ✅ Accessible anywhere inside the function
}
testVar();
console.log(typeof inside); // ❌ undefined globally
Example – global var usage
js
Copy code
var globalVar = "I am global";

function showGlobal() {
  console.log(globalVar); // ✅ Accessible inside function
}

showGlobal();
console.log(globalVar); // ✅ Accessible globally
🔹 let
Block-scoped: Respects {} blocks like if, for, while.

No re-declaration: Cannot be declared twice in the same scope.

Hoisted but uninitialized: Exists in the Temporal Dead Zone (TDZ) until execution reaches its line.

Reassignment allowed.

Example – let inside block
js
Copy code
if (true) {
  let y = "Inside block";
  console.log(y); // ✅ Accessible here
}
// console.log(y); // ❌ ReferenceError outside block
Example – let reassignment
js
Copy code
let age = 25;
age = 30; // ✅ Reassignment allowed
// let age = 35; // ❌ Cannot redeclare in same scope
🔹 const
Block-scoped (like let).

Must be initialized at declaration.

Cannot be reassigned, but if it’s an object/array, its contents can still be modified.

Example – const
js
Copy code
const country = "India";
// country = "USA"; // ❌ Error: Cannot reassign

const obj = { name: "Nitin" };
obj.name = "Patil"; // ✅ Allowed (property changed)
console.log(obj);   // { name: "Patil" }
🔹 Global vs Local with var
Declaring a variable with var outside any function makes it global.

Reassigning it inside a function changes the global variable.

Re-declaring with var inside a function shadows the global variable instead of modifying it.

Example – Reassignment updates global
js
Copy code
var name = "Nitin";  // global

function updateGlobal() {
  name = "Patil";   // reassigns global
}
updateGlobal();
console.log(name);  // ✅ Patil (global updated)
Example – Shadowing with var
js
Copy code
var name = "Nitin";  // global

function shadowGlobal() {
  var name = "Local";  // new local variable
  console.log("Inside:", name); // Local
}
shadowGlobal();
console.log("Outside:", name);  // Nitin (global unchanged)
✅ Summary
var → function-scoped, hoisted, allows re-declaration, unsafe in blocks.

let → block-scoped, safer, hoisted but uninitialized until line of code.

const → block-scoped, must be initialized, immutable binding but mutable objects.

Global vars can be reassigned inside functions.

Re-declaring with var inside a function shadows the global variable.
