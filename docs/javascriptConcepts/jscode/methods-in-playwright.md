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
    - To avoid failure in above step we have to add wait till all api network call done.
      ```js
      await page.goto("https://rahulshettyacademy.com/client");
      await page.locator("#userEmail").fill("anshika@gmail.com");
      await page.locator("#userPassword").fill("Iamking@000");
      await page.locator("[value='Login']").click();
      await page.waitForLoadState('networkidle');
      const titles=await page.locator(".card-body b").allTextContents();
      concole.log(titles);
      ```
