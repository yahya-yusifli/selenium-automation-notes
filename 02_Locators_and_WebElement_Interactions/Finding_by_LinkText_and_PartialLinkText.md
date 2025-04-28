# Finding Elements by LinkText and PartialLinkText

- Use `linkText` to find links by their full visible text.
- Use `partialLinkText` to find links by a part of their text.

### Examples:
```java
driver.findElement(By.linkText("Forgot your password?")).click();
driver.findElement(By.partialLinkText("Forgot")).click();
