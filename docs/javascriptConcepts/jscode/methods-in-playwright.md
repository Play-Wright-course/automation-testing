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
  await page.locator(".card-body a").nth(0).textContent  - It return 1st element/index bases
  OR
  await page.locator(".card-body a").first().textContent - It return 1st element
  OR
  await page.locator(".card-body a").last().textContent - It return last element
  ```

  - Scenario Want to store all product text in list etc.
     -  locator.alltextContents();
       ``` js
       console.log(await cardTitles.nth(1).textContent()); //textContent() by default have wait mechanism
       const allTitle=await page.locator(".card-body a").alltextContents(); // It didint not have and It will fail if we run only this line
       ```
