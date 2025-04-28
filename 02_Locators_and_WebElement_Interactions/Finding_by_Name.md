## 3. `Finding_by_Name.md`
```markdown
# Finding Elements by Name

The `name` attribute can be used if `id` is not available.  
It is especially common in form fields.

Example:
```java
WebElement passwordField = driver.findElement(By.name("inputPassword"));
passwordField.sendKeys("mypassword");

