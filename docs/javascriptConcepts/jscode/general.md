page.locator("<hmlTag>:'<text>'"  -> new playwright method to point locatr.
isVisible -> true/false
waitFor()  -> Methods help to to load element. Example. page.locator("  ").first().waitFor()

pressSequentially() -> type/fill wors in serach boc with sequentially
Example "ind2"  -> i later n later d  -> fill directly past ind --> It helps to handle autosuggestion dropdown.


getByLabel
getByPlaceholder
getByRole

playwrigh debugg/trace/ui

filters - in locator use to filter from multiple WebElement


js-config file

default timeout is 30 sec,
we can override in js configs with timeout and there is one more timeout for assertion,
``` yaml
timeout: 40*1000,
expect: {
  timeout: 40*1000,
}
```
