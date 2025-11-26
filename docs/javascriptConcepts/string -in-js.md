# JavaScript Strings --- Complete Guide

## 1. What is a String?

A **string** in JavaScript is a sequence of characters used to represent
text.\
Example:

``` js
let name = "Nitin";
```

------------------------------------------------------------------------

## 2. String Declaration Methods

### **a) Single Quotes**

``` js
let city = 'Pune';
```

### **b) Double Quotes**

``` js
let job = "Developer";
```

### **c) Backticks (Template Literals)**

Supports: - multiline strings\
- interpolation (`${variable}`)

``` js
let user = "Nitin";
let msg = `Hello ${user}, welcome!`;
```

------------------------------------------------------------------------

## 3. String Immutability

Strings in JavaScript **cannot be changed after creation**.

``` js
let s = "Hi";
s[0] = "h"; // ❌ does nothing
console.log(s); // "Hi"
```

To modify a string, create a new one:

``` js
s = "h" + s[1];
console.log(s); // "hi"
```

------------------------------------------------------------------------

## 4. String Comparison

### **== (loose equality)**

Converts types before comparison.

``` js
"10" == 10   // true
```

### **=== (strict equality)**

No type conversion.

``` js
"10" === 10  // false
```

### **localeCompare()**

Used for lexicographical comparison:

``` js
"apple".localeCompare("banana"); // -1
```

------------------------------------------------------------------------

## 5. String Methods --- Detailed With Examples

------------------------------------------------------------------------

### **1. charAt(index)**

Returns character at given index.

``` js
"Hello".charAt(1); // 'e'
```

------------------------------------------------------------------------

### **2. at(index)**

Supports negative index.

``` js
"Hello".at(-1); // 'o'
```

------------------------------------------------------------------------

### **3. indexOf()**

Finds first occurrence.

``` js
"javascript".indexOf("a"); // 1
```

------------------------------------------------------------------------

### **4. lastIndexOf()**

Finds last occurrence.

``` js
"javascript".lastIndexOf("a"); // 3
```

------------------------------------------------------------------------

### **5. includes()**

Checks substring present or not.

``` js
"hello world".includes("world"); // true
```

------------------------------------------------------------------------

### **6. startsWith()**

``` js
"JavaScript".startsWith("Java"); // true
```

### **7. endsWith()**

``` js
"JavaScript".endsWith("Script"); // true
```

------------------------------------------------------------------------

### **8. slice(start, end)**

Supports negative index.

``` js
"JavaScript".slice(0, 4); // 'Java'
"JavaScript".slice(-6);  // 'Script'
```

------------------------------------------------------------------------

### **9. substring(start, end)**

Negative values treated as 0.

``` js
"JavaScript".substring(4, 10); // "Script"
```

------------------------------------------------------------------------

### **10. substr(start, length)**

(Deprecated but asked in interviews)

``` js
"JavaScript".substr(4, 6); // "Script"
```

------------------------------------------------------------------------

### **11. toUpperCase() / toLowerCase()**

``` js
"hello".toUpperCase(); // "HELLO"
```

------------------------------------------------------------------------

### **12. trim()**

``` js
"   hi   ".trim(); // "hi"
```

### **trimStart()**

``` js
"   hi".trimStart();
```

### **trimEnd()**

``` js
"hi   ".trimEnd();
```

------------------------------------------------------------------------

### **13. replace()**

Replaces first match.

``` js
"hello world".replace("world","JS");
```

### **replaceAll()**

``` js
"aa11aa".replaceAll("a","b");
```

------------------------------------------------------------------------

### **14. split()**

Converts string → array.

``` js
"apple,mango".split(","); 
```

------------------------------------------------------------------------

### **15. concat()**

``` js
"Hello".concat(" JavaScript");
```

------------------------------------------------------------------------

### **16. match()**

Regex matching.

``` js
"abc123".match(/[0-9]+/);
```

------------------------------------------------------------------------

### **17. matchAll()**

``` js
[... "a1b2".matchAll(/[a-z]/g)];
```

------------------------------------------------------------------------

### **18. padStart()**

``` js
"7".padStart(3,"0"); // "007"
```

### **19. padEnd()**

``` js
"7".padEnd(3,"0"); // "700"
```

------------------------------------------------------------------------

### **20. repeat()**

``` js
"ha".repeat(3); // "hahaha"
```

------------------------------------------------------------------------

### **21. localeCompare()**

Lexicographic comparison.

``` js
"apple".localeCompare("banana"); // -1
```

------------------------------------------------------------------------

### **22. valueOf()**

Returns primitive string.

``` js
"hello".valueOf();
```

------------------------------------------------------------------------

### **23. toString()**

``` js
(100).toString();
```

------------------------------------------------------------------------

## 6. String Methods Table (Cheat Sheet)

  Method                Description                Example
  --------------------- -------------------------- ----------------------------
  **charAt()**          Returns char at index      `"Hi".charAt(1)`
  **at()**              Supports negative index    `"Hi".at(-1)`
  **indexOf()**         First occurrence           `"test".indexOf("t")`
  **lastIndexOf()**     Last occurrence            `"test".lastIndexOf("t")`
  **includes()**        True if substring exists   `"abc".includes("b")`
  **startsWith()**      Checks starting            `"Java".startsWith("J")`
  **endsWith()**        Checks ending              `"Java".endsWith("a")`
  **slice()**           Extracts part              `"Java".slice(1,3)`
  **substring()**       Similar to slice           `"Java".substring(1,3)`
  **substr()**          start + length             `"JavaScript".substr(4,6)`
  **toUpperCase()**     Uppercase                  `"hi".toUpperCase()`
  **toLowerCase()**     Lowercase                  `"HI".toLowerCase()`
  **trim()**            Removes spaces             `" hi ".trim()`
  **replace()**         Replace first match        `"aabb".replace("a","c")`
  **replaceAll()**      Replace all                `"aa".replaceAll("a","b")`
  **split()**           String → array             `"a,b".split(",")`
  **concat()**          Joins strings              `"a".concat("b")`
  **match()**           Regex match                `"abc".match(/a/)`
  **matchAll()**        All regex matches          `[...str.matchAll(/a/g)]`
  **padStart()**        Left padding               `"5".padStart(3,"0")`
  **padEnd()**          Right padding              `"5".padEnd(3,"0")`
  **repeat()**          Repeat string              `"ha".repeat(3)`
  **localeCompare()**   Compare strings            `"a".localeCompare("b")`

------------------------------------------------------------------------

## 7. Small Interview Programs

### Reverse string

``` js
str.split("").reverse().join("");
```

### Check palindrome

``` js
function isPalindrome(s){ return s === s.split("").reverse().join(""); }
```

### Count vowels

``` js
(str.match(/[aeiou]/gi) || []).length;
```

### Character frequency

``` js
for(let ch of str){ map[ch]=(map[ch]||0)+1; }
```

### First non-repeating character

``` js
for(let c of str){
  if(str.indexOf(c)===str.lastIndexOf(c)) return c;
}
```

------------------------------------------------------------------------

# End of Document
