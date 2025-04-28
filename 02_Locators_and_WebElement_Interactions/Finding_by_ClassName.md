# Finding Elements by Class Name

- Locates elements using the `class` attribute.
- If an element has multiple classes, prefer CSS Selector instead.

### Example:
```java
WebElement loginButton = driver.findElement(By.className("submitBtn"));
loginButton.click();
