- type - entering values
- click - click
- textContent() - get text from locator
- expect to containText aseertion
  ```js
  await expect(locator).toContainText("expected string");
  ```

- if we use lovator which matches to multiple element in dom and we tring to get string we get below error,
  ``` error
  STRINCT MODE VIOLATION
  ```

  - How we can travel from parent to child in playwright with css
  ```
  await page.locator(".card-body a").nth(0).textContent
  ```
