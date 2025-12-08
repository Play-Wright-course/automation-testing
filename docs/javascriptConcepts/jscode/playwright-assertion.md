# Playwright Assertions — Complete Guide

## Locator Assertions

| Assertion | Description | Syntax | Example |
|----------|-------------|--------|---------|
| **toBeVisible()** | Element should be visible | `await expect(locator).toBeVisible()` | ```js
await expect(page.getByText("Login")).toBeVisible();
``` |
| **toBeHidden()** | Element exists but not visible | `await expect(locator).toBeHidden()` | ```js
await expect(page.locator('#loader')).toBeHidden();
``` |
| **toBeEnabled()** | Element is enabled | `await expect(locator).toBeEnabled()` | ```js
await expect(page.locator('#submit')).toBeEnabled();
``` |
| **toBeDisabled()** | Element is disabled | `await expect(locator).toBeDisabled()` | ```js
await expect(page.locator('#submit')).toBeDisabled();
``` |
| **toBeEditable()** | Input is editable | `await expect(locator).toBeEditable()` | ```js
await expect(page.locator('#name')).toBeEditable();
``` |
| **toBeChecked()** | Checkbox is checked | `await expect(locator).toBeChecked()` | ```js
await expect(page.locator('#terms')).toBeChecked();
``` |
| **not.toBeChecked()** | Checkbox not checked | `await expect(locator).not.toBeChecked()` | ```js
await expect(page.locator('#subscribe')).not.toBeChecked();
``` |
| **toHaveAttribute()** | Matches attribute value | `await expect(locator).toHaveAttribute(name, value)` | ```js
await expect(page.locator('#loginBtn')).toHaveAttribute('type','submit');
``` |
| **toHaveClass()** | Matches CSS class | `await expect(locator).toHaveClass(value)` | ```js
await expect(page.locator('.item')).toHaveClass(/active/);
``` |
| **toHaveId()** | Matches element id | `await expect(locator).toHaveId(value)` | ```js
await expect(page.locator('#username')).toHaveId('username');
``` |
| **toHaveText()** | Exact/regex text match | `await expect(locator).toHaveText(value)` | ```js
await expect(page.locator('.msg')).toHaveText(/Success/);
``` |
| **toContainText()** | Partial text match | `await expect(locator).toContainText(value)` | ```js
await expect(page.locator('.label')).toContainText("Hello");
``` |
| **toHaveValue()** | Input value match | `await expect(locator).toHaveValue(value)` | ```js
await expect(page.locator('#email')).toHaveValue("test@gmail.com");
``` |
| **toHaveValues()** | Multi-select values | `await expect(locator).toHaveValues(array)` | ```js
await expect(page.locator('#cities')).toHaveValues(['NY', 'LA']);
``` |
| **toHaveCount()** | Number of elements | `await expect(locator).toHaveCount(number)` | ```js
await expect(page.locator('.cart-item')).toHaveCount(3);
``` |
| **toBeEmpty()** | No content | `await expect(locator).toBeEmpty()` | ```js
await expect(page.locator('#output')).toBeEmpty();
``` |
| **toBeInViewport()** | Element inside viewport | `await expect(locator).toBeInViewport()` | ```js
await expect(page.locator('#banner')).toBeInViewport();
``` |

## Page Assertions

| Assertion | Description | Syntax | Example |
|----------|-------------|--------|---------|
| **toHaveURL()** | Matches URL | `await expect(page).toHaveURL(value)` | ```js
await expect(page).toHaveURL(/dashboard/);
``` |
| **toHaveTitle()** | Matches page title | `await expect(page).toHaveTitle(value)` | ```js
await expect(page).toHaveTitle("Login Page");
``` |

## API Assertions

| Assertion | Description | Syntax | Example |
|----------|-------------|--------|----------|
| **toBeOK()** | Status is 2xx | `await expect(response).toBeOK()` | ```js
const res = await request.get(url);
await expect(res).toBeOK();
``` |
| **status() code** | Exact HTTP code | `expect(response.status()).toBe(value)` | ```js
expect(res.status()).toBe(201);
``` |
| **json body check** | Validate JSON | `expect(await res.json()).toEqual(obj)` | ```js
const body = await res.json();
expect(body.success).toBe(true);
``` |

## Soft Assertions

| Feature | Syntax | Example |
|---------|--------|---------|
| Soft assertion | `expect.soft(locator).assertion()` | ```js
expect.soft(page.locator('#msg')).toContainText('Success');
console.log("Test continues");
``` |

## Negated Assertions

| Negated Syntax | Example |
|----------------|---------|
| `expect(locator).not.toBeVisible()` | ```js
await expect(page.locator('#error')).not.toBeVisible();
``` |
| `expect(locator).not.toHaveText(value)` | ```js
await expect(page.locator('#msg')).not.toHaveText('Error');
``` |
| `expect(page).not.toHaveURL(value)` | ```js
await expect(page).not.toHaveURL(/login/);
``` |

## Assertions With Timeout

| Syntax | Example |
|--------|---------|
| `await expect(locator).assertion({ timeout: ms })` | ```js
await expect(page.locator('#status')).toHaveText("Done", { timeout: 8000 });
``` |


