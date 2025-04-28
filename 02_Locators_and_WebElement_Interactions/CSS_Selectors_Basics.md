# CSS Selectors Basics

- CSS Selectors are faster and more flexible than XPath.
- Used for locating elements by id, class, attributes, etc.

### Examples:
```java
driver.findElement(By.cssSelector("input[placeholder='Email']")).sendKeys("test@email.com");
driver.findElement(By.cssSelector(".submitBtn")).click();
driver.findElement(By.cssSelector("#username")).sendKeys("myUser");
