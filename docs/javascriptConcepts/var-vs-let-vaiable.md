# Difference Between `var` and `let` in JavaScript

## 1. Scope

-   **var**
    -   Function-scoped
    -   Available anywhere inside the function
-   **let**
    -   Block-scoped
    -   Available only inside the `{ }` block where it is declared

## 2. Hoisting

-   **var**
    -   Hoisted and initialized with `undefined`
    -   Can be accessed before declaration (but will be `undefined`)
-   **let**
    -   Hoisted but *not initialized*
    -   Cannot be accessed before declaration (Temporal Dead Zone)

## 3. Re-Declaration

-   **var**
    -   Allows re-declaration in the same scope
-   **let**
    -   Does not allow re-declaration in the same scope

## 4. Global Object Property (Browser)

-   **var**
    -   Declared globally → becomes property of `window` object
-   **let**
    -   Declared globally → does **not** attach to `window`

## 5. Recommended Usage

-   `var` → Not preferred; avoid using in modern JS
-   `let` → Use for variables whose values will change
-   `const` → Prefer for fixed or constant values

## Comparison Table

  -----------------------------------------------------------------------
  Feature                   `var`                  `let`
  ------------------------- ---------------------- ----------------------
  Scope                     Function-scoped        Block-scoped

  Hoisting                  Yes (initialized with  Yes (uninitialized,
                            `undefined`)           TDZ)

  Re-declaration            Allowed                Not allowed

  Global window property    Yes                    No

  Modern usage              Not recommended        Recommended
  -----------------------------------------------------------------------
