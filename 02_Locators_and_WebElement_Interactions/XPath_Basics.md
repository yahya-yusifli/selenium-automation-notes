# XPath Basics

- XPath is used to navigate through elements and attributes.
- It supports complex and dynamic element identification.

### Examples:
```java
driver.findElement(By.xpath("//input[@id='username']")).sendKeys("testUser");
driver.findElement(By.xpath("//button[text()='Sign In']")).click();
