# 2. Variables (var, let, const) – Deep Dive

JavaScript provides three ways to declare variables: `var`, `let`, and `const`.  
While all can store values, they differ in **scope**, **re-declaration rules**, **hoisting behavior**, and **mutability**.  

---

## 🔹 var
- **Function-scoped**: A `var` declared inside a function is available throughout the function.  
- **Ignores block scope**: Declaring inside `if`, `for`, or `{}` does not limit its scope.  
- **Hoisted**: Moved to the top of the scope during compilation, initialized with `undefined`.  
- **Allows re-declaration**: You can declare the same variable again in the same scope (bad practice).  

### Example – var inside block
```javascript
if (true) {
  var x = "Hello";
}
console.log(x); // ✅ Accessible outside block
