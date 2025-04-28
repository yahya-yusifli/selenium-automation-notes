# Finding Elements by Name

- Use `name` attribute if `id` is missing.
- Commonly used in form fields.

### Example:
```java
WebElement passwordField = driver.findElement(By.name("inputPassword"));
passwordField.sendKeys("mypassword123");
