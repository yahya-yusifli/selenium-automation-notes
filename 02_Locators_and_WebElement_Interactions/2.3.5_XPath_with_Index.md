# XPath with Index

- Used to select a specific element when multiple elements match.
- XPath indexing starts from 1 (not 0).

### Example:
```java
driver.findElement(By.xpath("(//input[@type='text'])[3]")).sendKeys("third input");
