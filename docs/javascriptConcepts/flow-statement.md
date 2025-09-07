# 4. Control Flow in JavaScript – Deep Dive

Control flow determines **the order in which code executes**.  
JavaScript provides control flow statements like **if...else, switch, loops (for, while, do...while), break/continue**.  

---

## 🔹 `if` Statement
Executes a block of code if a condition is true.

### Syntax
```javascript
if (condition) {
  // code to run if condition is true
}
```

### Example – `if`
```javascript
let score = 85;

if (score >= 50) {
  console.log("Pass");
}
```

**Playwright Use Case:** Check if an element exists before performing an action.

---

## 🔹 `if...else` Statement
Executes one block if condition is true, another if false.

### Syntax
```javascript
if (condition) {
  // code if true
} else {
  // code if false
}
```

### Example – `if...else`
```javascript
let score = 40;

if (score >= 50) {
  console.log("Pass");
} else {
  console.log("Fail");
}
```

---

## 🔹 `if...else if...else` Statement
Used when multiple conditions need to be checked sequentially.

### Syntax
```javascript
if (condition1) {
  // code1
} else if (condition2) {
  // code2
} else {
  // default code
}
```

### Example – `if...else if...else`
```javascript
let marks = 75;

if (marks >= 90) {
  console.log("Grade A");
} else if (marks >= 75) {
  console.log("Grade B");
} else if (marks >= 50) {
  console.log("Grade C");
} else {
  console.log("Fail");
}
```

---

## 🔹 `switch` Statement
An alternative to multiple `if...else if` conditions.  

### Syntax
```javascript
switch(expression) {
  case value1:
    // code
    break;
  case value2:
    // code
    break;
  default:
    // code if no case matches
}
```

### Example – `switch`
```javascript
let day = 3;

switch(day) {
  case 1:
    console.log("Monday");
    break;
  case 2:
    console.log("Tuesday");
    break;
  case 3:
    console.log("Wednesday");
    break;
  default:
    console.log("Another day");
}
```

**Playwright Use Case:** Decide which browser or test scenario to run based on a config variable.

---

## 🔹 `for` Loop
Repeats a block of code a fixed number of times.

### Syntax
```javascript
for (initialization; condition; increment) {
  // code block
}
```

### Example – `for`
```javascript
for (let i = 1; i <= 5; i++) {
  console.log("Count:", i);
}
```

**Playwright Use Case:** Iterate through a list of elements to perform actions like click or validate text.

---

## 🔹 `while` Loop
Repeats as long as a condition is true.

### Syntax
```javascript
while (condition) {
  // code block
}
```

### Example – `while`
```javascript
let i = 1;
while (i <= 5) {
  console.log("Count:", i);
  i++;
}
```

---

## 🔹 `do...while` Loop
Executes the code block **at least once**, then checks the condition.

### Syntax
```javascript
do {
  // code block
} while (condition);
```

### Example – `do...while`
```javascript
let i = 6;
do {
  console.log("Count:", i);
  i++;
} while (i <= 5);  // runs once even though condition is false
```

---

## 🔹 `break` and `continue`
**JavaScript `break` and `continue` work the same way as in Java.**
- **`break`** → exits the loop immediately  
- **`continue`** → skips the current iteration and moves to next

### Example – `break` & `continue`
```javascript
for (let i = 1; i <= 5; i++) {
  if (i === 3) break;      // stops loop at 3
  console.log(i);
}

for (let i = 1; i <= 5; i++) {
  if (i === 3) continue;   // skips 3
  console.log(i);
}
```

**Java Example (for comparison)**
```java
for (int i = 1; i <= 5; i++) {
    if (i == 3) break; // exits loop at 3
    System.out.println(i);
}

for (int i = 1; i <= 5; i++) {
    if (i == 3) continue; // skips 3
    System.out.println(i);
}
```

---

## ✅ Summary
- **Conditional Statements:** `if`, `if...else`, `if...else if...else`, `switch`  
- **Loops:** `for`, `while`, `do...while`  
- **Loop Control:** `break`, `continue`  

These control flow statements are essential for **decision-making and iteration** in JavaScript and Playwright tests.

