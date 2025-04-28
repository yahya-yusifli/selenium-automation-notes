# Finding Elements by ID

The `id` attribute is one of the fastest and most reliable ways to locate a web element.  
IDs are expected to be unique on a page.

Example:
```java
WebElement usernameField = driver.findElement(By.id("inputUsername"));
usernameField.sendKeys("testuser");

